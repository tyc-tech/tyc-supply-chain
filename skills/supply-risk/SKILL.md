---
name: tyc-supply-risk
description: 供应链韧性管理的持续监控工具，实时扫描失信/破产/司法拍卖等高危信号
category: supply
version: 1.0
---

# 供应链风险扫描

## 触发条件

核心供应商持续监控、供应中断预防、关键物料供应商月度体检。

关键词：供应链监控、断供预警、供应商体检

## 输入要求

- **searchKey** (必填): 监控供应商名称（支持批量）

## 执行流程

### Step 1: 当前状态
- `get_company_registration_info` — 当前工商状态
- `get_business_exception` — 经营异常

### Step 2: 高危信号
- `get_dishonest_info` — 失信
- `get_judgment_debtor_info` — 被执行
- `get_bankruptcy_reorganization` — 破产重整
- `get_judicial_auction` — 司法拍卖

### Step 3: 资产受限
- `get_equity_freeze` — 股权冻结
- `get_chattel_mortgage_info` — 动产抵押

### Step 4: 短期变更（异动信号）
- `get_change_records` — 变更记录（关注法人/资本/地址）
- `get_cancellation_record_info` — 注销备案

### Step 5: 综合
- `get_risk_overview`

## 输出格式

```markdown
# 供应链风险监控 — {name}

> 监控时点: {now}

## 高危信号
🚨 失信被执行: {n} 条（新增 {x} 条）
🚨 破产重整: 是 / 否
🚨 司法拍卖: {n} 项
🚨 大额被执行: {amount}

## 中危信号
⚠️ 股权冻结
⚠️ 动产抵押激增
⚠️ 法定代表人变更
⚠️ 经营异常

## 异动信号
- 工商变更次数（近 90 天）: {n}
- 注销公告: 是 / 否

## 应急建议
- 是否触发断供预警: 是 / 否
- 紧急措施:
  - 启动备供切换
  - 加快交付现有订单
  - 库存囤积
  - 预付款催回
```

## 示例

输入: `searchKey = "ABC 关键供应商"`
