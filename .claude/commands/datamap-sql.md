---
description: 在数据地图平台自动写SQL查数、导出数据、分析结果
argument-hint: [SQL查询需求描述]
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, AskUserQuestion
---

# 数据地图 SQL 自动查数助手

你是一个能通过 agent-browser 自动操作数据地图平台写 SQL 查数的助手。

## 用户需求

$ARGUMENTS

## 自动初始化（每次运行自动完成）

### 第1步：检查 agent-browser 是否可用

```bash
agent-browser --version
```

如果命令不存在，自动安装：

```bash
cd "项目根目录" && npm install
```

安装完成后再次验证。如果仍失败，提示用户检查 Node.js 环境。

### 第2步：启动 Chrome 并连接

使用独立 Chrome 配置目录（保存登录状态，不影响日常浏览器）：

```bash
# 检查 9222 端口是否已被占用（Chrome 是否已在运行）
netstat -an | grep 9222 | grep LISTENING
```

如果端口未被占用，启动 Chrome：
```bash
# Windows:
start "" "chrome" --remote-debugging-port=9222 --user-data-dir=".chrome-profile" --no-first-run
# macOS:
# open -a "Google Chrome" --args --remote-debugging-port=9222 --user-data-dir="$(pwd)/.chrome-profile" --no-first-run
```

等待 4 秒后连接：
```bash
agent-browser connect 9222
```

如果端口已被占用（说明之前已启动），直接连接：
```bash
agent-browser connect 9222
```

### 第3步：检查本地配置

读取 `.claude/datamap-config.local.json`，如果不存在则执行自动初始化：

1. 打开数据地图首页：
   ```bash
   agent-browser open "http://datamap.pdt.mixiaojin.srv/"
   agent-browser wait --load networkidle
   ```

2. 获取页面快照，找到用户的笔记本：
   ```bash
   agent-browser snapshot -i
   ```

3. 从快照中找到包含 `noteId` 的笔记本链接，提取 noteId

4. 如果找到多个笔记本，用 `AskUserQuestion` 让用户选择

5. 如果页面跳转到登录页，**停止执行**并提示：
   > 请先在弹出的 Chrome 浏览器中手动登录数据地图平台，登录后重新运行 `/datamap-sql`。

6. 创建数据目录并保存配置：
   ```bash
   mkdir -p ./data
   ```
   写入 `.claude/datamap-config.local.json`：
   ```json
   {
     "noteId": "获取到的noteId",
     "dataDir": "./data"
   }
   ```

### 第4步：读取配置

从 `.claude/datamap-config.local.json` 读取 `noteId` 和 `dataDir`，后续步骤使用。

## 表结构缓存

**重要：在执行任何查询前，先读取表结构缓存文件** `.claude/docs/table-schemas.md`。
- 如果目标表已有缓存结构，直接使用，无需 DESC
- 如果是新表，先执行 DESC 获取结构，查询完成后**必须**将表结构更新到缓存文件

## 操作流程

### 第一步：导航到数据地图

```bash
agent-browser open "http://datamap.pdt.mixiaojin.srv/#/sql/query?noteId={noteId}"
agent-browser wait --load networkidle
agent-browser get title
```

确认页面标题为「SQL查询 - 数据地图」。如果跳转到登录页，**停止执行**并提示用户先手动登录。

### 第二步：写入 SQL

使用 agent-browser 的 eval 命令通过 CodeMirror API 写入 SQL：

```bash
agent-browser eval "document.querySelectorAll('.CodeMirror')[0].CodeMirror.setValue('YOUR_SQL_HERE')"
```

**注意事项：**
- 日期变量用 `${date-1}` 表示昨天，`${date}` 表示今天
- SQL 中的单引号需要转义
- 如果需要写入到已有的编辑器单元格，先找到对应 index 的 CodeMirror

### 第三步：执行 SQL

```bash
agent-browser eval "
  const cm0 = document.querySelectorAll('.CodeMirror')[0];
  let container = cm0;
  for (let i = 0; i < 10; i++) {
    container = container.parentElement;
    if (!container) break;
    const runBtn = Array.from(container.querySelectorAll('button'))
      .find(b => b.textContent.trim() === '运 行');
    if (runBtn) { runBtn.click(); break; }
  }
"
```

### 第四步：等待查询完成

- 小查询（<100行）：`agent-browser wait 5`
- 中等查询（100-1000行）：`agent-browser wait 15`
- 大查询（>1000行）：`agent-browser wait 30`

检查是否还在加载：
```bash
agent-browser eval "!!document.querySelector('.ant-spin-spinning')"
```

### 第五步：读取结果

从 Vue 组件的 dataSource 中读取数据（支持全部行，不受分页限制）：

```bash
agent-browser eval "
  const tables = document.querySelectorAll('.ant-table');
  const firstTable = tables[0];
  let el = firstTable;
  let dataSource = null;
  for (let i = 0; i < 15; i++) {
    el = el.parentElement;
    if (!el) break;
    const vueKey = Object.keys(el).find(k => k.startsWith('__vue__'));
    if (vueKey) {
      const vue = el[vueKey];
      if (vue.$data) {
        for (const key of Object.keys(vue.$data)) {
          const val = vue.$data[key];
          if (Array.isArray(val) && val.length > 0 && val[0] && typeof val[0] === 'object') {
            dataSource = val;
            break;
          }
        }
      }
      if (dataSource) break;
    }
  }
  JSON.stringify(dataSource)
"
```

将返回的 JSON 保存为本地文件，然后用 Python 解析为表格展示。

### 第六步（可选）：下载 CSV

点击结果区域的下载按钮：

```bash
agent-browser eval "
  const wrapper = document.querySelector('[id^=pannel-wrapper]');
  const icons = wrapper.querySelectorAll('.wheader__btns.operation-bar .anticon');
  const visibleIcons = Array.from(icons).filter(el => el.getBoundingClientRect().width > 0);
  const downloadBtn = visibleIcons[visibleIcons.length - 3];
  downloadBtn.click();
"
agent-browser wait 1
agent-browser snapshot -i
```

从快照中找到「导出csv」选项并点击：
```bash
agent-browser click @eN   # N 是导出csv对应的ref编号
```

下载的文件会自动保存到 `.playwright-mcp/` 目录（如果用 agent-browser 则保存到浏览器默认下载目录）。

### 第七步（可选）：本地数据分析

如果用户需要分析数据：

```bash
pip install pandas openpyxl -q 2>/dev/null
python << 'PYEOF'
import pandas as pd
df = pd.read_csv("下载的文件路径.csv", sep=",", dtype=str)
# ... 分析逻辑 ...
with pd.ExcelWriter("{dataDir}/输出文件.xlsx", engine='openpyxl') as writer:
    df.to_excel(writer, sheet_name='原始数据', index=False)
PYEOF
```

## 常用表参考

| 表名 | 数据源 | 分区 | 说明 |
|------|--------|------|------|
| `policy_db.cp_credit_variable_raw` | doris队列 | 无 | 策略执行表（key-value结构） |
| `cfc.ods_gd_case_base_df` | 消金数仓(hive) | dt | 案件基础表 |
| `dws_sxj_amount_adjust_instruction` | 消金数仓(hive) | dt | 调额指令表 |
| `ods_mifi_risk_base_di` | 消金数仓(hive) | dt | 风控基础数据日表 |
| `dwd_loan_xj_contract_fact_df` | 消金数仓(hive) | dt | 现金贷合同事实表 |
| `dwd_loan_user_contract_fact_df` | 消金数仓(hive) | dt | 用户合同事实表 |
| `ods_loan_order_info_df` | 消金数仓(hive) | dt | 订单信息表 |

**注意：** hive表必须加 `WHERE dt = '${date-1}'` 分区条件，否则报错「分区表没有分区条件约束」。Doris表（如policy_db开头的）无此限制。

## 表结构记录规范

每次查询新表后，必须将表结构记录到 `.claude/docs/table-schemas.md`，包括：
1. 表名、数据源、是否有分区
2. 完整字段列表（字段名、类型、说明）
3. 业务含义（如枚举值：MXJ_result 1=通过，2=拒绝，-1=未处理，7=其他）

### 自动同步到 GitHub

更新表结构文件后，**必须**自动提交并推送到 GitHub，让团队其他人同步：

```bash
cd "项目根目录"
git add .claude/docs/table-schemas.md
git commit -m "docs: 更新表结构 - [表名]"
git pull --rebase origin main && git push origin main
```

如果 push 失败（比如没有配置 git 凭证），提示用户：
> 表结构已更新到本地，但推送到 GitHub 失败。请配置 git 凭证后手动 push：
> ```
> git push origin main
> ```

## 错误处理

- 如果页面跳转到登录页，提示用户需要先手动登录
- 如果查询超时，提示用户检查 SQL 是否正确
- 如果数据源不可用，提示用户切换数据源（页面左上角下拉框）

## 输出格式

查询完成后，以清晰的表格形式展示结果，并根据数据内容提供简要分析。如果用户要求下载，确认文件已保存并告知路径。
