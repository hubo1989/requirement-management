# Transaction Day 日统计表结构文档

## 表基本信息

- **表名**: transaction_day
- **表描述**: 交易日统计表，基于transaction_main明细数据按日汇总的统计数据
- **字段总数**: 41个字段
- **数据来源**: 从交易流水表按日清洗汇总生成，以doris数据库形式提供查询
- **更新频率**: 每日凌晨更新前一日数据

## 表结构详细信息


| 序号 | 字段名称                 | 数据类型      | 约束条件                                              | 字段描述                                          |
| ---- | ------------------------ | ------------- | ----------------------------------------------------- | ------------------------------------------------- |
| 1    | id                       | bigint        | PRIMARY KEY, AUTO_INCREMENT                           | 主键ID                                            |
| 2    | stat_date                | date          | NOT NULL                                              | 统计日期                                          |
| 3    | bank_code                | string        |                                                       | 银行代码                                          |
| 4    | bank_name                | string        |                                                       | 银行名称                                          |
| 5    | mcc_code                 | string        |                                                       | 商户mcc                                           |
| 6    | merchant_type            | string        |                                                       | 商户类型（实体商户/资金商户），与原数据组逻辑一致 |
| 7    | trans_channel            | string        |                                                       | 交易渠道（all/online/offline/mobile）             |
| 8    | total_trans_count        | bigint        | DEFAULT 0                                             | 总交易笔数                                        |
| 9    | total_trans_amount       | decimal(20,3) | DEFAULT 0                                             | 总交易金额（分）                                  |
| 10   | success_trans_count      | bigint        | DEFAULT 0                                             | 成功交易笔数                                      |
| 11   | success_trans_amount     | decimal(20,3) | DEFAULT 0                                             | 成功交易金额（分）                                |
| 12   | failed_trans_count       | bigint        | DEFAULT 0                                             | 失败交易笔数                                      |
| 13   | failed_trans_amount      | decimal(20,3) | DEFAULT 0                                             | 失败交易金额（分）                                |
| 14   | qualified_trans_count    | bigint        | DEFAULT 0                                             | 达标交易笔数                                      |
| 15   | qualified_trans_amount   | decimal(20,3) | DEFAULT 0                                             | 达标交易金额（分）                                |
| 16   | qualified_merchant_count | bigint        | DEFAULT 0                                             | 达标商户数                                        |
| 17   | avg_trans_amount         | decimal(14,3) | DEFAULT 0                                             | 平均交易金额（分）                                |
| 18   | max_trans_amount         | decimal(20,3) | DEFAULT 0                                             | 最大交易金额（分）                                |
| 19   | min_trans_amount         | decimal(20,3) | DEFAULT 0                                             | 最小交易金额（分）                                |
| 20   | total_fee_amount         | decimal(14,3) | DEFAULT 0                                             | 总手续费金额（分）                                |
| 21   | debit_card_count         | bigint        | DEFAULT 0                                             | 借记卡交易笔数                                    |
| 22   | credit_card_count        | bigint        | DEFAULT 0                                             | 贷记卡交易笔数                                    |
| 23   | debit_card_amount        | decimal(20,3) | DEFAULT 0                                             | 借记卡交易金额（分）                              |
| 24   | credit_card_amount       | decimal(20,3) | DEFAULT 0                                             | 贷记卡交易金额（分）                              |
| 25   | unique_merchant_count    | bigint        | DEFAULT 0                                             | 活跃商户数                                        |
| 26   | total_merchant_count     | bigint        | DEFAULT 0                                             | 交易商户数                                        |
| 27   | created_time             | timestamp     | DEFAULT CURRENT_TIMESTAMP                             | 创建时间                                          |
| 28   | updated_time             | timestamp     | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP | 更新时间                                          |
| 29   | consume_trans_count      | bigint        | DEFAULT 0                                             | 消费交易笔数                                      |
| 30   | consume_trans_amount     | decimal(20,3) | DEFAULT 0                                             | 消费交易金额（分）                                |
| 31   | refund_trans_count       | bigint        | DEFAULT 0                                             | 退款交易笔数                                      |
| 32   | refund_trans_amount      | decimal(20,3) | DEFAULT 0                                             | 退款交易金额（分）                                |
| 33   | preauth_complete_count   | bigint        | DEFAULT 0                                             | 预授权完成撤销交易笔数                            |
| 34   | preauth_complete_amount  | decimal(20,3) | DEFAULT 0                                             | 预授权完成撤销交易金额（分）                      |
| 35   | wechat_pay_count         | bigint        | DEFAULT 0                                             | 微信支付笔数                                      |
| 36   | wechat_pay_amount        | decimal(20,3) | DEFAULT 0                                             | 微信支付金额（分）                                |
| 37   | alipay_count             | bigint        | DEFAULT 0                                             | 支付宝支付笔数                                    |
| 38   | alipay_amount            | decimal(20,3) | DEFAULT 0                                             | 支付宝支付金额（分）                              |
| 39   | bank_card_count          | bigint        | DEFAULT 0                                             | 银行卡刷卡笔数                                    |
| 40   | bank_card_amount         | decimal(20,3) | DEFAULT 0                                             | 银行卡刷卡金额（分）                              |
| 41   | preauth_finish_count     | bigint        | DEFAULT 0                                             | 预授权完成笔数                                    |

## 字段分类说明

### 1. 基础标识字段 (1-7)

主键、统计日期、银行信息、商户类别（mcc）和商户类型等基础标识字段。商户类型字段，与原数据组区分逻辑一致：实体商户为分公司和渠道的真商机构。资金商户为机构大类限制营销中心、全网自营，机构小类为：

- 渠道部-s
- ﻿渠道部-好拓客
- 渠道部-直拓客
- 客户满意部
- ﻿渠道部-代理

### 2. 交易总量统计字段 (8-13)

记录总交易笔数、金额以及成功/失败交易的统计数据。

### 3. 达标业务统计字段 (14-16)

记录达标交易笔数、金额和达标商户数等业务关键指标。

### 4. 交易金额分析字段 (17-19)

记录平均、最大、最小交易金额，用于交易金额分布分析。

### 5. 费用统计字段 (20)

记录总手续费金额，用于收益分析。

### 6. 卡类型统计字段 (21-24)

按借记卡和贷记卡分别统计交易笔数和金额。

### 7. 商户活跃度字段 (25-26)

记录活跃商户数和交易商户数，用于商户活跃度分析。活跃商户定义：日正向交易-逆向交易大于等于1000以上。

### 8. 系统管理字段 (27-28)

记录数据创建和更新时间。

### 9. 交易方向统计字段 (29-34)

按交易方向分类统计交易笔数和金额：

- 消费交易统计
- 退款交易统计
- 预授权完成撤销交易统计

### 10. 钱包类型统计字段 (35-41)

按钱包类型分类统计交易笔数和金额：

- 微信支付统计
- 支付宝支付统计
- 银行卡刷卡统计
- 预授权完成统计

## 数据约束说明

### 主键约束

- `id` 字段作为主键，自增长，确保每条记录的唯一性

### 唯一性约束

```sql
-- 统计日期+银行代码+商户mcc的组合唯一
CREATE UNIQUE INDEX uk_stat_date_bank_mcc ON transaction_day(stat_date, bank_code,);
```

### 数据类型约束

- **date类型**: 统计日期，格式为YYYY-MM-DD
- **string类型**: 用于存储银行代码、银行名称、交易渠道等文本信息
- **bigint类型**: 用于存储交易笔数、商户数等计数数据
- **decimal类型**: 用于存储精确的金额数据，避免浮点数精度问题
- **timestamp类型**: 用于记录数据创建和更新时间

### 业务约束

- 金额字段使用分为单位存储，避免小数点精度问题
- 统计日期不能为未来日期
- 交易渠道字段限制为：'all', 'online', 'offline', 'mobile'
- 商户类型字段限制为：'实体商户', '资金商户'
- 所有金额和计数字段不能为负数

## 索引建议

### 主要查询索引

```sql
-- 统计日期索引
CREATE INDEX idx_stat_date ON transaction_day(stat_date);

-- 银行代码索引
CREATE INDEX idx_bank_code ON transaction_day(bank_code);

-- 商户mcc索引
CREATE INDEX idx_mcc_code ON transaction_day(mcc_code);

-- 商户类型索引
CREATE INDEX idx_merchant_type ON transaction_day(merchant_type);

-- 组合索引：日期+银行
CREATE INDEX idx_date_bank ON transaction_day(stat_date, bank_code);

-- 组合索引：日期+商户mcc
CREATE INDEX idx_date_mcc ON transaction_day(stat_date, mcc_code);

-- 组合索引：日期+商户类型
CREATE INDEX idx_date_merchant_type ON transaction_day(stat_date, merchant_type);

-- 组合索引：银行代码+商户mcc
CREATE INDEX idx_bank_mcc ON transaction_day(bank_code, mcc_code);

-- 组合索引：银行代码+商户类型
CREATE INDEX idx_bank_merchant_type ON transaction_day(bank_code, merchant_type);
```

### 性能优化索引

```sql
-- 时间范围查询索引
CREATE INDEX idx_stat_date_range ON transaction_day(stat_date DESC);

-- 银行名称索引（用于模糊查询）
CREATE INDEX idx_bank_name ON transaction_day(bank_name);
```

## 数据生成规则

### 数据清洗逻辑

基于transaction_main表按以下维度进行日汇总：

1. **统计维度**：

   - 按统计日期（trans_date）分组
   - 按银行代码（bank_code）分组
   - 按商户mcc（mcc_code）分组
   - 按商户类型（merchant_type）分组

### 数据更新策略

1. **增量更新**：每日凌晨2点执行前一日数据汇总
2. **全量重算**：每月1号重新计算上月所有数据，确保数据准确性
3. **实时监控**：监控数据生成过程，异常时及时告警

## 数据治理说明

### 数据质量要求

1. **完整性**：每日必须生成所有活跃银行的统计数据
2. **一致性**：汇总数据与明细数据保持一致
3. **准确性**：金额计算精确到分，避免精度丢失
4. **时效性**：统计数据在次日上午8点前完成更新

### 数据安全要求

1. **审计日志**：记录所有数据访问和修改操作
2. **数据备份**：定期备份统计数据
