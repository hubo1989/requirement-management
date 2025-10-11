# Transaction Day 日统计表结构文档

## 表基本信息

- **表名**: transaction_day
- **表描述**: 交易日统计表，基于transaction_main明细数据按日汇总的统计数据
- **字段总数**: 43个字段
- **创建时间**: 2024年
- **数据来源**: 从transaction_main表按日清洗汇总生成，以doris数据库形式提供查询
- **更新频率**: 每日凌晨更新前一日数据

## 表结构详细信息

| 序号 | 字段名称                 | 数据类型      | 约束条件                                              | 字段描述                              |
| ---- | ------------------------ | ------------- | ----------------------------------------------------- | ------------------------------------- |
| 1    | id                       | bigint        | PRIMARY KEY, AUTO_INCREMENT                           | 主键ID                                |
| 2    | stat_date                | date          | NOT NULL                                              | 统计日期                              |
| 3    | bank_code                | string        |                                                       | 银行代码                              |
| 4    | bank_name                | string        |                                                       | 银行名称                              |
| 5    | trans_channel            | string        |                                                       | 交易渠道（all/online/offline/mobile） |
| 6    | total_trans_count        | bigint        | DEFAULT 0                                             | 总交易笔数                            |
| 7    | total_trans_amount       | decimal(20,3) | DEFAULT 0                                             | 总交易金额（分）                      |
| 8    | success_trans_count      | bigint        | DEFAULT 0                                             | 成功交易笔数                          |
| 9    | success_trans_amount     | decimal(20,3) | DEFAULT 0                                             | 成功交易金额（分）                    |
| 10   | failed_trans_count       | bigint        | DEFAULT 0                                             | 失败交易笔数                          |
| 11   | failed_trans_amount      | decimal(20,3) | DEFAULT 0                                             | 失败交易金额（分）                    |
| 12   | qualified_trans_count    | bigint        | DEFAULT 0                                             | 达标交易笔数                          |
| 13   | qualified_trans_amount   | decimal(20,3) | DEFAULT 0                                             | 达标交易金额（分）                    |
| 14   | qualified_merchant_count | bigint        | DEFAULT 0                                             | 达标商户数                            |
| 15   | avg_trans_amount         | decimal(14,3) | DEFAULT 0                                             | 平均交易金额（分）                    |
| 16   | max_trans_amount         | decimal(20,3) | DEFAULT 0                                             | 最大交易金额（分）                    |
| 17   | min_trans_amount         | decimal(20,3) | DEFAULT 0                                             | 最小交易金额（分）                    |
| 18   | total_fee_amount         | decimal(14,3) | DEFAULT 0                                             | 总手续费金额（分）                    |
| 19   | debit_card_count         | bigint        | DEFAULT 0                                             | 借记卡交易笔数                        |
| 20   | credit_card_count        | bigint        | DEFAULT 0                                             | 贷记卡交易笔数                        |
| 21   | debit_card_amount        | decimal(20,3) | DEFAULT 0                                             | 借记卡交易金额（分）                  |
| 22   | credit_card_amount       | decimal(20,3) | DEFAULT 0                                             | 贷记卡交易金额（分）                  |
| 23   | unique_merchant_count    | bigint        | DEFAULT 0                                             | 活跃商户数                            |
| 24   | total_merchant_count     | bigint        | DEFAULT 0                                             | 交易商户数                            |
| 25   | created_time             | timestamp     | DEFAULT CURRENT_TIMESTAMP                             | 创建时间                              |
| 26   | updated_time             | timestamp     | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP | 更新时间                              |
| 27   | consume_trans_count      | bigint        | DEFAULT 0                                             | 消费交易笔数                          |
| 28   | consume_trans_amount     | decimal(20,3) | DEFAULT 0                                             | 消费交易金额（分）                    |
| 29   | refund_trans_count       | bigint        | DEFAULT 0                                             | 退款交易笔数                          |
| 30   | refund_trans_amount      | decimal(20,3) | DEFAULT 0                                             | 退款交易金额（分）                    |
| 31   | preauth_complete_count   | bigint        | DEFAULT 0                                             | 预授权完成撤销交易笔数                |
| 32   | preauth_complete_amount  | decimal(20,3) | DEFAULT 0                                             | 预授权完成撤销交易金额（分）          |
| 33   | wechat_pay_count         | bigint        | DEFAULT 0                                             | 微信支付笔数                          |
| 34   | wechat_pay_amount        | decimal(20,3) | DEFAULT 0                                             | 微信支付金额（分）                    |
| 35   | alipay_count             | bigint        | DEFAULT 0                                             | 支付宝支付笔数                        |
| 36   | alipay_amount            | decimal(20,3) | DEFAULT 0                                             | 支付宝支付金额（分）                  |
| 37   | bank_card_count          | bigint        | DEFAULT 0                                             | 银行卡刷卡笔数                        |
| 38   | bank_card_amount         | decimal(20,3) | DEFAULT 0                                             | 银行卡刷卡金额（分）                  |
| 39   | preauth_finish_count     | bigint        | DEFAULT 0                                             | 预授权完成笔数                        |
| 40   | preauth_finish_amount    | decimal(20,3) | DEFAULT 0                                             | 预授权完成金额（分）                  |
| 41   | icbc_count               | bigint        | DEFAULT 0                                             | 工商银行交易笔数                      |
| 42   | icbc_amount              | decimal(20,3) | DEFAULT 0                                             | 工商银行交易金额（分）                |
| 43   | abc_count                | bigint        | DEFAULT 0                                             | 农业银行交易笔数                      |
| 44   | abc_amount               | decimal(20,3) | DEFAULT 0                                             | 农业银行交易金额（分）                |

## 字段分类说明

### 1. 基础标识字段 (1-5)

主键、统计日期、银行信息和交易渠道等基础标识字段。

### 2. 交易总量统计字段 (6-11)

记录总交易笔数、金额以及成功/失败交易的统计数据。

### 3. 达标业务统计字段 (12-14)

记录达标交易笔数、金额和达标商户数等业务关键指标。

### 4. 交易金额分析字段 (15-17)

记录平均、最大、最小交易金额，用于交易金额分布分析。

### 5. 费用统计字段 (18)

记录总手续费金额，用于收益分析。

### 6. 卡类型统计字段 (19-22)

按借记卡和贷记卡分别统计交易笔数和金额。

### 7. 商户活跃度字段 (23-24)

记录活跃商户数和交易商户数，用于商户活跃度分析。

### 8. 系统管理字段 (25-26)

记录数据创建和更新时间。

### 9. 交易方向统计字段 (27-32)

按交易方向分类统计交易笔数和金额：
- 消费交易统计
- 退款交易统计
- 预授权完成撤销交易统计

### 10. 钱包类型统计字段 (33-40)

按钱包类型分类统计交易笔数和金额：
- 微信支付统计
- 支付宝支付统计
- 银行卡刷卡统计
- 预授权完成统计

### 11. 银行卡细分统计字段 (41-44)

按发卡银行分类统计交易笔数和金额：
- 工商银行统计
- 农业银行统计

## 数据约束说明

### 主键约束

- `id` 字段作为主键，自增长，确保每条记录的唯一性

### 唯一性约束

```sql
-- 统计日期+银行代码+交易渠道的组合唯一
CREATE UNIQUE INDEX uk_stat_date_bank_channel ON transaction_day(stat_date, bank_code, trans_channel);
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
- 所有金额和计数字段不能为负数

## 索引建议

### 主要查询索引

```sql
-- 统计日期索引
CREATE INDEX idx_stat_date ON transaction_day(stat_date);

-- 银行代码索引
CREATE INDEX idx_bank_code ON transaction_day(bank_code);

-- 交易渠道索引
CREATE INDEX idx_trans_channel ON transaction_day(trans_channel);

-- 组合索引：日期+银行
CREATE INDEX idx_date_bank ON transaction_day(stat_date, bank_code);

-- 组合索引：日期+渠道
CREATE INDEX idx_date_channel ON transaction_day(stat_date, trans_channel);
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
   - 按交易渠道（trans_channel）分组
2. **汇总计算**：

   ```sql
   -- 示例汇总SQL
   INSERT INTO transaction_day (
       stat_date, bank_code, bank_name, trans_channel,
       total_trans_count, total_trans_amount,
       success_trans_count, success_trans_amount,
       failed_trans_count, failed_trans_amount,
       qualified_trans_count, qualified_trans_amount,
       qualified_merchant_count, avg_trans_amount,
       max_trans_amount, min_trans_amount,
       total_fee_amount, debit_card_count, credit_card_count,
       debit_card_amount, credit_card_amount, unique_merchant_count
   )
   SELECT 
       trans_date as stat_date,
       bank_code,
       MAX(card_bank) as bank_name,
       trans_channel,
       COUNT(*) as total_trans_count,
       SUM(trans_amt) as total_trans_amount,
       SUM(CASE WHEN trans_status = 'SUCCESS' THEN 1 ELSE 0 END) as success_trans_count,
       SUM(CASE WHEN trans_status = 'SUCCESS' THEN trans_amt ELSE 0 END) as success_trans_amount,
       SUM(CASE WHEN trans_status != 'SUCCESS' THEN 1 ELSE 0 END) as failed_trans_count,
       SUM(CASE WHEN trans_status != 'SUCCESS' THEN trans_amt ELSE 0 END) as failed_trans_amount,
       -- 达标交易逻辑（根据业务规则定义）
       SUM(CASE WHEN trans_amt >= 100000 THEN 1 ELSE 0 END) as qualified_trans_count,
       SUM(CASE WHEN trans_amt >= 100000 THEN trans_amt ELSE 0 END) as qualified_trans_amount,
       COUNT(DISTINCT CASE WHEN trans_amt >= 100000 THEN merchant_id END) as qualified_merchant_count,
       AVG(trans_amt) as avg_trans_amount,
       MAX(trans_amt) as max_trans_amount,
       MIN(trans_amt) as min_trans_amount,
       SUM(fee_amt) as total_fee_amount,
       SUM(CASE WHEN card_type = 'DEBIT' THEN 1 ELSE 0 END) as debit_card_count,
       SUM(CASE WHEN card_type = 'CREDIT' THEN 1 ELSE 0 END) as credit_card_count,
       SUM(CASE WHEN card_type = 'DEBIT' THEN trans_amt ELSE 0 END) as debit_card_amount,
       SUM(CASE WHEN card_type = 'CREDIT' THEN trans_amt ELSE 0 END) as credit_card_amount,
       COUNT(DISTINCT merchant_id) as unique_merchant_count
   FROM transaction_main 
   WHERE trans_date = '2024-01-15'  -- 指定统计日期
   GROUP BY trans_date, bank_code, trans_channel;
   ```

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

1. **访问控制**：建立严格的数据访问权限控制
2. **审计日志**：记录所有数据访问和修改操作
3. **数据备份**：定期备份统计数据
4. **脱敏处理**：对外提供数据时进行适当脱敏

### 数据保留策略

1. **热数据**：近1年数据保持在主表，支持快速查询
2. **温数据**：1-3年数据迁移到历史表
3. **冷数据**：超过3年的数据归档到冷存储
4. **法规要求**：按照金融监管要求保留必要的历史数据

## 使用说明

### 常用查询示例

```sql
-- 查询指定日期所有银行的交易统计
SELECT * FROM transaction_day 
WHERE stat_date = '2024-01-15' 
AND trans_channel = 'all'
ORDER BY total_trans_amount DESC;

-- 查询指定银行近30天的交易趋势
SELECT stat_date, total_trans_count, total_trans_amount
FROM transaction_day 
WHERE bank_code = 'ICBC' 
AND trans_channel = 'all'
AND stat_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY)
ORDER BY stat_date;

-- 查询指定时间范围内的银行交易汇总
SELECT 
    bank_name,
    SUM(total_trans_count) as total_count,
    SUM(total_trans_amount) as total_amount,
    SUM(qualified_trans_count) as qualified_count,
    SUM(qualified_merchant_count) as qualified_merchants
FROM transaction_day 
WHERE stat_date BETWEEN '2024-01-01' AND '2024-01-31'
AND trans_channel = 'all'
GROUP BY bank_code, bank_name
ORDER BY total_amount DESC;

-- 查询交易成功率统计
SELECT 
    bank_name,
    stat_date,
    total_trans_count,
    success_trans_count,
    ROUND(success_trans_count * 100.0 / total_trans_count, 2) as success_rate
FROM transaction_day 
WHERE stat_date >= DATE_SUB(CURDATE(), INTERVAL 7 DAY)
AND trans_channel = 'all'
ORDER BY stat_date DESC, success_rate DESC;
```

### API数据格式示例

```json
{
  "date": "2024-01-15",
  "bankCode": "ICBC",
  "bankName": "工商银行",
  "transactionChannel": "all",
  "totalTransactions": 12450,
  "totalAmount": 356780000,
  "successTransactions": 12380,
  "successAmount": 355120000,
  "qualifiedTransactions": 8900,
  "qualifiedAmount": 298560000,
  "qualifiedMerchants": 1250,
  "avgTransactionAmount": 28650,
  "activeMerchants": 2100,
  "successRate": 99.44
}
```

### 注意事项

1. 查询大量历史数据时建议使用分页查询
2. 金额计算时注意单位转换（分转元）
3. 时间范围查询时注意使用索引优化性能
4. 统计数据查询建议使用缓存提高响应速度
5. 跨月查询时注意数据分区策略
