---
name: tyc-supply-chain-brief
description: 供应链周报 / 高管仪表板
argument-hint: "<采购方企业名> [--period 周期] [--vendors 重点供应商列表]"
---

# /tyc-supply-chain-brief · 供应链周报

本命令由 SKILL 文件定义，详见：[`../skills/supply-chain-brief/SKILL.md`](../skills/supply-chain-brief/SKILL.md)

## 快速使用

```
/tyc-supply-chain-brief <searchKey>
```

替换 `<searchKey>` 为目标企业名称或统一社会信用代码。

## 参数与示例

参数与产出格式见 SKILL.md。典型产出：Markdown 报告（可直接上屏或归档）。

## 底层 MCP 调用

通过 `tyc` MCP server（`https://mcp.tianyancha.com/v1`）调用 T1.1 业务语义聚合层工具。

## 相关命令

参见 [`../README.md`](../README.md) SKILL 清单章节。
