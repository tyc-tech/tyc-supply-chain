# 🔗 tyc-supply-chain

> **供应链 / 供应商管理 AI SKILL 集** — 天眼查 OpenAPI + MCP 协议驱动的 6 个采购向 SKILL（含建筑工程招投标）

[![License](https://img.shields.io/badge/License-Apache%202.0-green.svg)](LICENSE)
[![MCP](https://img.shields.io/badge/MCP-TYC%20天眼查-orange.svg)](https://agent.tianyancha.com)

---

## 1. 项目简介

`tyc-supply-chain` 为采购总监、供应商管理（SQM）、procurement、供应链风控、建筑总包采购提供 AI Agent SKILL 集，覆盖：

- 新供应商准入 KYC
- 供应商 18 类风险扫描
- 供应商年度复评
- 供应链周报（高管仪表板）
- 采购支出分析
- 建筑工程投标资质核查（资质 / 注册人员 / 业绩 / 不良行为）

---

## 2. 核心价值

```
+---------------------------------------------------------------+
|   供应链全生命周期 AI SKILL × 天眼查数据                      |
|                                                               |
|   准入 → 日常 → 复评 → 深度评估                               |
|   /tyc-new-supplier → /tyc-supply-chain-brief → /tyc-supplier-annual
|                                                               |
|   + 战略决策：                                                 |
|   /tyc-supply-risk      → 18 类风险扫描                       |
|   /tyc-spend-analysis   → 采购支出 + 整合机会                 |
|                                                               |
|   + 建筑工程：                                                 |
|   /tyc-construction-bid → 资质 + 业绩 + 人员 + 不良 四维       |
|                                                               |
+---------------------------------------------------------------+
```

---

## 3. 快速开始（2 种装法选一）

### 方式 A · bash 一键脚本（推荐 · 30 秒搞定）

```bash
bash <(curl -sL https://raw.githubusercontent.com/tyc-opensource/tyc-supply-chain/main/install_tyc_mcp.sh)
```

脚本会：① 提示输入 `TYC_MCP_API_KEY`（[申请](https://agent.tianyancha.com)）→ ② 自动写入 `~/.claude/.mcp.json` → ③ 复制 SKILL 到 `~/.claude/skills/tyc-*` → ④ 复制命令到 `~/.claude/commands/`。完成后**重启 Claude Code** 即可使用。

### 方式 B · 本地 plugin-dir（开发 / 调试）

```bash
git clone https://github.com/tyc-opensource/tyc-supply-chain.git
cd tyc-supply-chain
export TYC_MCP_API_KEY="your_api_key_here"
claude --plugin-dir .
```

启动后项目级 `.mcp.json` 自动加载。

---

### 试用

```
/tyc-new-supplier 某候选供应商公司
/tyc-supply-risk 某在线供应商
/tyc-spend-analysis 某采购方 --category "精密铸件" --region 长三角
/tyc-construction-bid 某建筑总包候选
```

---

## 4. SKILL / Command 列表（6 个）

| # | 命令 | 名称 | 用途 |
|---|------|------|------|
| 1 | `/tyc-supply-risk` | 供应商 18 类风险扫描 | 在线供应商风险监控 |
| 2 | `/tyc-new-supplier` | 新供应商准入 KYC | 准入流程 |
| 3 | `/tyc-supplier-annual` | 供应商年度复评 | 年度回顾 |
| 4 | `/tyc-supply-chain-brief` | 供应链周报 / 高管仪表板 | 每周 KPI |
| 5 | `/tyc-spend-analysis` | 采购支出分析 | 整合机会 / RFQ 策略 |
| 6 | `/tyc-construction-bid` | 建筑工程投标资质核查 | 总包资质审查 |

### 目录结构

```
tyc-supply-chain/
├── skills/
│   ├── supply-risk/SKILL.md
│   ├── new-supplier/SKILL.md
│   ├── supplier-annual/SKILL.md
│   ├── supply-chain-brief/SKILL.md
│   ├── spend-analysis/SKILL.md
│   └── construction-bid/SKILL.md
├── agents/                        # 业务 Agent 定义
│   ├── procurement-calendar-agent.md
│   ├── spend-intelligence-agent.md
│   └── vendor-health-monitor.md
├── evals/
├── docs/
│   ├── SUPPLY_CHAIN_RISKS.md      # 18 类风险清单
│   ├── CONSTRUCTION_QUALS.md      # 建筑资质速查表
│   └── MCP_CONFIGURATION.md
└── README.md
```

---

## 5. 典型场景

### 场景 A: 新供应商准入 KYC

```
/tyc-new-supplier 某新候选供应商
  ↓ 工商 + 股东 + 风险 + 规模 + 财务
Claude: 准入建议 + 合同条款提示
```

### 场景 B: 供应链周报（每周）

```
/tyc-supply-chain-brief {本方采购企业} --period "近 7 天"
  ↓ 并发扫描全部供应商 + 新增风险信号 + 在途事件
Claude: VP 仪表板（健康度 / KPI / 本周行动建议）
```

### 场景 C: 年度采购支出复盘

```
/tyc-spend-analysis {本方采购企业} --category "精密铸件"
  ↓ 供应商池画像 + 品类集中度 + 整合机会 + 市场基准
Claude: TOP 10 整合机会 + 高风险 5 家替换建议 + 年度节约目标拆解
```

### 场景 D: 建筑总包投标资格审查

```
/tyc-construction-bid 某建筑乙方
  ↓ 资质证书 / 注册人员 / 工程业绩 / 不良行为 四维
Claude: 投标资格建议（通过 / 缺件 / 拒绝）+ 证据证书号
```

---

## 6. 天眼查 MCP 集成

| 用途 | 工具 |
|------|------|
| 上下游识别 | `get_suppliers_and_customers` |
| 供应商风险 | `get_risk_overview` + 18 类风险工具 |
| 建筑资质 | `get_construction_qualifications` / `get_construction_registered_personnel` / `get_construction_projects` / `get_construction_bad_conduct` |
| 支出分析 | `get_bidding_info` + `search_companies_by_industry_region` + `search_bids` |

详见 [docs/MCP_CONFIGURATION.md](docs/MCP_CONFIGURATION.md)。

---

## 7. 与 [`tyc-vendor-assessment`](../tyc-vendor-assessment/) 关系

| 维度 | 本仓 | `tyc-vendor-assessment` |
|-----|-----|------------------------|
| SKILL 数 | 6（流程齐套）| 1（深度评估）|
| 适合 | 日常采购运营、年度复盘 | 战略供应商评审、单品类深度尽调 |

两仓可共存，互不冲突。

---

## 8-12. 配置 / FAQ / 贡献 / License / 致谢 / 联系

Apache-2.0 · [LICENSE](LICENSE) · contact@tianyancha.com
