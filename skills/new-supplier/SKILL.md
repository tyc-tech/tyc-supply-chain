---
name: tyc-new-supplier
description: 招投标评审阶段的候选供应商快速筛查工具，3 分钟批量出具筛查结论
category: supply
version: 1.0
---

# 新供应商快速筛选

## 触发条件

招投标评审会前、批量供应商初筛、采购委员会会前数据准备。

关键词：招投标筛选、批量筛查、新供应商初筛、评审前置

## 输入要求

- **searchKey** (必填): 供应商企业名称（支持单个或批量循环调用）

## 执行流程

### Step 1: 主体合规速查
- `get_company_registration_info`
- `get_company_scale`

### Step 2: 黑名单速查
- `get_dishonest_info` — 失信黑名单
- `get_judgment_debtor_info` — 被执行黑名单
- `get_serious_violation` — 严重违法

### Step 3: 资质真实性
- `get_qualifications` — 关键资质
- `get_administrative_license`

### Step 4: 综合
- `get_risk_overview`

## 输出格式

```markdown
# 新供应商速筛 — {name}

## 通过/失败
- ✓ 通过 / ❌ 失败

## 速筛清单
| 检查项 | 结果 |
|-------|------|
| 工商存续 | ✓ / ❌ |
| 失信被执行 | ✓ 无 / ❌ {n} 条 |
| 严重违法 | ✓ 无 / ❌ {n} 条 |
| 必备资质 | ✓ 完整 / ❌ 缺失 |
| 综合风险 | 低 / 中 / 高 |

## 评审建议
- 是否进入下一轮评审: 是 / 否
- 失败原因（若否）: ...
- 加强关注点: ...
```

## 示例

输入: `searchKey = "投标供应商 1"`（批量场景循环调用即可）
