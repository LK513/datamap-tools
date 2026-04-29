# 数据表结构缓存

> 团队共享文件。使用 `/datamap-sql` 查数后，新表结构请补充到此文件。
> 位置：`.claude/docs/table-schemas.md`（项目根目录下）

## policy_db.cp_credit_variable_raw

- **数据源**: doris队列
- **分区**: 无dt分区（Doris表）
- **结构**: key-value格式，field_name存变量名，value存变量值

| 字段 | 类型 | 说明 |
|------|------|------|
| dt | BIGINT | 日期，格式20260429 |
| instruction | BIGINT | 指令ID |
| xiaomi_id | BIGINT | 用户ID |
| mode | BIGINT | 模式 |
| scene_code | VARCHAR(64) | 场景编码 |
| field_name | VARCHAR(128) | 变量名（如MXJ_result） |
| create_time | BIGINT | 创建时间 |
| process_id | BIGINT | 流程ID |
| value | VARCHAR(20000) | 变量值 |
| update_time | BIGINT | 更新时间 |
| value_status | - | 值状态 |
| group_id | - | 分组ID |
| sys_proc_time | - | 系统处理时间 |
| product_id | - | 产品ID（102、115等） |
| pkg_id | - | 包ID |

**已知field_name取值**:
- `MXJ_result`: 授信结果，1=通过，2=拒绝，-1=未处理，7=其他

---

## cfc.ods_gd_case_base_df

- **数据源**: 消金数仓(hive)
- **分区**: dt（必须加 `WHERE dt = '${date-1}'`）
- **行数**: 约53列

主要字段（前10列）:

| 字段 | 类型 | 说明 |
|------|------|------|
| dt | STRING | 分区字段，日期 |
| ... | ... | 共53个字段 |

---

## 常用表快速参考

| 表名 | 数据源 | 分区 | 说明 |
|------|--------|------|------|
| `policy_db.cp_credit_variable_raw` | doris | 无 | 策略执行表，key-value结构 |
| `cfc.ods_gd_case_base_df` | hive | dt | 案件基础表 |
| `dws_sxj_amount_adjust_instruction` | hive | dt | 调额指令表 |
| `ods_mifi_risk_base_di` | hive | dt | 风控基础数据日表 |
| `dwd_loan_xj_contract_fact_df` | hive | dt | 现金贷合同事实表 |
| `dwd_loan_user_contract_fact_df` | hive | dt | 用户合同事实表 |
| `ods_loan_order_info_df` | hive | dt | 订单信息表 |
