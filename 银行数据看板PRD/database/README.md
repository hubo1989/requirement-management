# 银行交易数据库设计项目

## 项目概述

本项目是交易明细的统计表清洗方案，专门用于处理大规模交易数据统计的存储、聚合和分析。系统支持动态配置、数据质量监控、性能优化等企业级功能。

## 项目特点

### 🚀 核心功能

- **交易数据统计：** 支持多种支付渠道、卡类型的交易统计数据存储
- **智能聚合**: 自动化日统计数据聚合，支持多维度分析
- **动态配置**: 业务参数可动态调整，无需修改代码
- **质量监控**: 完整的数据质量检查和清理机制
- **性能优化**: 分区表、复合索引、存储过程优化

### 🛡️ 企业级特性

- **数据约束**: 完善的字段约束和校验规则
- **异常处理**: 存储过程包含完整的异常处理机制
- **日志记录**: 详细的执行日志和质量检查日志
- **分区管理**: 按月分区，支持历史数据管理
- **安全设计**: 卡号脱敏、权限控制

## 核心表结构

### 主要数据表

1. **business_config** - 业务配置表
2. **transaction_main** - 主交易表（数据来源）
3. **daily_transaction_stats** - 日统计汇总表（抽取并清洗结果）
4. **data_quality_log** - 数据质量日志表
5. **aggregation_log** - 聚合执行日志表

## 使用示例

### 日常数据聚合

```sql
-- 聚合指定日期数据
CALL aggregate_daily_stats('2024-01-01');

-- 查看聚合结果
SELECT * FROM daily_transaction_stats WHERE stats_date = '2024-01-01';
```

### 配置管理

```sql
-- 修改达标阈值
UPDATE business_config 
SET config_value = '6000.000' 
WHERE config_key = 'qualified_amount_threshold';

-- 获取当前配置
SELECT get_config_value('qualified_amount_threshold');
```

### 数据质量监控

```sql
-- 检查数据质量
CALL check_data_quality('2024-01-01');

-- 查看质量报告
SELECT * FROM data_quality_log WHERE check_date = '2024-01-01';
```

## 扩展功能

### 支持的业务场景

- 银行卡消费统计
- 风险交易监控
- 渠道效果分析
- 商户交易分析

### 可扩展配置

- 达标金额阈值
- 高风险金额阈值
- 数据保留策略
- 质量检查规则
- 聚合计算规则

### 数据类型规范

- 金额字段: `DECIMAL(20,3)`
- 日期字段: `VARCHAR(10)` 格式 'YYYY-MM-DD'
- 时间字段: `VARCHAR(8)` 格式 'HH:MM:SS'
- 状态字段: `ENUM` 类型限定取值
