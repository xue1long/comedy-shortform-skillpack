---
name: comic-toolbox
description: |
  Router for John Vorhaus Comic Toolbox methods. Dispatches to individual tool skills for premise, character, toolbox diagnosis, sketch structure, throughline, jeopardy, and sitcom arcs.
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: router
  cangjie.bundle-id: bundle.comic-toolbox
  cangjie.capability-count: 12
  cangjie.entrypoint-count: 8
---
# The Comic Toolbox — 来源路由入口（compact pack）

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- The book does not teach stand-up, improv, or visual comedy directly.
- Pre-1994 examples are Western/sitcom-centric; does not cover short-form web drama.

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. Comedy is truth and pain—universal reference is the audience entry ticket.
2. The comic premise is the gap between comic reality and real reality; premises are falsifiable one-sentence claims.
3. Every useful character is a funnel: Strong Comic Perspective + Flaws + Humanity + Exaggeration.
4. Comic throughlines use seven beats and a double-win resolution.
5. Jeopardy is the audience reason to care; raise price of failure and prize for success.

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| apply comic-premise to a comic beat | references/capabilities/comic-premise.md | 已晋级为独立 Skill `comic-premise`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| apply comic-perspective to a comic beat | references/capabilities/comic-perspective.md | 已晋级为独立 Skill `comic-perspective`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| apply comic-toolbox-tools to a comic beat | references/capabilities/comic-toolbox-tools.md | 已晋级为独立 Skill `comic-toolbox-tools`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| apply sketch-structure to a comic beat | references/capabilities/sketch-structure.md | 已晋级为独立 Skill `sketch-structure`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| apply comic-throughline to a comic beat | references/capabilities/comic-throughline.md | 已晋级为独立 Skill `comic-throughline`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| apply comic-jeopardy to a comic beat | references/capabilities/comic-jeopardy.md | 已晋级为独立 Skill `comic-jeopardy`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| apply sitcom-structure to a comic beat | references/capabilities/sitcom-structure.md | 已晋级为独立 Skill `sitcom-structure`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| use comic-risk-mindset via router | references/capabilities/comic-risk-mindset.md | — |
| use comic-truth-pain via router | references/capabilities/comic-truth-pain.md | — |
| use comic-rewrite via router | references/capabilities/comic-rewrite.md | — |
| use comic-scrapmetal via router | references/capabilities/comic-scrapmetal.md | — |
| use comic-genre-types via router | references/capabilities/comic-genre-types.md | — |

**非能力类查询**：
- 书名/作者/章节/整书概览 → references/overview.md
- 术语解释 → references/glossary.md
- 决策规则速查（不需要原文依据时） → references/cheatsheet.md
- 完整意图与关键词索引（本表未覆盖的意图先查这里） → references/capability-index.md

## 加载规则

- 每次任务先读本文件，再按路由表加载 **1** 张能力卡；任务明确跨域时最多加载 2 张。
- 概览/书名类问题不加载能力卡，用「核心原则」与 overview.md 回答。
- 路由表与 capability-index.md 都无法命中的意图，明确告知超出本书范围，不要硬套。

## 边界与判停

- If the source cannot be verified in the bundled chapters, downgrade to reference.
