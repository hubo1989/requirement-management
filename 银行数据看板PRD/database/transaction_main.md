# Transaction Main 表结构文档

## 表基本信息

- **表名**: transaction_main
- **表描述**: 交易主表，存储银行交易相关的详细数据
- **字段总数**: 137个字段
- **创建时间**: 2024年
- **数据类型**: 包含字符串、整型、浮点型等多种数据类型

## 表结构详细信息

| 序号 | 字段名称                | 数据类型      | 约束条件 | 字段描述                                                                     |
| ---- | ----------------------- | ------------- | -------- | ---------------------------------------------------------------------------- |
| 1    | trans_id                | string        | NOT NULL | 交易数据ID                                                                   |
| 2    | srefno                  | string        |          | 系统参考号                                                                   |
| 3    | mpos_bus_id             | string        |          | MPOS流水busid                                                                |
| 4    | mpos_user_id            | string        |          | MPOS用户ID                                                                   |
| 5    | mpos_mobile             | string        |          | MPOS手机号                                                                   |
| 6    | trans_time              | string        |          | 交易时间                                                                     |
| 7    | trans_date              | string        |          | 交易日期                                                                     |
| 8    | trans_month             | bigint        |          | 交易月份                                                                     |
| 9    | trans_hour              | bigint        |          | 交易小时                                                                     |
| 10   | trans_type              | string        |          | DD交易类型                                                                   |
| 11   | trans_code              | string        |          | DD交易代码                                                                   |
| 12   | is_direct_cups          | bigint        |          | 是否银联直联（银联要求有些用户必须要直接关联到银联）                         |
| 13   | trans_channel           | string        |          | 交易渠道                                                                     |
| 14   | pay_channel             | string        |          | 清结算支付渠道                                                               |
| 15   | agent_org               | string        |          | 外发代理机构号                                                               |
| 16   | agent_trans_code        | string        |          | 外发交易码                                                                   |
| 17   | trans_status            | string        |          | 交易状态                                                                     |
| 18   | trans_cnt               | bigint        |          | 交易笔数                                                                     |
| 19   | trans_amt               | decimal(20,3) |          | 交易金额(分)                                                                 |
| 20   | amt_interval            | string        |          | 金额区间                                                                     |
| 21   | ccy_code                | string        |          | DD币种                                                                       |
| 22   | pay_cnt                 | bigint        |          | 支付笔数                                                                     |
| 23   | pay_amt                 | decimal(14,3) |          | 支付金额                                                                     |
| 24   | swing_card_way          | string        |          | 刷卡方式                                                                     |
| 25   | pay_style               | string        |          | DD支付形态(微信POSP等)预留                                                   |
| 26   | pay_card_no             | string        |          | 支付卡号                                                                     |
| 27   | card_bin                | string        |          | 卡BIN                                                                        |
| 28   | card_type               | string        |          | DD卡种(区分借贷记)                                                           |
| 29   | card_bank               | string        |          | 发卡银行                                                                     |
| 30   | bank_code               | string        |          | 工农中建等各行代码                                                           |
| 31   | card_attr_sign          | string        |          | DD内外卡类型                                                                 |
| 32   | settle_amt              | decimal(20,3) |          | 结算金额                                                                     |
| 33   | fee_amt                 | decimal(14,3) |          | 交易手续费(商户成本)                                                         |
| 34   | merchant_base_fee       | decimal(14,3) |          | 商户基准成本(代理商成本)                                                     |
| 35   | cups_std_rate           | string        |          | 银联费率标准(借贷分离)                                                       |
| 36   | fee_rate                | string        |          | 消费费率                                                                     |
| 37   | merchant_id             | string        |          | 商户号                                                                       |
| 38   | merchant_name           | string        |          | 商户名称                                                                     |
| 39   | merchant_type           | string        |          | 商户类型                                                                     |
| 40   | merchant_level          | string        |          | 商户等级                                                                     |
| 41   | merchant_status         | string        |          | 商户状态                                                                     |
| 42   | terminal_id             | string        |          | 终端号                                                                       |
| 43   | terminal_type           | string        |          | 终端类型                                                                     |
| 44   | terminal_status         | string        |          | 终端状态                                                                     |
| 45   | pos_entry_mode          | string        |          | POS进入模式                                                                  |
| 46   | batch_no                | string        |          | 批次号                                                                       |
| 47   | trace_no                | string        |          | 流水号                                                                       |
| 48   | auth_code               | string        |          | 授权码                                                                       |
| 49   | resp_code               | string        |          | 应答码                                                                       |
| 50   | resp_msg                | string        |          | 应答信息                                                                     |
| 51   | org_trans_date          | string        |          | 原交易日期                                                                   |
| 52   | org_trans_time          | string        |          | 原交易时间                                                                   |
| 53   | org_trace_no            | string        |          | 原流水号                                                                     |
| 54   | org_auth_code           | string        |          | 原授权码                                                                     |
| 55   | org_resp_code           | string        |          | 原应答码                                                                     |
| 56   | org_amt                 | decimal(20,3) |          | 原交易金额                                                                   |
| 57   | org_settle_amt          | decimal(20,3) |          | 原结算金额                                                                   |
| 58   | org_fee_amt             | decimal(14,3) |          | 原手续费                                                                     |
| 59   | reversal_flag           | string        |          | 冲正标志                                                                     |
| 60   | reversal_reason         | string        |          | 冲正原因                                                                     |
| 61   | reversal_time           | string        |          | 冲正时间                                                                     |
| 62   | mcc_code                | string        |          | 商户MCC                                                                      |
| 63   | txn_mcc_code            | string        |          | 增值商户MCC                                                                  |
| 64   | trans_area              | string        |          | 交易地区码(银联32域)                                                         |
| 65   | province_code           | string        |          | 交易省份代码                                                                 |
| 66   | city_code               | string        |          | 交易城市代码                                                                 |
| 67   | txn_province            | string        |          | 交易省份(增值)                                                               |
| 68   | txn_city                | string        |          | 交易城市(增值)                                                               |
| 69   | mobile_area             | string        |          | 手机号对应地区                                                               |
| 70   | discount_mark           | bigint        |          | 优惠标志                                                                     |
| 71   | discount_std            | string        |          | 优惠标准                                                                     |
| 72   | txn_discount_std        | string        |          | 优惠标准(增值)                                                               |
| 73   | sign_org                | string        |          | 签约机构                                                                     |
| 74   | service_org             | string        |          | 落地机构                                                                     |
| 75   | acq_org                 | string        |          | 收单机构                                                                     |
| 76   | acq_node                | string        |          | 收单节点                                                                     |
| 77   | iss_org                 | string        |          | 发卡机构                                                                     |
| 78   | iss_node                | string        |          | 发卡节点                                                                     |
| 79   | fwd_org                 | string        |          | 转发机构                                                                     |
| 80   | fwd_node                | string        |          | 转发节点                                                                     |
| 81   | proc_org                | string        |          | 处理机构                                                                     |
| 82   | proc_node               | string        |          | 处理节点                                                                     |
| 83   | clear_date              | string        |          | 清算日期                                                                     |
| 84   | settle_date             | string        |          | 结算日期                                                                     |
| 85   | clear_flag              | string        |          | 清算标志                                                                     |
| 86   | settle_flag             | string        |          | 结算标志                                                                     |
| 87   | refund_state            | string        |          | 退款状态                                                                     |
| 88   | refund_amt              | decimal(20,3) |          | 已退金额                                                                     |
| 89   | orig_fee_amt            | decimal(14,3) |          | 原始手续费                                                                   |
| 90   | fee_settle_flag         | string        |          | 手续费结算标志                                                               |
| 91   | income_sys_check_date   | string        |          | 入账系统核对日期                                                             |
| 92   | thd_chk_flag            | string        |          | 与第三方对账标志                                                             |
| 93   | usr_fee_ddt_flg         | string        |          | 手续费内扣标志                                                               |
| 94   | back_code               | string        |          | 退回码                                                                       |
| 95   | fake_card_flag          | bigint        |          | 伪卡标识                                                                     |
| 96   | device_type             | string        |          | 设备型号                                                                     |
| 97   | tran_tim_str            | string        |          | 交易时间字符串                                                               |
| 98   | is_his                  | bigint        |          | 是否历史数据                                                                 |
| 99   | crd_no1                 | string        |          | 订单id                                                                       |
| 100  | special_charge_type     | bigint        |          | 商户优惠标识(值含分离后)                                                     |
| 101  | cups_std_exchange       | decimal(14,3) |          | 银联标准交换费(值含分离)                                                     |
| 102  | cups_std_settle         | decimal(14,3) |          | 银联标准结算清算费                                                           |
| 103  | cups_shd_exchange       | decimal(14,3) |          | 银联应收交换费(值含分离)                                                     |
| 104  | cups_shd_settle         | decimal(14,3) |          | 银联应收结算清算费(值含分离)                                                 |
| 105  | cups_real_exchange      | decimal(14,3) |          | 银联实收交换费(值含分离)                                                     |
| 106  | cups_real_settle        | decimal(14,3) |          | 银联实收结算清算费(值含分离)                                                 |
| 107  | txn_special_charge_type | bigint        |          | 交易特殊收费类型                                                             |
| 108  | bill_no                 | string        |          | 商户订单号                                                                   |
| 109  | rom_ver                 | string        |          | 固件厂商版本                                                                 |
| 110  | maintain_code           | string        |          | 维护方代码                                                                   |
| 111  | trade_kind              | string        |          | 行业小类                                                                     |
| 112  | coop_bank               | string        |          | 合作银行机构号                                                               |
| 113  | sid                     | string        |          | MPOS前置交易流水号                                                           |
| 114  | client_ip               | string        |          | MPOS交易发生的真实IP                                                         |
| 115  | client_location         | string        |          | MPOS交易发生的经纬坐标                                                       |
| 116  | small_secret            | string        |          | 小额免密标识                                                                 |
| 117  | segment1                | string        |          | 如果SMALL_SECRET为1，则本字段表示为其转化方案对机构 对应机构表SYS_ORGAN_INFO |
| 118  | maintain_org            | string        |          | 维护机构                                                                     |
| 119  | order_no                | string        |          | 订单号                                                                       |
| 120  | branch_org_id           | string        |          | 分支机构ID                                                                   |
| 121  | ori_merchant_code       | string        |          | 原始商户号(多商户号)                                                         |
| 122  | ori_biz_term_no         | string        |          | 原始业务终端号                                                               |
| 123  | small_product_class     | string        |          | 产品小类                                                                     |
| 124  | ifdeposit               | string        |          | 押金交易                                                                     |
| 125  | actyp                   | string        |          | 扫码借贷记标识                                                               |
| 126  | device_sn               | string        |          | 终端序列号                                                                   |
| 127  | product_id              | string        |          | 产品id                                                                       |
| 128  | pay_card_no_mask        | string        |          | pay_card_no升级字段                                                          |
| 129  | busi_type_code          | string        |          | 业务类别                                                                     |
| 130  | ymd                     | string        |          | 年月日                                                                       |
| 131  | sweep_mark              | string        |          | 扫码标识                                                                     |
| 132  | partition_field1        | NULL          |          | 分区字段1                                                                    |
| 133  | partition_field2        | NULL          |          | 分区字段2                                                                    |
| 134  | col_name                | data_type     |          | 列名                                                                         |
| 135  | partition_field3        | NULL          |          | 分区字段3                                                                    |
| 136  | ymd                     | string        |          | 年月日(分区)                                                                 |
| 137  | sweep_mark              | string        |          | 扫码标识(分区)                                                               |

## 字段分类说明

### 1. 基础交易信息字段 (1-11)

包含交易的基本标识信息，如交易ID、参考号、时间等核心字段。

### 2. 渠道和机构信息字段 (12-17)

记录交易涉及的各种渠道、代理机构等信息。

### 3. 金额和计数字段 (18-23)

存储交易相关的金额、笔数等数值信息。

### 4. 支付卡片信息字段 (24-31)

记录支付卡的详细信息，包括卡号、卡种、发卡行等。

### 5. 费用和结算字段 (32-36)

存储各种费用、费率和结算相关信息。

### 6. 商户信息字段 (37-41)

记录商户的基本信息和状态。

### 7. 终端设备字段 (42-49)

存储终端设备相关信息和交易响应码。

### 8. 原交易信息字段 (50-58)

记录原始交易的相关信息，用于退款、冲正等场景。

### 9. 冲正相关字段 (59-61)

处理交易冲正的相关信息。

### 10. 地理位置字段 (62-69)

记录交易发生的地理位置信息。

### 11. 优惠和折扣字段 (70-72)

存储交易优惠相关信息。

### 12. 机构节点字段 (73-82)

记录交易处理过程中涉及的各个机构节点。

### 13. 清算结算字段 (83-90)

处理交易的清算和结算相关信息。

### 14. 系统管理字段 (91-99)

系统内部管理和标识字段。

### 15. 银联费用相关字段 (100-107)

存储银联相关的各种费用信息，包括标准费用、应收费用、实收费用等。

### 16. 商户订单和设备信息字段 (108-112)

记录商户订单号、设备版本、维护信息等商户相关数据。

### 17. MPOS交易详细信息字段 (113-118)

存储MPOS交易的详细信息，包括流水号、IP地址、地理位置等。

### 18. 订单和商户扩展字段 (119-125)

记录订单号、原始商户信息、产品分类、押金交易等扩展信息。

### 19. 设备和产品标识字段 (126-131)

存储设备序列号、产品ID、业务类别、扫码标识等设备和产品相关信息。

### 20. 分区和系统字段 (132-137)

数据库分区相关字段和系统内部使用的特殊字段。

## 数据约束说明

### 主键约束

- `trans_id` 字段作为主键，确保每条交易记录的唯一性

### 数据类型约束

- **string类型**: 用于存储文本信息，如ID、名称、状态等
- **bigint类型**: 用于存储大整数，如计数、标志位等
- **decimal类型**: 用于存储精确的金额数据，避免浮点数精度问题

### 业务约束

- 金额字段使用分为单位存储，避免小数点精度问题
- 时间字段支持多种格式，便于不同系统间的数据交换
- 状态字段使用标准化编码，确保数据一致性

## 索引建议

### 主要查询索引

```sql
-- 交易日期索引
CREATE INDEX idx_trans_date ON transaction_main(trans_date);

-- 商户号索引
CREATE INDEX idx_merchant_id ON transaction_main(merchant_id);

-- 交易状态索引
CREATE INDEX idx_trans_status ON transaction_main(trans_status);

-- 组合索引：日期+商户
CREATE INDEX idx_date_merchant ON transaction_main(trans_date, merchant_id);
```

### 性能优化索引

```sql
-- 金额范围查询索引
CREATE INDEX idx_trans_amt ON transaction_main(trans_amt);

-- 时间范围查询索引
CREATE INDEX idx_trans_time ON transaction_main(trans_time);

-- 银行代码索引
CREATE INDEX idx_bank_code ON transaction_main(bank_code);
```

## 数据治理说明

### 数据质量要求

1. **完整性**: 核心字段不允许为空
2. **一致性**: 状态字段必须符合预定义的枚举值
3. **准确性**: 金额字段必须与业务规则一致
4. **时效性**: 交易数据应实时或准实时入库

### 数据安全要求

1. **敏感信息脱敏**: 卡号、手机号等敏感信息需要脱敏处理
2. **访问控制**: 建立严格的数据访问权限控制
3. **审计日志**: 记录所有数据访问和修改操作
4. **数据备份**: 定期备份重要交易数据

### 数据保留策略

1. **热数据**: 近3个月数据保持在主表
2. **温数据**: 3-12个月数据迁移到历史表
3. **冷数据**: 超过1年的数据归档到冷存储
4. **法规要求**: 按照金融监管要求保留必要的历史数据

## 使用说明

### 常用查询示例

```sql
-- 查询指定日期的交易记录
SELECT * FROM transaction_main 
WHERE trans_date = '2024-01-15';

-- 查询指定商户的交易汇总
SELECT merchant_id, COUNT(*) as trans_count, SUM(trans_amt) as total_amount
FROM transaction_main 
WHERE trans_date BETWEEN '2024-01-01' AND '2024-01-31'
GROUP BY merchant_id;

-- 查询失败交易记录
SELECT * FROM transaction_main 
WHERE trans_status != 'SUCCESS'
AND trans_date = CURRENT_DATE;
```

### 注意事项

1. 查询大量历史数据时建议使用分页查询
2. 金额计算时注意单位转换（分转元）
3. 时间字段查询时注意时区处理
4. 敏感信息查询需要相应权限