# 数据表结构参考

> 自动从数据地图平台 DESC 获取，最后更新时间：2026-04-29

## 表索引

| # | 表名 | 列数 | 说明 |
|---|------|------|------|
| 1 | [ods_call_record](#ods_call_record) | 26 | 业务系统标识 |
| 2 | [ods_calling_detail](#ods_calling_detail) | 42 | 一组完整的通话的唯一标识 |
| 3 | [ods_cp_datasource_info_df](#ods_cp_datasource_info_df) | 27 | 业务库主键 |
| 4 | [ods_cp_policy_scene_df](#ods_cp_policy_scene_df) | 13 | secret |
| 5 | [ods_cs_complaint_order](#ods_cs_complaint_order) | 26 | 案件id |
| 6 | [ods_cs_ledger_info_df](#ods_cs_ledger_info_df) | 35 | 核销后还款 |
| 7 | [ods_cs_outer_call_info](#ods_cs_outer_call_info) | 29 | 主键 |
| 8 | [ods_gd_admin_guard_orgn_df](#ods_gd_admin_guard_orgn_df) | 9 | 创建时间 |
| 9 | [ods_gd_admin_guard_user_df](#ods_gd_admin_guard_user_df) | 19 | 创建时间 |
| 10 | [ods_gd_case_contact_record_df](#ods_gd_case_contact_record_df) | 25 | id |
| 11 | [ods_gd_case_contract](#ods_gd_case_contract) | 32 | id |
| 12 | [ods_gd_case_detail_df](#ods_gd_case_detail_df) | 51 | id |
| 13 | [ods_gd_case_detail_settlement](#ods_gd_case_detail_settlement) | 47 | id |
| 14 | [ods_loan_contract_record_df](#ods_loan_contract_record_df) | 31 | id, id center生成 |
| 15 | [ods_loan_order_info_df](#ods_loan_order_info_df) | 28 | 主键 |
| 16 | [ods_loan_user_contract_df](#ods_loan_user_contract_df) | 23 | id, id center生成 |
| 17 | [ods_mifi_risk_base_di](#ods_mifi_risk_base_di) | 29 | 消金业务产品ID |
| 18 | [ods_tb_product_account_df](#ods_tb_product_account_df) | 39 | 业务库主键,产品账户id |
| 19 | [ods_user_contract_df](#ods_user_contract_df) | 39 | 业务库主键 |
| 20 | [ods_user_profile_df](#ods_user_profile_df) | 16 | 业务库主键 |
| 21 | [ods_user_repay_detail_df](#ods_user_repay_detail_df) | 19 | 业务库主键 |
| 22 | [policy_db.cp_credit_variable_raw](#policy_dbcp_credit_variable_raw) | 14 | 变量原始记录表（doris队列） |

---

## ods_call_record

**列数**: 26

| 字段 | 类型 | 说明 |
|------|------|------|
| business_label | string | 业务系统标识 |
| business_request_id | string | 业务系统请求id |
| call_reason | string | 呼叫原因 |
| call_type | string | 呼叫类型 |
| create_time | timestamp | create_time |
| department_id | int | 业务部门编码 |
| id | bigint | 话务系统id |
| mobile | string | 客户手机号加密 |
| mobile_md5 | string | 客户手机号md5 |
| outside_record_url | string | 外部录音文件地址 |
| outside_request_id | string | 请求外部id |
| provider | string | 外呼供应商标识 |
| record_nas_url | string | 录音文件nas地址加密 |
| remark | string | 备注 |
| response_content | string | 服务商返回信息加密 |
| seat_no | int | 坐席号 |
| update_time | timestamp | update_time |
| business_label_id | bigint | 业务系统id |
| business_type | string | 首次业务提交时间 |
| call_msg | string | 呼叫msg |
| call_task_id | bigint | 呼叫任务唯一id |
| exist_upload_check | int | 是否进行过质检上传 |
| notify_upstream_time | timestamp | 成功通知上游的时间，未通知为空 |
| product_id | bigint | 产品id |
| user_id | bigint | 消金用户ID |
| dt | int | 分区字段 |

## ods_calling_detail

**列数**: 42

| 字段 | 类型 | 说明 |
|------|------|------|
| callid | string | 一组完整的通话的唯一标识 |
| user_name | string | 已知用户名称 |
| user_nick | string | 客户昵称 |
| user_company_name | string | 所属公司 |
| start_time | string | 呼叫时间 |
| caller | string | 主叫号码 |
| callee | string | 被叫号码 |
| number_provice | string | 号码归属地 |
| call_type | string | 0（呼入），1（呼出）、11（咨询客服），12（咨询第三方），21(转接咨询)、22(转接客服)、23(转接第三方)，3(监听)、4(强插通话)、5(强拆通话) |
| call_flag | string | 0未接听，1已接听 |
| call_way | string | 1网页电话，2sip话机，3手机 |
| group_name | string | 技能组 |
| agentid | string | 坐席 |
| staff_emails | string | 坐席邮箱 |
| final_group_name | string | 最后接待技能组 |
| final_receive_staffids | string | 最后接待坐席 |
| queue_state | string | 1.未排队 2.排队成功 3.排队超时 4.排队离开 |
| queue_duration | string | 排队时长 |
| agent_ring_time | string | 振铃时间 |
| ring_time_duration | string | 单位秒 |
| agent_hungup_time | string | 摘机时间 |
| agent_answer_time | string | 座席通话时长 |
| transfer_count | string | 转接次数 |
| hold_count | string | 保持次数 |
| hold_duration | string | 保持时长 |
| end_time | string | 整个呼叫服务通话结束时间 |
| call_duration | string | 通话总时长 |
| call_result | string | 10.坐席接听 11.振铃未接听 12.ivr放弃 13.排队放弃 14.非服务时间来电... |
| voice_aliyun_url | string | 接通的有值 |
| ender | string | 挂断方 |
| satisfy_value | string | 未评价/非常不满意/不满意/一般/满意/非常满意... |
| satisfy_level | string | 0：未开启满意度，2：二级满意度，3：三级满意度，5：五级满意度，10：自定义满意度 |
| ivrpath | string | IVR轨迹 |
| business_name | string | 服务总结所属业务名称 |
| business_type_name | string | 业务类型 |
| handle_status | string | 处理状态 |
| remarks | string | 备注 |
| fieldname1 | string | 服务总结自定义字段名称1 |
| fieldvalue1 | string | 服务总结自定义字段值1 |
| fieldname2 | string | 服务总结自定义字段名称2 |
| fieldvalue2 | string | 服务总结自定义字段值2 |
| dt | int | 分区字段 |

## ods_cp_datasource_info_df

**列数**: 27

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | 业务库主键 |
| code | int | 数据源code |
| name | string | 数据源名称 |
| type | int | 数据源类型 |
| bean_name | string | 实例名 |
| tp_datasources | string | 三方数据源列表 |
| charge_method | string | 三方计费方式 |
| table_name | string | HBASE表名 |
| column_family | string | HBASE列簇 |
| column_qualifiers | string | HBASE列标识 |
| column_alias | string | 字段别名 |
| row_key_type | int | row_key加密方式 |
| status | int | 状态 |
| wiki | string | wiki地址 |
| remark | string | 备注 |
| create_time | bigint | 创建时间 |
| update_time | bigint | 创建时间 |
| created_by | string | 创建人 |
| updated_by | string | 更新人 |
| interface_path | string | apus调用接口interface |
| last_active_time | bigint | 最近活跃时间 |
| required_vars | string | 必需变量 |
| timeout_millis | int | 超时时长 |
| expire_date | bigint | 缓存天数 |
| fetch_pattern | int | 数据查询模式 |
| charge_status | int | 收费状态:0-不收费, 1-收费 |
| dt | int | 分区日期 |

## ods_cp_policy_scene_df

**列数**: 13

| 字段 | 类型 | 说明 |
|------|------|------|
| api_code | string | secret |
| category | int | 场景分类 |
| code | string | 场景代号 |
| create_by | string | 创建人 |
| create_time | bigint | 创建时间 |
| flow_strategy | string | 场景流量分配 |
| id | bigint | id |
| name | string | 场景名称 |
| organization | string | 所属业务线 |
| status | int | 状态 |
| update_by | string | 更新人 |
| update_time | bigint | 更新时间 |
| dt | int | 分区字段 |

## ods_cs_complaint_order

**列数**: 26

| 字段 | 类型 | 说明 |
|------|------|------|
| case_id | bigint | 案件id |
| client_phone_encrypt | string | 客户手机号 |
| client_phone_hash | string | 顾客手机号hash |
| contact_phone_encrypt | string | 联系电话 |
| contact_phone_hash | string | 联系手机号hash |
| create_time | bigint | 创建时间 |
| first_content | string | 第一次反馈内容 |
| first_level | string | 一级分类 |
| id | bigint | 主键 |
| is_duty | string | 机构是否有责 |
| order_end_time | bigint | 结案时间 |
| order_id | string | 订单号 |
| order_operator | string | 结案操作人 |
| order_source | string | 工单来源 |
| org_id | bigint | 机构id |
| penalty_level | string | 处罚等级 |
| product_id | string | 产品id |
| remark | string | 结案备注 |
| response_time | bigint | 反馈时间 |
| second_content | string | 第二次反馈内容 |
| second_level | string | 二级分类 |
| state | int | 工单状态 |
| update_time | bigint | 更新时间 |
| user_id | bigint | 用户id |
| violation_type | string | 违规类型 |
| dt | int | 分区字段 |

## ods_cs_ledger_info_df

**列数**: 35

| 字段 | 类型 | 说明 |
|------|------|------|
| after_write_offrepayment | bigint | 核销后还款 |
| batch | string | 批次 |
| case_days | int | 立案距还款天数 |
| case_filing_time | bigint | 立案时间 |
| contingency_fee | string | 风险代理费 |
| contingency_fee_ratio | string | 风险代理费比例 |
| create_time | bigint | 创建时间 |
| id | bigint | 主键 |
| law_days | int | 移交律所距还款天数 |
| law_firm | string | 律所 |
| litigation_manage_id | bigint | 诉讼管理表id |
| name_encrypt | string | 加密名字 |
| name_hash | string | 名字hash |
| off_balance_sheet_repayment | bigint | 表外还款 |
| on_balance_sheet_repayment | bigint | 表内还款 |
| product_id | bigint | 产品id |
| reduce_repayment | bigint | 减免还款 |
| remark | string | 备注 |
| repaying_party | string | 还款方 |
| repayment_amount | bigint | 还款金额 |
| repayment_flow | bigint | 还款流水 |
| repayment_time | bigint | 还款时间 |
| state | int | 数据状态  1-存在  2-删除 |
| time_partition | bigint | 时间分区 |
| update_time | bigint | 更新时间 |
| user_id | bigint | 用户id |
| group_id | bigint | 催收系统组织id |
| instance_litigation_fees | string | 诉讼费 |
| trade_mode | bigint | 还款类型 |
| turnover | string | 周转 |
| disposal_method | string | 处置方式 |
| iam_group | string | 法诉二级组织 |
| total_amount | bigint | 总还款额 |
| write_off_time | bigint | 核销时间 |
| dt | int | 分区字段 |

## ods_cs_outer_call_info

**列数**: 29

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | 主键 |
| p_unique_id | string | 通话唯一标识(中台) |
| cs_unique_id | string | 催收测通话唯一标识 |
| case_id | bigint | 案件id |
| user_id | bigint | 用户id |
| relation | int | 关系  1-本人  2-联系人  3-新建联系人 |
| assignee | string | 拨打员工账号 |
| phone_hash | string | hash手机号 |
| phone | string | 加密手机号 |
| skill_group_id | bigint | 催收测技能组id |
| orgn_id | bigint | 催收测机构id |
| age | int | 账龄 |
| ovd_days | int | 逾期天数 |
| create_time | bigint | 创建时间（拨打时间） |
| case_type | int | 拨打案件类型  1-逾期 2-到期提醒 |
| call_type | int | 呼叫方式  0-主动外呼  1预测式外呼 |
| is_call | int | 是否接通 |
| call_start_time | bigint | 呼叫开始时间 |
| call_end_time | bigint | 呼叫结束时间 |
| talk_time | int | 通话时长 |
| display_number | string | 外显号码 |
| display_number_hash | string | 外显号码hash |
| url | string | 录音地址 |
| nas_url | string | nas url |
| recording_track_type | string | 音轨道类型 |
| out_assignee | string | 外部员工唯一标识 |
| unified_social_code | string | bpo机构统一社会信用代码 |
| unified_name | string | bpo机构公司名称 |
| dt | int | 分区字段 |

## ods_gd_admin_guard_orgn_df

**列数**: 9

| 字段 | 类型 | 说明 |
|------|------|------|
| create_time | bigint | 创建时间 |
| created_by | string | 创建人 |
| id | bigint | 机构id |
| orgn_code | string | 机构code |
| orgn_name | string | 机构名称 |
| state | int | 状态 |
| update_time | bigint | 更新时间 |
| updated_by | string | 更新人 |
| dt | int | 按天分区 |

## ods_gd_admin_guard_user_df

**列数**: 19

| 字段 | 类型 | 说明 |
|------|------|------|
| create_time | bigint | 创建时间 |
| created_by | string | 创建人 |
| group_id | bigint | 技能组id |
| id | bigint | 员工id |
| orgn_id | bigint | 机构id |
| part_id | bigint | 部门id |
| roles | string | 角色 |
| state | int | 状态 |
| update_time | bigint | 更新时间 |
| updated_by | string | 更新人 |
| user_account | string | 员工账号 |
| user_name_encryption | string | 员工姓名加密 |
| user_name_hash | string | 员工姓名hash |
| phone_hash | string | hash手机号 |
| phone_mask | string | 脱敏手机号 |
| phone_encrypt | string | 加密手机号 |
| group_roles | string | 组织id+角色id |
| seat_no | int | 坐席工号 |
| dt | int | 按天分区 |

## ods_gd_case_contact_record_df

**列数**: 25

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | id |
| user_id | bigint | 用户 |
| case_id | bigint | 案件ID |
| title | int | 主题类型 |
| contact_type | int | 联络方式 |
| relationship | int | 联系对象 |
| phone_encryption | string | 联系电话 |
| call_result | int | 拨打结果 |
| contact_result | int | 联络结果 |
| consent_time | bigint | 承诺还款时间 |
| remark | string | 备注内容 |
| orgn_id | bigint | 机构id |
| created_by | string | 创建人 |
| create_time | bigint | 创建时间 |
| age | int | 账龄 |
| case_type | int | 案件类型  1-逾期  2-到期提醒 |
| days | int | 逾期天数 |
| next_reach_time | bigint | 下次跟进时间 |
| ovd_amount | bigint | 记录催记时的逾期金额 |
| real_age | int | 合同维度账龄 |
| real_days | int | 合同维度逾期天数 |
| review | int | 审核结果  0-未审核 1-不合格 2-合格 |
| review_operator | string | 审核人 |
| review_time | bigint | 审核时间 |
| dt | int | 日分区 |

## ods_gd_case_contract

**列数**: 32

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | id |
| contract_id | bigint | 合同id |
| fund_mode | int | 出资模式id |
| fund_pattern | string | 资金模式id |
| rule_id | int | rule id |
| data_from | int | 数据来源 |
| product_id | string | 产品id |
| case_id | bigint | 案件id |
| user_id | bigint | 用户id |
| ovd_total | bigint | 逾期总额 |
| ovd_principal | bigint | 逾期本金 |
| ovd_interest | bigint | 逾期利息 |
| ovd_penalty | bigint | 逾期罚息 |
| ovd_other | bigint | 逾期其他费用 |
| repaid_ovd_total | bigint | 全部还款额 |
| repaid_ovd_principal | bigint | 已还本金 |
| repaid_ovd_interest | bigint | 已还利息 |
| repaid_ovd_penalty | bigint | 已还罚息 |
| repaid_ovd_other | bigint | 已还逾期其他费用 |
| balance | bigint | 贷款余额/未还本金 |
| state | int | 状态：1-逾期，2-不逾期 |
| ovd_start_time | bigint | 逾期开始时间 |
| last_repay_time | bigint | 最近还款时间 |
| create_time | bigint | 创建时间 |
| update_time | bigint | 修改时间 |
| real_age | int | 实时账龄 |
| orgn_age | int | 机构账龄 |
| contract_type | string | 合同类型 |
| days | int | 逾期天数 |
| real_days | int | 实时逾期天数 |
| spot_age | int | 即期账龄 |
| dt | int | 分区字段 |

## ods_gd_case_detail_df

**列数**: 51

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | id |
| case_id | bigint | 案件ID |
| user_id | bigint | userId |
| name_encryption | string | 加密姓名 |
| name_hash | string | 姓名hash |
| id_card_encryption | string | 身份证加密 |
| id_card_hash | string | 身份证hash |
| state | int | 状态 1:委外处理中, 2:已完成, 3:撤回未完成, 4:已重分配,5无效 |
| days | int | 委外逾期天数 |
| days_now | int | 当前逾期天数 |
| ovd_total | bigint | 逾期金额 |
| ovd_principal | bigint | 委外时逾期本金 |
| ovd_interest | bigint | 委外时逾期利息 |
| ovd_penalty | bigint | 委外时逾期罚息 |
| ovd_other | bigint | 委外时逾期其他费用 |
| repaid_ovd_principal | bigint | 委外时已还本金 |
| repaid_ovd_interest | bigint | 委外时已还利息 |
| repaid_ovd_penalty | bigint | 委外时已还罚息 |
| repaid_ovd_other | bigint | 委外时已还逾期其他费用 |
| repaid_ovd_total | bigint | 全部还款额 |
| orgn_id | bigint | 归属公司 |
| age | int | 工单账龄 |
| age_now | int | 当前工单账龄 |
| assignee | string | 当前处理人 |
| assignee_name_encryption | string | 催收员加密名字 |
| assignee_name_hash | string | 催收员名字hash |
| assign_time | bigint | 分配时间（页面展示） |
| orgn_assign_time | bigint | 机构分配时间 |
| orgn_assign_time_month | string | 机构分配时间所在月 |
| assign_real_time | bigint | 实际分配时间（计算回款） |
| return_time | bigint | 回收时间 |
| end_time | bigint | 案件结束时间 |
| ovd_start_time | bigint | 逾期开始时间(逾期登记薄start_time) |
| first_ovd_day | int | 首次逾期日 |
| first_ovd_day_month | string | 首次逾期所在月 |
| case_type | int | 1-正常 2-留案 |
| create_time | bigint | 创建时间 |
| update_time | bigint | 修改时间 |
| age_change_time | bigint | 账龄变化日 |
| age_stage | string | 账龄阶段 |
| balance | bigint | 分配余额 |
| is_del | int | 记录状态，1-有效，2-删除 |
| not_user_repaid | bigint | 非用户还款 |
| real_age | int | 合同维度实际账龄 |
| real_age_now | int | 当前实时账龄 |
| real_ovd_days | int | 合同维度最大逾期天数 |
| record_type | int | 类型 1-表示分配记录;2-新增逾期期次记录 |
| repayment_day | int | 还款日 |
| risk_level | int | 风险等级  1-高风险，2-中风险 3-低风险 4-未触碰 |
| repayment_detail | string | 各产品还款明细 |
| dt | int | 按天分区 |

## ods_gd_case_detail_settlement

**列数**: 47

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | id |
| case_id | bigint | 案件ID |
| user_id | bigint | userId |
| name_encryption | string | 加密姓名 |
| name_hash | string | 姓名hash |
| id_card_encryption | string | 身份证加密 |
| id_card_hash | string | 身份证hash |
| state | int | 状态 1:委外处理中, 2:已完成, 3:撤回未完成, 4:已重分配,5无效 |
| days | int | 委外逾期天数 |
| days_now | int | 当前逾期天数 |
| ovd_total | bigint | 逾期金额 |
| ovd_principal | bigint | 委外时逾期本金 |
| ovd_interest | bigint | 委外时逾期利息 |
| ovd_penalty | bigint | 委外时逾期罚息 |
| ovd_other | bigint | 委外时逾期其他费用 |
| repaid_ovd_principal | bigint | 委外时已还本金 |
| repaid_ovd_interest | bigint | 委外时已还利息 |
| repaid_ovd_penalty | bigint | 委外时已还罚息 |
| repaid_ovd_other | bigint | 委外时已还逾期其他费用 |
| repaid_ovd_total | bigint | 全部还款额 |
| orgn_id | bigint | 归属公司 |
| age | int | 工单账龄 |
| age_now | int | 当前工单账龄 |
| assign_time | bigint | 分配时间（页面展示） |
| orgn_assign_time | bigint | 机构分配时间 |
| orgn_assign_time_month | string | 机构分配时间所在月 |
| assign_real_time | bigint | 实际分配时间（计算回款） |
| return_time | bigint | 回收时间 |
| end_time | bigint | 案件结束时间 |
| ovd_start_time | bigint | 逾期开始时间 |
| first_ovd_day | int | 首次逾期日 |
| first_ovd_day_month | string | 首次逾期所在月 |
| case_type | int | 1-正常 2-留案 |
| create_time | bigint | 创建时间 |
| update_time | bigint | 修改时间 |
| risk_level | int | 风险等级  1-高风险，2-中风险 3-低风险 4-未触碰 |
| real_age | int | 合同维度实际账龄 |
| real_ovd_days | int | 合同维度最大逾期天数 |
| is_del | int | 记录状态，1-有效，2-删除 |
| age_stage | string | 账龄阶段 |
| not_user_repaid | bigint | 非用户还款 |
| repayment_day | int | 还款日 |
| real_age_now | int | 当前实时账龄 |
| balance | bigint | 分配余额 |
| age_change_time | bigint | 账龄变化日 |
| repayment_detail | string | 各产品还款明细 |
| dt | int | 分区字段 |

## ods_loan_contract_record_df

**列数**: 31

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | id, id center生成 |
| instruction_id | bigint | 授信流水号 |
| biz_instruction_id | bigint | 业务流水号 |
| user_id | bigint | 用户ID,签署方id |
| template_id | bigint | 合同模板ID |
| template_type | int | 模板类型 |
| template_version | int | 合同模板version |
| status | int | 合同状态：ContractStatusEnum |
| product_id | bigint | 产品ID |
| fund_mode | int | fundMode |
| main_contract_id | bigint | 主合同id |
| trade_code | int | 交易号 |
| serial_number | string | 合同编号 |
| channel | int | 渠道来源 |
| out_id | string | 外部合同id |
| organization | int | 所属机构 |
| view_url | string | 预览地址 |
| ca_location | string | CA机构地址 |
| local_location | string | 本地地址 |
| origin_document_url | string | 原始下载url |
| extension_info | int | 扩展信息，0标识不存在表格，1表示存在表格 |
| create_time | timestamp | 创建时间 |
| update_time | timestamp | 更新时间 |
| sign_time | timestamp | 签署时间 |
| effective_time | timestamp | 生效时间 |
| upload_status | int | 合同上传状态，1-未上传，2-上传完成 |
| note | string | 备注 |
| key_elements | string | 关键要素，json格式, key center加密 |
| ca_location_back_up | string | 机构地址备份 |
| sign_channel | int | sign_channel |
| dt | int | 按天分区 |

## ods_loan_order_info_df

**列数**: 28

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | 主键 |
| create_time | timestamp | 创建时间 |
| update_time | timestamp | 更新时间 |
| product_id | bigint | 产品ID |
| product_version | bigint | 产品版本号 |
| channel | bigint | 渠道来源 |
| instruction_id | bigint | 流水号 |
| user_id | bigint | 用户ID |
| trade_code | bigint | 交易类型(1:支用,2:还款,3:日切,4:授信,5:绑卡) |
| trade_mode | bigint | 交易模式(1:支用,2:还款,3:日切,4:授信,5:绑卡) |
| amount | bigint | 交易金额 |
| trade_status | int | 交易状态(1:交易成功,2:交易失败,3:处理中) |
| expire_status | int | 过期状态(1:未过期,2:已过期) |
| inside_error_code | int | 内部错误码 |
| inside_error_msg | string | 内部错误信息 |
| out_error_code | string | 外部错误码 |
| out_error_msg | string | 外部错误信息 |
| extra_data | string | 扩展信息 |
| external_instruction_id | string | 外部流水号 |
| mi_info_id | bigint | miId注册系统内部映射 |
| out_info_id | bigint | outId注册系统内部映射 |
| main_product_id | bigint | 主产品ID |
| finish_time | timestamp | 订单完成时间 |
| biz_time | bigint | 业务时间 |
| biz_instruction_id | bigint | 业务流水号 |
| owner_code | bigint | 归属方 |
| fund_id | bigint | 出资模式 |
| dt | int | 分区日期 |

## ods_loan_user_contract_df

**列数**: 23

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | id, id center生成 |
| instruction_id | bigint | 授信流水号 |
| template_id | bigint | 合同模板ID |
| product_id | bigint | 产品ID |
| trade_code | int | 交易号 |
| channel | int | 渠道来源 |
| out_id | string | 外部合同id |
| key_elements | string | 关键要素，json格式, key center加密 |
| user_status | int | 合同用户状态：0待生效、1已生效、2已取消、3已变更 |
| status | int | 合同状态：1正常、2结清、3逾期，4无效 |
| user_id | bigint | 用户ID,签署方id |
| organization | int | 所属机构，具体成员参看枚举类 |
| ca_location | string | CA机构地址 |
| local_location | string | 本地地址 |
| create_time | timestamp | 创建时间 |
| update_time | timestamp | 更新时间 |
| sign_time | timestamp | 签署时间 |
| effective_time | timestamp | 生效时间 |
| note | string | 备注 |
| file_source_info | string | 合同协议文件信息 |
| serial_number | string | 合同编号 |
| view_url | string | 预览地址 |
| dt | int | 按天分区 |

## ods_mifi_risk_base_di

**列数**: 29

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint |  |
| user_id | bigint |  |
| instruction_id | bigint |  |
| id_num | string |  |
| mobile | string |  |
| device_id | string |  |
| tp_id | int |  |
| product_id | int |  |
| source_id | int |  |
| biz_id | int |  |
| bizteam_id | int |  |
| techteam_id | int |  |
| section_id | int |  |
| strategy_id | int |  |
| model_id | int |  |
| request_param | string |  |
| response | string |  |
| pattern | int |  |
| fetch_from | int |  |
| is_validresult | int |  |
| is_hitcache | int |  |
| status | int |  |
| latency | bigint |  |
| source_time | bigint |  |
| log_time | bigint |  |
| is_fee | int |  |
| business_product_id | bigint | 消金业务产品ID |
| nested_strategy_id | int | 子场景id |
| dt | int | 日分区 |

## ods_tb_product_account_df

**列数**: 39

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | 业务库主键,产品账户id |
| user_id | bigint | 用户ID |
| status | string | 状态 |
| create_time | timestamp | 创建时间 |
| update_time | timestamp | 更新时间 |
| note | string | 备注 |
| sub_business_account_id | bigint | 子业务账户id |
| instruction_id | bigint | 开户流水号 |
| product_id | bigint | 产品id |
| cycle_account | int | 是否循环账户 |
| rate | int | 利率 |
| rate_type | int | 利率类型 |
| credit_amount | int | 授信额度 |
| start_time | timestamp | 开始时间 |
| end_time | timestamp | 到期时间 |
| invalid_time | timestamp | 作废时间 |
| frozen_amount | int | 冻结额度 |
| lock_amount | int | 锁定额度 |
| temp_amount | int | 临时额度 |
| diff_amount | int | 调整额度 |
| available_amount | int | 可用额度 |
| used_amount | int | 已用额度 |
| repay_method | int | 还款方式列表 |
| max_term | int | 最高期数 |
| repay_day | int | 还款日 |
| product_strategy_id | bigint | 产品策略对应的id |
| principal_penalty_rate | int | 本罚利率 |
| interest_penalty_rate | int | 利罚利率 |
| account_identifier | bigint | 账户识别码 |
| contract_code | string | 授信协议的编号 |
| version | int | 版本号 |
| pre_repay_amount | int | 预还款额度 |
| product_account_type | string | 预还款额度 |
| owner_code | bigint | 账户归属方 |
| biz_instruction_id | bigint | 业务流水号 |
| credit_ban_end_date | timestamp | 授信封禁期结束时间 |
| pay_ban_end_date | timestamp | 支用封禁期结束时间 |
| lock_status | string | locked：已锁定，unlock：未锁定 |
| dt | int | 日分区 |

## ods_user_contract_df

**列数**: 39

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | 业务库主键 |
| contract_id | bigint | 借据号 |
| user_id | bigint | 用户ID |
| product_id | bigint | 产品id |
| product_version | int | 产品版本 |
| channel | int | 渠道号 |
| graceful_days | int | 宽限天数 |
| term_num | int | 期数 |
| fund_mode | int | 资金模式 |
| principal | bigint | 本金 |
| rate | bigint | 利率 |
| fee_rate | bigint | 费率 |
| overdue_principal_rate | bigint | 本罚利率 |
| overdue_interest_rate | bigint | 利罚利率 |
| repayment_mode | int | 还款方式 |
| start_date | bigint | 起始日 |
| end_date | bigint | 结束日 |
| unpaid_principal | bigint | 未还本金 |
| value_date | bigint | 起息日 |
| accounting_date | bigint | 当前会计时间 |
| principal_base_amount | bigint | 本金基数 |
| overdue_principal_base_amount | bigint | 逾期本金基数 |
| overdue_interest_base_amount | bigint | 逾期利息基数 |
| settlement_time | bigint | 结清时间 |
| contract_status | int | 合同状态 |
| accrue_interest_status | int | 计息状态 |
| write_off | int | 核销状态 |
| accrual | int | 应计非应计状态 |
| account_channel | int | 记账方式 |
| account_time | bigint | 账务时间 |
| create_time | bigint | 创建时间 |
| update_time | bigint | 更新时间 |
| limit_line | bigint | 封顶线 |
| paid_charge | bigint | 当前已还费用 |
| is_subsidy | int | 是否贴息 |
| account_id | bigint | 账户id |
| account_identifier | bigint | 账号识别码 |
| repay_day | int | 固定还款日 |
| dt | int | 日分区 |

## ods_user_profile_df

**列数**: 16

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | 业务库主键 |
| name | string | 姓名[加密] |
| name_token | string | 姓名md5 |
| id_card_type | int | 证件类型: 0-未知类型,1-身份证 |
| id_card_no | string | 证件号码[加密] |
| id_card_no_token | string | 证件号码token |
| mobile | string | 手机号[加密] |
| mobile_token | string | 手机token |
| remark | string | 备注 |
| old_create_time | bigint | 创建时间 |
| old_update_time | bigint | 更新时间 |
| create_time_1 | timestamp | 创建时间 |
| update_time_1 | timestamp | 更新时间 |
| create_time | timestamp | 创建时间 |
| update_time | timestamp | 更新时间 |
| dt | int | 日分区 |

## ods_user_repay_detail_df

**列数**: 19

| 字段 | 类型 | 说明 |
|------|------|------|
| id | bigint | 业务库主键 |
| instruction_id | bigint | 流水号 |
| user_id | bigint | 用户id |
| product_id | bigint | 产品id |
| trade_code | int | 交易代码 |
| trade_mode | int | 交易模式 |
| contract_id | bigint | 借据号 |
| term_no | int | 期次号 |
| term_id | bigint | 期次id |
| amount | bigint | 还款金额 |
| repay_amount_type | int | 还款金额类型 |
| write_off | int | 核销状态 |
| accrual | int | 应计状态 |
| account_time | bigint | 账务时间 |
| create_time | bigint | 创建时间 |
| account_id | bigint | 账户id |
| account_identifier | bigint | 账户识别号 |
| update_time | timestamp | 更新时间 |
| dt | int | 日分区 |

---

## policy_db.cp_credit_variable_raw

**数据源**: doris队列（非spark_tbds）
**分区**: 无dt分区（Doris表）
**说明**: key-value格式，field_name存变量名，value存变量值

**列数**: 14

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
