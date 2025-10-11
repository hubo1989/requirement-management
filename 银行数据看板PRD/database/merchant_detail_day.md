# Merchant Detail 日统计表结构文档

## 表基本信息

- **表名**: merchant_detail_day
- **表描述**: 商户明细日统计表，基于transaction_main明细数据按日汇总的商户维度统计数据
- **字段总数**: 20个字段
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
| 5    | mcc_code                 | string        |                                                       | 商户行业类型代码(MCC)                 |
| 6    | mcc_name                 | string        |                                                       | 商户行业类型名称                      |
| 7    | province_code            | string        |                                                       | 商户所在省份代码                      |
| 8    | province_name            | string        |                                                       | 商户所在省份名称                      |
| 9    | branch_code              | string        |                                                       | 商户所属分公司代码                    |
| 10   | branch_name              | string        |                                                       | 商户所属分公司名称                    |
| 11   | agent_code               | string        |                                                       | 代理商代码(三代机构号)                |
| 12   | agent_name               | string        |                                                       | 代理商名称                            |
| 13   | merchant_count           | bigint        | DEFAULT 0                                             | 商户数量                              |
| 14   | trans_count              | bigint        | DEFAULT 0                                             | 交易笔数                              |
| 15   | trans_amount             | decimal(20,3) | DEFAULT 0                                             | 交易金额（分）                        |
| 16   | qualified_merchant_count | bigint        | DEFAULT 0                                             | 达标商户数                            |
| 17   | qualified_trans_count    | bigint        | DEFAULT 0                                             | 达标交易笔数                          |
| 18   | qualified_trans_amount   | decimal(20,3) | DEFAULT 0                                             | 达标交易金额（分）                    |
| 19   | created_time             | timestamp     | DEFAULT CURRENT_TIMESTAMP                             | 创建时间                              |
| 20   | updated_time             | timestamp     | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP | 更新时间                              |

## 字段分类说明

### 1. 基础标识字段 (1-4)

主键、统计日期、银行信息等基础标识字段。

### 2. 商户分类字段 (5-12)

商户分类信息：
- 商户行业类型(MCC)
- 商户地区信息
- 商户所属分公司
- 代理商信息

### 3. 商户统计字段 (13-18)

商户数量和交易统计：
- 商户数量
- 交易笔数和金额
- 达标商户数和交易统计

### 4. 系统管理字段 (19-20)

记录数据创建和更新时间。

## 数据约束说明

### 主键约束

- `id` 字段作为主键，自增长，确保每条记录的唯一性

### 唯一性约束

```sql
-- 统计日期+银行代码+MCC+省份+分公司+代理商的组合唯一
CREATE UNIQUE INDEX uk_merchant_detail ON merchant_detail_day(
    stat_date, bank_code, mcc_code, province_code, branch_code, agent_code
);
```

### 业务约束

- 金额字段使用分为单位存储，避免小数点精度问题
- 统计日期不能为未来日期
- 所有金额和计数字段不能为负数

## 索引建议

### 主要查询索引

```sql
-- 统计日期索引
CREATE INDEX idx_stat_date ON merchant_detail_day(stat_date);

-- 银行代码索引
CREATE INDEX idx_bank_code ON merchant_detail_day(bank_code);

-- MCC索引
CREATE INDEX idx_mcc_code ON merchant_detail_day(mcc_code);

-- 省份索引
CREATE INDEX idx_province_code ON merchant_detail_day(province_code);

-- 分公司索引
CREATE INDEX idx_branch_code ON merchant_detail_day(branch_code);

-- 代理商索引
CREATE INDEX idx_agent_code ON merchant_detail_day(agent_code);
```

## 数据生成规则

### 数据清洗逻辑

基于transaction_main表按以下维度进行日汇总：

1. **统计维度**：

   - 按统计日期（trans_date）分组
   - 按银行代码（bank_code）分组
   - 按商户行业类型（mcc_code）分组
   - 按商户所在省份（province_code）分组
   - 按商户所属分公司（branch_code）分组
   - 按代理商代码（agent_code）分组

2. **汇总计算**：

   ```sql
   -- 示例汇总SQL
   INSERT INTO merchant_detail_day (
       stat_date, bank_code, bank_name, mcc_code, mcc_name,
       province_code, province_name, branch_code, branch_name,
       agent_code, agent_name, merchant_count, trans_count,
       trans_amount, qualified_merchant_count, qualified_trans_count,
       qualified_trans_amount
   )
   SELECT 
       trans_date as stat_date,
       bank_code,
       MAX(card_bank) as bank_name,
       mcc_code,
       MAX(mcc_name) as mcc_name,
       province_code,
       MAX(province_name) as province_name,
       branch_code,
       MAX(branch_name) as branch_name,
       agent_code,
       MAX(agent_name) as agent_name,
       COUNT(DISTINCT merchant_id) as merchant_count,
       COUNT(*) as trans_count,
       SUM(trans_amt) as trans_amount,
       COUNT(DISTINCT CASE WHEN trans_amt >= 100000 THEN merchant_id END) as qualified_merchant_count,
       SUM(CASE WHEN trans_amt >= 100000 THEN 1 ELSE 0 END) as qualified_trans_count,
       SUM(CASE WHEN trans_amt >= 100000 THEN trans_amt ELSE 0 END) as qualified_trans_amount
   FROM transaction_main 
   WHERE trans_date = '2024-01-15'  -- 指定统计日期
   GROUP BY trans_date, bank_code, mcc_code, province_code, branch_code, agent_code;
   ```

## 数据应用场景

### 1. 商户行业分析

- 按MCC代码分析不同行业商户的交易情况
- 识别高价值行业和低价值行业
- 为行业拓展提供数据支持

### 2. 地区分析

- 按省份分析商户分布和交易情况
- 识别高价值地区和低价值地区
- 为地区拓展提供数据支持

### 3. 分公司业绩分析

- 按分公司分析商户数量和交易情况
- 评估分公司业绩
- 为分公司管理提供数据支持

### 4. 代理商分析

- 按代理商分析商户数量和交易情况
- 评估代理商贡献
- 为代理商管理提供数据支持

### 5. 达标商户分析

- 按不同维度分析达标商户情况
- 识别高价值商户特征
- 为商户运营提供数据支持