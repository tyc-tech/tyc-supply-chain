---
name: vendor-health-monitor
description: 供应商健康度监控 Agent · 7 * 24 监控供应商风险信号，触发预警
---

# Vendor Health Monitor Agent

## 用途

7×24 轮询关键供应商的风险信号（基于 `/tyc-supply-chain-brief` 的增量监控模式）：

- 新增失信 / 被执行 → 🔴 立即预警
- 新增开庭公告 → 🟡 关注
- 新增舆情负面 → 🟡 关注
- 财务变化 → 🔵 月度跟踪

## 输出

- Slack / 企微消息推送
- 邮件日 / 周报
