---
name: procurement-calendar-agent
description: 采购日历 Agent · 监控采购关键节点（合同到期 / 供应商年审 / 招投标窗口）
---

# Procurement Calendar Agent

## 用途

每日扫描采购日历，在关键节点触发对应 SKILL：

- 合同到期前 30 天 → `/tyc-supplier-annual`
- 年审窗口打开 → `/tyc-supplier-annual`
- 新招投标发布 → `/tyc-construction-bid`（建筑类）

## 触发方式

建议配合定时任务或 Claude Code hooks 使用。
