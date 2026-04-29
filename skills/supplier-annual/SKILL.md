---
name: tyc-supplier-annual
description: 供应商年度评审的标准化核查工具，输出经营/资质/信用变更结构化报告
category: supply
version: 1.0
---

# 供应商年度健康体检

## 触发条件

年度供应商评审会议、年度合作续签决策、采购年度回顾。

关键词：供应商年度、合作续签、年度体检、采购回顾

## 输入要求

- **searchKey** (必填): 供应商企业名称 或 信用代码

## 执行流程

### Step 1: 经营变化
- `get_company_registration_info` — 当前 vs 去年
- `get_change_records` — 工商变更（近 12 月）
- `get_company_scale` — 规模变化

### Step 2: 资质有效性
- `get_qualifications` — 资质证书与到期
- `get_administrative_license` — 行政许可

### Step 3: 信用记录变化
- `get_credit_evaluation` — 信用评级
- `get_administrative_penalty` — 处罚（近 12 月）
- `get_business_exception` — 经营异常

### Step 4: 司法记录
- `get_judicial_documents`
- `get_dishonest_info`

### Step 5: 业务能力
- `get_bidding_info` — 中标记录
- `get_team_members` — 核心团队

## 输出格式

```markdown
# 供应商年度体检 — {name}

> 体检周期: {year-1} → {year}

## 一、经营变化（同比）
| 指标 | 上年 | 本年 | 变化 |
|------|------|------|------|
| 注册资本 | | | |
| 参保人数 | | | |
| 分支机构 | | | |
| 法定代表人 | | | 变更 / 未变 |

## 二、资质有效性
- 总资质数: {n}（同比 {±x}）
- 临期资质: {n}
- 过期资质: {n}
- 新增资质: {n}

## 三、信用记录变化
- 信用评级: {上年} → {本年}
- 新增处罚: {n} 条
- 经营异常: {n} 次

## 四、司法记录
- 新增诉讼: {n}
- 新增失信: {n}

## 五、业务能力
- 中标项次（本年）: {n}
- 核心团队稳定性: ...

## 六、续签建议
- 综合评级变化: A → A / A → B / ...
- 续签建议: 续签 / 调整合作模式 / 终止
- 关注事项: ...
```

## 示例

输入: `searchKey = "某长期合作供应商"`
