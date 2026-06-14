---
name: socratic-method-cooking
description: Use when the user has a vague empirical-paper topic and wants Codex to first clarify the core theme and data assets, then use verified literature search to make evidence-based research-gap recommendations, and finally match each feasible gap to a conventional or recombined methodology flow for an empirical manuscript.
---

# Socratic Method Cooking / 方法流烹饪

Use this skill to help the user turn a rough empirical-paper idea into a source-backed research-gap recommendation and then match the gap to a defensible methodology flow. It combines Socratic planning, verified literature search, data-asset reasoning, and method-flow synthesis.

The final output is a research-method plan, not code and not an unverified literature list.

## Core Idea

Many empirical papers fail because the research question, data assets, literature gap, identification strategy, model sequence, robustness checks, and contribution claim do not form one coherent chain.

This skill treats methods like recipes:

- First decide what dish the user can actually cook: the most core theme and the user's current data assets.
- Then use `$socratic-paper-finder` to read the literature before recommending gaps.
- Speak through evidence in three modes: `用文献说话`, `借文献说话`, and `立足用户数据资产说话`.
- If the field already has a stable recipe, recommend the conventional robust method flow and explain how to implement it.
- If the user's topic is special, build a "new dish" by combining already accepted method modules from the literature, then test whether the combination is theoretically, empirically, and technically feasible.
- A research gap is useful only if it is real, source-backed, not already saturated, and feasible under the user's current or realistically obtainable data resources.
- Never invent a method, paper, DOI, dataset, effect, parameter, or authority claim.

## Required Skill Composition

When using this skill, reuse the logic of these local skills:

- `$socratic-planner`: first clarify the user's empirical-paper idea through iterative Socratic questioning until explicit approval.
- `$socratic-paper-finder`: after approval, search authoritative sources, verify real references, and build a source-backed evidence table.

If either skill is unavailable, follow the same workflow manually and state the fallback.

## Non-Negotiable Workflow

1. Clarify the user's `most core theme` and `current data assets` before searching.
2. Convert the dialogue into an approved search boundary: topic, population/context, variables, data structure, likely claim type, and gap types to test.
3. Search the web only after approval, using `$socratic-paper-finder` logic.
4. Verify each relevant paper or method source with DOI, PMID/PMCID, publisher page, official guideline page, working-paper page, or institutional source.
5. Read the literature for gap evidence, not just titles, abstracts, or method labels.
6. Make research-gap recommendations by combining `user need + literature reading + data assets`.
7. For each candidate gap, say separately what the literature directly supports, what adjacent literature can be borrowed for, and what the user's data can actually support.
8. Reject gaps that are already solved, too broad, unsupported, or infeasible under the user's data resources.
9. Match each feasible gap to a conventional robust flow or a recombined "new dish" method flow.
10. Validate any recombination with compatibility and gap-feasibility checks before recommending it.
11. Output a structured evidence-based gap recommendation and methodology-flow matching report with source links.

Do not skip the clarification and approval stage unless the user has already supplied all required boundaries and explicitly asks to proceed with searching.

## Phase 1: Core Theme And Data-Asset Lock-In

Ask one compact question set. Prefer choice cards when the user is vague.

```markdown
### 我先锁定“核心主题”和“数据资产”

**卡片 1：最核心的主题**
A. 我能用一句话说清楚研究对象和问题
B. 我只有一个大方向，还需要收窄
C. 我有多个主题候选，需要比较哪个更可做
D. 我主要想找一个能发表的 research gap

请补充：最想研究的对象、场景、人群/行业/地区、核心解释变量、核心结果变量。

**卡片 2：当前数据资产**
A. 已有可分析数据
B. 有目标数据库/公开数据源
C. 需要先找数据
D. 只能做二手文献、案例、政策文本或公开材料

请补充：变量、时间跨度、样本量、空间/机构/个体粒度、是否面板、是否可追踪、是否能合并外部数据、访问权限。

**卡片 3：用户真正想要的贡献**
A. 解释机制/影响路径
B. 估计因果效应
C. 做预测或分类
D. 做测量、指数、评价或比较
E. 找一个更容易被审稿人认可的 gap

**卡片 4：方法偏好**
A. 尽量采用传统稳健方法流
B. 在稳健基础上做小创新
C. 希望组合多个方法流形成新突破
D. 先让文献告诉我哪条路最自然

**卡片 5：输出用途**
A. 写开题/研究设计
B. 写论文方法部分
C. 准备投稿前方法审计
D. 为后续实证代码实现做路线图

**卡片 6：你最想找的 gap 类型**
A. 主题/场景 gap：别人没在这个对象或场景做过
B. 数据/测量 gap：别人没有这个数据、指标或观测粒度
C. 方法/识别 gap：别人方法不够稳健或不能回答当前问题
D. 机制/异质性 gap：别人没有解释为什么、对谁有效、何时有效
E. 先让文献检索后判断，不预设 gap
```

After the user answers:

- Restate the `most core theme` in one sentence.
- Inventory the user's current data assets and missing data in a small table.
- Identify what claims the data can plausibly support: causal, descriptive, predictive, measurement, mechanism, or exploratory.
- Identify the user's target contribution.
- List known constraints, non-goals, and assumptions.
- Draft likely gap types, but mark them as `待文献核验`.
- Draft the search boundary.
- Ask for explicit approval before browsing.

Treat `可以`, `确认`, `没有问题`, `通过`, `approve`, or equivalent explicit approval as permission to search.

Do not search if the most core theme or data assets are still too vague to define search keywords and feasibility criteria. Ask another Socratic clarification round instead.

## Phase 2: Literature And Method Search

Search because the task requires current, source-backed literature.

Search in layers:

1. Core empirical methods for the topic.
2. Directly comparable applied studies.
3. Methodological review, reporting standard, or field guideline sources.
4. Adjacent method flows that solve a similar data, identification, measurement, or robustness problem.
5. Limitation, future-work, and open-question statements in high-quality papers.
6. Recent high-quality papers that show acceptable combinations.

Prioritize:

- Publisher DOI pages, PubMed/PMC/NCBI when relevant, Crossref/OpenAlex/Semantic Scholar metadata, SSRN/NBER/RePEc/arXiv when field-appropriate, official guidelines, and major-journal pages.
- Primary empirical papers over blog posts or unsourced summaries.
- Method papers and reporting standards when judging whether a method module is accepted.

For every included source, record:

- Title, authors, year, venue.
- DOI/PMID/PMCID/publisher/official URL.
- Research question.
- Data and sample.
- Method-flow steps.
- Claimed limitations, future work, or unresolved gaps.
- Identification or validity assumptions.
- Robustness/sensitivity checks.
- What part can be reused for the user's paper.
- Evidence status: `verified`, `partial`, or `reject`.

## Phase 3: Extract Method Flows

Represent each paper's method flow as ordered modules, for example:

```text
Research question
-> theory/mechanism framing
-> data source and sample construction
-> variable/measurement design
-> identification or modeling strategy
-> baseline model
-> robustness checks
-> heterogeneity or mechanism tests
-> validity threats and limitations
-> contribution claim
```

For each method flow, classify:

- `传统稳健流`: commonly used, reviewer-friendly, and directly implementable.
- `邻近可借鉴流`: not the same topic, but solves a similar empirical or identification problem.
- `组合候选模块`: a method module that may be recombined with others.
- `不建议使用`: weak fit, unverifiable, outdated, or likely to create invalid claims.

## Phase 4: Evidence-Based Gap Finder

Before recommending a method flow, cautiously evaluate whether a publishable gap still exists and whether it can be implemented under the user's current data resources.

Do not equate "few papers found" with a real gap. A gap must be supported by literature evidence, reviewer logic, and implementation feasibility.

Use three evidence voices for every gap recommendation:

- `用文献说话`: what verified literature directly says, including established findings, saturated areas, limitations, and future-work statements.
- `借文献说话`: what adjacent literature allows you to borrow by analogy, such as method modules, measurement strategies, identification logic, robustness designs, or theoretical mechanisms.
- `立足用户数据资产说话`: what the user's variables, sample, time span, granularity, mergeability, and access rights can actually support.

Only recommend a gap when these three voices can be made mutually consistent.

Classify each candidate gap:

- `真实可做 gap`: verified sources suggest the issue is unresolved, and the user's data/resources can plausibly address it.
- `可能可做 gap`: evidence is partial or adjacent, and the gap needs more search or a narrower claim.
- `伪 gap/已饱和`: prior literature already solves it, or the novelty is only a change of wording.
- `高风险 gap`: interesting but blocked by missing data, invalid identification, unverifiable measures, or unrealistic workload.
- `不可做 gap`: cannot be implemented under current resources without changing the research question or obtaining major new data.

Evaluate gap feasibility against the user's assets:

- Data availability: required variables, sample, time span, granularity, merge keys, and access rights.
- Identification feasibility: whether the gap can support causal, predictive, descriptive, measurement, or mechanism claims.
- Method-cooking route: which accepted modules can be combined to address the gap.
- Minimum viable analysis: the smallest empirical design that can test whether the gap is real.
- Difficulty: `low`, `medium`, `high`, or `not feasible`.
- Main blocker: data, theory, measurement, identification, computation, ethics, or citation support.

Prefer smaller executable gaps over broad impressive-sounding gaps. If a gap is attractive but not feasible with current assets, either downgrade it or propose the missing asset needed.

Use this recommendation test:

```text
candidate gap is recommendable only if:
  literature evidence shows the issue is unresolved or under-tested
  and adjacent literature provides reusable methods or theory
  and the user's current/obtainable data can operationalize the gap
  and the claim type does not exceed what the data and method can support
```

## Phase 5: Traditional Flow Vs New-Dish Flow

First ask whether a stable conventional method flow already fits.

If yes, recommend the conventional flow:

- Explain why it is the safest path.
- Show the step-by-step implementation logic.
- List required data and assumptions.
- List robustness checks.
- State what contribution remains possible without overclaiming novelty.

If no, or if the user's need is special, design "new dish" candidates:

- Use only method modules already seen in verified literature.
- Combine modules by function, not by superficial similarity.
- Keep the sequence coherent: problem -> data -> measurement -> identification/model -> validation -> claim.
- Explain the analogy in plain language, like combining accepted dishes into a new but cookable recipe.

Example logic:

```text
Stable flow A: tomato + egg
Stable flow B: green pepper + pork
Candidate new flow: tomato + green pepper

Academic translation:
Can the measurement module from Flow A be paired with the identification strategy from Flow B?
Do their data structure, assumptions, time order, and outcome definitions remain compatible?
If compatible, what extra robustness check is needed to convince reviewers?
```

Do not propose mechanical permutations. A combination is valid only if it passes the compatibility checks.

## Compatibility Checks For New-Dish Flows

Score each candidate as `green`, `yellow`, or `red`.

Check:

- Research-question fit: does the combination answer the user's actual question?
- Theory fit: do the mechanisms contradict each other?
- Data fit: are the required data granularity, time scale, sample, and variables available?
- Measurement fit: are constructs and proxies defensible?
- Identification/model fit: do assumptions remain coherent after combination?
- Order fit: do the steps create a logical empirical pipeline?
- Robustness fit: can common threats be tested or bounded?
- Literature legitimacy: is each module accepted in verified sources?
- Novelty fit: is the contribution more than relabeling old methods?
- Gap fit: does the flow address a real, source-backed, feasible gap?
- Feasibility: can the user realistically implement it?

Reject or downgrade any candidate with unresolved red flags in identification, data availability, or source legitimacy.

## Output Template

Use Chinese by default unless the user requests English.

```markdown
# 方法流匹配报告

## 1. 论文想法定稿
- 最核心主题：
- 核心问题：
- 目标贡献：
- 数据条件：
- 不做什么：
- 关键假设：

## 2. 用户数据资产盘点
| 数据资产 | 已有/可获得 | 变量/指标 | 时间跨度 | 样本/粒度 | 可合并性 | 可支持的主张 | 主要缺口 |

## 3. 检索边界与证据来源
- 检索关键词：
- 纳入范围：
- 排除范围：
- 已验证来源：

## 4. 文献阅读结论：用文献说话
| 文献/来源 | 已解决什么 | 尚未解决什么 | 明示局限/未来研究 | 对本研究的启发 |

## 5. 邻近借用：借文献说话
| 可借用模块 | 来源文献 | 原场景 | 可迁移到本题的理由 | 迁移风险 |

## 6. 学界已有方法流地图
| 方法流 | 代表文献 | 适用问题 | 数据要求 | 核心步骤 | 稳健性 | 可迁移模块 |

## 7. Gap Finder：处处循证的 research gap recommendation
| 候选 gap | 用户需求依据 | 用文献说话 | 借文献说话 | 立足用户数据资产说话 | 是否仍存在 | 实现难度 | 推荐等级 | 主要风险 |

### Gap 结论
- 真实可做 gap：
- 可能可做 gap：
- 伪 gap/已饱和：
- 高风险或不可做 gap：

## 8. 传统稳健方法流推荐
- 是否存在直接可用的传统流：
- 推荐路径：
- 实现步骤：
- 必备数据：
- 必做稳健性：
- 适合投稿叙事：

## 9. “新菜式”组合创新候选
| 候选流 | 组合来源 | 组合逻辑 | 可行性 | 最大风险 | 必要验证 |

## 10. 最终推荐：gap-methodology flow 匹配
- 首选方法流：
- 备选方法流：
- 不建议的方法流：
- 为什么这样选：

## 11. 可执行路线图
1. 数据准备
2. 指标/变量构造
3. 基线模型或主分析
4. 稳健性与敏感性
5. 异质性/机制/扩展分析
6. 论文写作中的方法叙事

## 12. 仍需用户确认
- 待确认问题：
- 下一步：
```

If the user needs an evidence workbook, create an Excel-compatible table following `$socratic-paper-finder` conventions.

## Evidence And Safety Rules

- All literature-backed claims need source links.
- Mark unknowns as `未核验`, `原文未披露`, or `待确认`; do not fill gaps from memory.
- Do not overclaim novelty. Use `可能 gap`, `待核验 gap`, or `已被部分解决` when evidence is incomplete.
- A gap is not recommended unless it is both literature-grounded and implementable under the user's data/resource constraints.
- Separate direct evidence from borrowed evidence. Do not present an analogy from adjacent literature as if it directly proves the user's topic.
- Tie every recommended gap to an explicit data asset or clearly state the missing data needed.
- Do not ask for passwords, API keys, private datasets, confidential manuscripts, or unreleased results. Ask for redacted summaries when sensitive context is involved.
- Do not run code, download private files, or access private systems as part of this skill unless the user explicitly switches from planning/search to execution.
- Make clear when a proposed new-dish flow is a hypothesis requiring validation, not an established method.

## Approval Gate

After presenting the final report, ask:

```markdown
请选择：
A. 没有问题，采用这个方法流
B. 继续追问，我要再收窄论文想法
C. 继续检索，我要扩大/改变文献边界
D. 修改组合逻辑，我认为某个方法模块不合适
```

Only treat A or equivalent explicit approval as completion. Otherwise continue the loop.
