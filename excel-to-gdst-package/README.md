# Excel to GDST Converter

将 Excel 规则表转换为 GDST 决策表文件。

## 文件说明

- `excel_to_gdst_v2.py` - 主转换脚本
- `SKILL.md` - 详细使用文档

## 快速使用

```bash
python excel_to_gdst_v2.py 规则表.xlsx
```

## Excel 格式要求

| 列位置 | 内容 | 必需 |
|--------|------|------|
| 第1行 | 元数据（可选） | 否 |
| 第2行 | 表头：规则名、条件、...、结果 | 是 |

表头必须包含 `规则名` 和 `结果` 两列。

## 示例

```
| 规则名 | 条件 | 车分层 | 蚂蚁星河标签 | 结果 |
|--------|------|--------|--------------|------|
| myxh_AmtIndex_A | v.get("risk_group")=="A" | | v.get("myxh_risk_seg")==1 | myxh_amtindex_a=1.2 |
```

## 输出

生成 `.gdst` 文件，文件名取自第一个条件列的值（规则名）。

## 依赖

- Python 3.x
- openpyxl

```bash
pip install openpyxl
```
