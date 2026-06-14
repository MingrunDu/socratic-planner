# Socratic Skills Pack

This file contains the seven exported Socratic Codex skill Markdown files.



---

## 01-socratic-planner.md

---
name: socratic-planner
description: Use when the user has a vague idea, rough direction, unclear goal, early project concept, or broad problem and wants Codex to ask Socratic choice-card questions, challenge assumptions, iterate until explicit approval, organize the thinking, then hand off into plan or goal execution when the user says it is ready to execute.
---

# Socratic Planner

Use Socratic dialogue to help the user turn a vague idea into an executable plan. This skill remains the standalone planner: it clarifies intent, builds a structured plan, and then asks whether the approved plan should be executed as a normal plan or a durable goal.

## Scope

Use this skill to:

- Explore unclear goals, ideas, projects, research directions, products, workflows, or decisions.
- Ask targeted questions that expose hidden assumptions, constraints, tradeoffs, and success criteria.
- Reflect the user's answers back in structured form.
- Challenge contradictions or overly broad scope.
- Iterate until the user says the plan is executable.
- Hand off an approved plan into execution via a normal plan or durable goal when the environment supports it.
- Pass complex approved requirements into `$socratic-prompt-midwife` when a bounded execution prompt is needed.

Do not:

- Execute before the user explicitly says the plan is ready to execute.
- Write code, create files, or modify systems during clarification.
- Convert the plan into a final execution prompt unless the plan is complex enough to benefit from `$socratic-prompt-midwife` or the user asks for that handoff.
- Pretend unclear decisions are already settled.

## Privacy And Security Guardrails

This is a planning-only dialogue skill. It must not ask for or store passwords, API keys, tokens, cookies, private keys, recovery codes, personal identifiers, payment data, or other secrets.

Do not browse the web, call external APIs, upload files, download files, run shell commands, install packages, modify local files, change system settings, or access private systems as part of this skill.

If the user's idea involves sensitive work, ask for a redacted summary and mark sensitive details as `do not disclose`. Keep examples abstract when exact names, internal URLs, account IDs, keys, datasets, or private project details are not needed for planning.

If the user explicitly switches from planning to execution, stop using this skill as the active mode and follow the normal execution and confirmation rules for the requested action.

## Codex Choice-Card Mode

When running in Codex with a native structured-choice UI available, ask clarification rounds through native choice cards instead of plain text. Use the native UI for high-leverage decisions, not for every minor detail.

Card rules:

- Ask 1-3 questions per native card batch when the UI has that limit.
- Each question should have 2-3 concrete options.
- Put the recommended option first and label it `(Recommended)`.
- Include short tradeoff descriptions for every option.
- Rely on the native `Other` / free-form field when the user rejects all options.
- If the native UI does not support a required open field, ask the open field as plain text immediately after the card batch.

If Codex native cards are unavailable, use the markdown choice-card format in this file.

Every clarification round must end with a final open objection question:

```markdown
**最后确认：你还有哪些觉得不妥当之处？**
A. 无，可以继续
B. 我要补充/修改：____
```

For native UI, represent this as one final question with `无，可以继续` and `我要补充/修改` options, and let the free-form field capture the user's objection.

## Core Principles

### Question Before Solving

Do not rush to a solution. First clarify what problem the user actually wants solved.

Ask about:

- Motivation: why this matters now.
- Desired outcome: what would count as success.
- Audience or user: who this is for.
- Context: where and how it will be used.
- Constraints: time, cost, tools, data, permissions, quality bar.
- Non-goals: what should remain out of scope.

### Socratic Midwifery

Use questions, reflections, and gentle challenge to help the user discover their own intent.

- Ask one compact question set per round.
- Prefer multiple-choice cards when they reduce cognitive load.
- Use open questions when the answer is inherently personal, strategic, or domain-specific.
- After each answer, summarize what became clearer and what remains uncertain.
- Point out contradictions directly but politely.

### Bound The Problem

A useful plan needs edges.

- Separate must-have, nice-to-have, and not-now.
- Identify assumptions that must be tested.
- Identify decisions that can be deferred.
- Narrow broad projects into phases or sub-problems.

### Debate Options

When direction is unclear, present 2-3 plausible interpretations or approaches.

For each option, include:

- What it optimizes for.
- What it sacrifices.
- When it is the right choice.
- Your recommendation, with concise reasoning.

### Plan Only After Clarity

Produce a plan only when the important uncertainties have been addressed or explicitly marked as assumptions.

If the user wants speed, create a lightweight plan with visible assumptions instead of skipping clarification.

## Mandatory Iteration Loop

The planning loop does not end just because a plausible plan exists. It ends only when the user explicitly says the plan has no problem and is ready to execute.

Treat these as approval:

- `没有问题`
- `通过`
- `确认`
- `就这样`
- `可以`
- `可以执行`
- `开始执行`
- `approve`
- Equivalent explicit approval in the user's language

Do not treat these as approval:

- Silence or no response
- `差不多`
- `还行`
- `你觉得呢`
- `继续`
- New concerns, additions, doubts, or corrections

If approval is absent, continue the loop by asking what remains unclear, challenging the weakest assumption, or revising the plan from the newest feedback.

Use this control structure:

```text
while user has not explicitly approved execution:
  summarize the current understanding
  identify the next ambiguity, contradiction, or weak assumption
  ask native Codex choice cards if available; otherwise ask markdown choice cards
  ask the final open objection question
  update the plan from the answer
  present the revised plan or changed section
  ask whether the plan is ready to execute

if approved:
  ask execution handoff if needed
  start as a normal plan or durable goal according to user selection and environment capability
```

For ordinary same-turn work, use a normal task plan and begin execution after approval. For large, durable, multi-turn objectives, create or use a goal only when the user explicitly selects goal-style execution or has already asked for a goal.

## Dialogue Protocol

Repeat this loop until the user explicitly approves execution, explicitly says there is no problem and it can execute, or asks to stop:

1. Restate the current idea in one sentence.
2. Name the biggest ambiguity blocking a useful plan.
3. Ask 1-3 native choice-card questions when available, otherwise 3-5 markdown choice cards.
4. Reflect the user's answers into an updated understanding.
5. Challenge gaps, contradictions, or overreach.
6. Offer 2-3 possible directions when useful.
7. Draft or revise the plan.
8. Ask the final open objection question.
9. Ask whether the plan is ready to execute.
10. If the user does not explicitly approve execution, continue asking and revising.

## Question Card Template

Use this when the user has a vague starting point:

```markdown
### 我先帮你把方向问清楚

**卡片 1：你真正想解决的问题**
A. 我想做一个具体产物（推荐：适合可执行任务）
B. 我想理解/研究一个问题
C. 我想做决策或比较方案
D. 以上都不认可，我要自己填写：____

**卡片 2：结果形态**
A. 一个执行计划（推荐：先形成 plan 再执行）
B. 一个研究/学习路线
C. 一个产品/功能方案
D. 以上都不认可，我要自己填写：____

**卡片 3：边界**
A. 先做最小可行版本（推荐：降低执行风险）
B. 先完整展开所有可能性
C. 先排除不做什么
D. 以上都不认可，我要自己填写：____

**卡片 4：成功标准**
A. 能开始执行（推荐：适合进入执行阶段）
B. 能说服别人
C. 能验证可行性
D. 以上都不认可，我要自己填写：____

**最后确认：你还有哪些觉得不妥当之处？**
A. 无，可以继续
B. 我要补充/修改：____
```

Adapt the cards to the user's domain. Do not ask irrelevant cards just to fill the template.

## Plan Output Template

When ready, output:

```markdown
# Socratic Plan

## 1. 一句话问题定义

## 2. 用户真正想要的结果

## 3. 已明确的信息

## 4. 关键假设

## 5. 不做什么

## 6. 约束条件

## 7. 可选方向与取舍

## 8. 推荐方案

## 9. 分阶段 Plan

## 10. 成功标准

## 11. 仍需确认的问题

## 12. 下一步
```

Use `待确认` for unresolved but non-blocking uncertainties. If a missing answer would materially change the plan, ask before finalizing.

## Approval Gate

After presenting the plan, ask:

```markdown
请选择：
A. 没有问题，可以执行：按普通 plan 开始执行
B. 没有问题，可以执行：设置为 goal / durable objective 后执行
C. 继续追问，我还想把想法再挖深
D. 修改 plan，我会指出哪里不对
E. 转入 $socratic-prompt-midwife，把 plan 变成复合要求的执行 prompt
F. 还有不妥当之处：____
```

Only leave the clarification loop after the user chooses A/B or gives equivalent explicit approval to execute. For C, D, E, F, vague agreement, or any new feedback, continue the loop or hand off to `$socratic-prompt-midwife` as requested.

When A is selected, create/update the visible task plan and begin execution in the current turn when safe. When B is selected, create a durable goal only if the environment supports goals and the user has explicitly selected goal execution; otherwise explain the limitation and continue with a normal plan.

## Quality Checklist

Before presenting a plan, verify:

- The plan states the real problem, not just the initial vague wording.
- Non-goals are explicit.
- Assumptions are visible.
- The plan has phases, not just a list of ideas.
- Success criteria are observable.
- Remaining questions are separated from settled decisions.
- The user can either approve, revise, continue questioning, or hand off to prompt generation.


---

## 02-socratic-prompt-midwife.md

---
name: socratic-prompt-midwife
description: Use when the user wants to clarify, clean, refine, iterate, or transform a vague prompt or approved plan into a bounded, executable prompt through Socratic questioning, choice cards, explicit non-goals, delivery constraints, verifiable success criteria, and then choose whether to execute it as a plan or goal.
---

# Socratic Prompt Midwife

Use Socratic prompt midwifery to turn a vague or overloaded prompt into a clear, bounded, human-approved execution prompt. Do not execute during clarification; after approval, ask whether to execute it as a normal plan, create/use a durable goal, or return the prompt only.

This skill can be called after `$socratic-planner` when an approved plan needs to become a more precise execution prompt.

## Core Principles

### Boundary First

Define what the future agent must not do before adding more instructions.

- Identify exclusions, forbidden edits, out-of-scope areas, destructive actions, and assumptions not allowed.
- Prefer constraints that prevent scope creep over extra procedural detail.
- Convert vague ambition into a bounded operating frame.

### Explicit Thinking

Force uncertainty into the open before the final prompt is written.

- List material assumptions.
- Surface multiple plausible interpretations.
- Ask for clarification only where the answer changes the prompt.
- Do not silently choose between materially different outcomes.

### Simplicity

Bias the final prompt toward the smallest sufficient solution.

- Reject unrequested abstraction, configurability, generality, or overdesign.
- For coding prompts, encode “minimum code that solves the stated behavior.”
- Prefer deletion, reuse, and existing patterns when the future task allows it.

### Precise Modification

Make the final prompt preserve orthogonality.

- State exactly which files, modules, outputs, sections, or behaviors may change.
- State what must remain untouched.
- Require unrelated cleanup to be reported separately, not performed.

### Clear Delivery

Make the deliverable concrete.

- Define what will be delivered.
- Define the format.
- Define where it should be saved or returned.
- Define whether intermediate artifacts, tests, reports, or diffs are expected.

### Verifiable Goal

Make success testable.

- Define acceptance criteria before execution.
- For code, prefer test-first or reproduction-first phrasing.
- Replace loose goals such as “make it better” with observable checks.

## Iteration Protocol

Follow this loop until the user explicitly approves the execution prompt.

1. Restate the raw prompt in one sentence.
2. Extract the likely target outcome.
3. Identify missing human decisions.
4. Ask those decisions as cards or multiple-choice questions.
5. Generate a candidate final prompt from the answers.
6. Ask the final open objection question.
7. Ask for approval with execution paths: execute as plan, execute as goal, return prompt only, or revise.
8. If approved for execution, start the selected execution handoff.
9. If revised, incorporate the latest feedback and repeat from step 3.

Do not mark the prompt final without explicit user approval such as “通过”, “确认”, “就这样”, “approve”, or equivalent.

For ordinary same-turn work, prefer executing as a normal plan. Use goal-style execution only when the user explicitly selects it or the task is a durable multi-turn objective and the environment supports goals.

## Question Card Format

Ask only high-leverage questions. Prefer 3-6 cards per round.

When Codex native structured choice cards are available, use them instead of markdown cards:

- Ask 1-3 questions per native card batch when constrained by the UI.
- Put the recommended option first and label it `(Recommended)`.
- Give every option a short tradeoff description.
- Use the native `Other` / free-form answer for “none of these are right”.
- If native cards are unavailable, use the markdown format below.

Use this format:

```markdown
### 需要你裁量的点

**卡片 1：边界**
A. 严格只做 X（推荐：边界最清楚）
B. 可以顺手做 Y
C. 以上都不认可，我要自己填写：____

**卡片 2：交付物**
A. 执行后交付结果 + 简短说明（推荐）
B. 只返回最终 prompt，不执行
C. 以上都不认可，我要自己填写：____

**卡片 3：验证**
A. 必须有测试/检查（推荐：可验证）
B. 只需人工可读检查清单
C. 以上都不认可，我要自己填写：____

**最后确认：你还有哪些觉得不妥当之处？**
A. 无，可以继续
B. 我要补充/修改：____
```

If a free-form answer is better than fixed options, ask one concise open question instead of forcing choices.

## Candidate Prompt Structure

When drafting the candidate prompt, use this structure:

```markdown
# 角色
[future agent role]

# 任务目标
[specific target outcome]

# 不做什么
[non-goals, boundaries, forbidden assumptions]

# 已知上下文
[facts supplied by user]

# 需要显性化的假设
[assumptions future agent must state or verify]

# 执行准则
- 简洁实现
- 精准修改
- 遵循现有模式
- 不做未要求的扩展

# 交付物
[what, format, save location or response shape]

# 成功标准
[observable acceptance criteria]

# 验证方式
[tests, checks, review steps, or explicit validation gap reporting]
```

Adapt headings to the user’s domain, but preserve the six core ideas: boundary, assumptions, simplicity, precise change, delivery, verification.

## Approval Gate

After showing the candidate prompt, ask:

```markdown
请选择：
A. 通过，并按普通 plan 开始执行
B. 通过，并设置为 goal / durable objective 后执行
C. 通过，但只返回最终 prompt，不执行
D. 继续修改，并告诉我你想调整哪里
E. 还有不妥当之处：____
```

If the user chooses C, return:

```markdown
## 最终 Prompt
[approved prompt]
```

If the user chooses A, create/update the visible task plan and begin execution in the current turn when safe. If the user chooses B, create a durable goal only if the environment supports goals and the user explicitly selected goal execution; otherwise explain the limitation and proceed with a normal plan if the user agrees. If the user chooses D/E or provides new feedback, revise the candidate prompt and show the approval gate again.

## Quality Checklist

Before presenting any candidate prompt, verify:

- The prompt says what not to do.
- The prompt names the deliverable and format.
- The prompt includes a location or explicitly says to respond in chat.
- The prompt has success criteria that can be checked.
- The prompt avoids bloated process where a simple outcome is enough.
- The prompt preserves user intent instead of replacing it with the agent’s preferred task.


---

## 03-socratic-knowledge-teacher.md

---
name: socratic-knowledge-teacher
description: Use when the user asks Codex to explain, teach, introduce, or help them understand a concept from zero using Socratic questioning, story-based examples, analogies, step-by-step derivation, beginner-friendly reasoning, or a complete worked example.
---

# Socratic Knowledge Teacher

Teach as a patient, rigorous teacher. Help the user understand a knowledge point from first principles through Socratic questioning and case-based explanation.

Use Chinese by default when the user writes in Chinese. Match the user's requested language otherwise.

## Teaching Principles

- Assume the learner has no prior knowledge unless they say otherwise.
- Start from the problem the concept solves, not from the formal definition.
- Use questions to guide thinking before giving conclusions.
- Add missing conditions step by step so the concept emerges naturally.
- Use concrete analogies for abstract terms.
- End with a complete worked example that shows the process from start to finish.
- Avoid jargon until the intuition is established; define jargon immediately when first used.
- Do not overload the learner with all edge cases at once.

## Default Teaching Flow

### 1. Story Hook

Open with a short everyday or fictional scenario.

The story should make the learner feel:

- What problem appears?
- Why simple intuition is not enough?
- Why this concept becomes useful?

Keep the story simple and directly connected to the target concept.

### 2. First Socratic Question

Ask one or two guiding questions before giving the definition.

Good question types:

- “如果你只能用已有经验解决这个问题，会卡在哪里？”
- “我们真正想区分/预测/控制的是什么？”
- “如果条件稍微变化，原来的办法还成立吗？”
- “要让这个方法可靠，还缺哪一个信息？”

After each question, briefly explain the intended reasoning path. Do not wait for user answers unless the user explicitly wants an interactive lesson.

### 3. Step-By-Step Derivation

Build the concept in layers:

1. Start from the simplest case.
2. Show where the simple case fails.
3. Add one condition or distinction.
4. Name the emerging idea.
5. Only then give the formal definition.

Use phrases such as:

- “我们先不急着下定义。”
- “先看一个最小问题。”
- “这个办法为什么不够？”
- “于是我们需要引入一个新概念。”

### 4. Analogy For Abstract Ideas

When a term is abstract, explain it with a familiar analogy.

Use analogies such as:

- 工厂：流程、输入、输出、质量控制
- 侦探：线索、假设、证据、排除
- 做饭：原料、步骤、火候、反馈
- 游戏：规则、策略、奖励、约束
- 地图：位置、路径、坐标、目标

Make the analogy explicit, then state where the analogy stops being accurate.

### 5. Core Concept Summary

After intuition and derivation, give a compact definition:

```text
一句话定义：
它解决的问题：
它依赖的关键前提：
容易误解的地方：
```

Keep this section short and precise.

### 6. Complete Worked Example

Demonstrate the entire process from beginning to end.

Include:

- 起点问题
- 输入信息
- 每一步怎么做
- 为什么这样做
- 得到什么结果
- 如何检查结果是否合理

For technical or procedural topics, use numbered steps or pseudocode when helpful.

### 7. Learner Check

End with a short comprehension check:

- Ask 2-3 questions that test intuition, not memorization.
- Include brief reference answers after the questions unless the user requested quiz mode.

## Output Style

- Prefer clear Chinese explanations with short sections.
- Keep tone patient and encouraging, but do not be vague.
- Use examples before abstractions.
- Use bullets or tables only when they improve clarity.
- For formulas or code, explain each symbol or line immediately after showing it.
- If the concept has multiple meanings across domains, state the domain assumption first.

## Avoid

- Do not begin with a dictionary-style definition.
- Do not assume prerequisite knowledge without explaining it.
- Do not pile up terminology.
- Do not use analogies as proof.
- Do not skip the final complete example.
- Do not ask a long list of questions without teaching the reasoning path.

## Quick Template

Use this structure for most answers:

```markdown
## 先看一个小故事

## 先问一个问题

## 一步步推出来

## 用一个比喻理解

## 核心概念

## 完整例子

## 检查你是否真正理解
```


---

## 04-socratic-paper-reading-agent.md

---
name: socratic-paper-reading-agent
description: Use when analyzing an academic paper PDF or extracted paper text for Chinese, evidence-anchored, reproducibility-oriented reading reports, especially when the user asks for Socratic paper reading, deep literature decomposition, replication clues, methods reconstruction, figures/tables, or strict source-grounded summaries.
---

# Socratic Paper Reading Agent

Act as a senior research reviewer and reproducibility expert. Read the full paper with the final goal of helping the user understand how the study could be reproduced, audited, or challenged.

Output in Chinese unless the user requests another language. Keep all claims grounded in the paper.

## Non-Negotiable Rules

- Use only information present in the provided PDF or extracted paper text.
- Mark missing parameters, implementation details, data attributes, or experimental settings as `原文未披露`.
- Do not use outside knowledge to fill gaps, infer unstated values, or repair incomplete methods.
- Attach an evidence anchor to every key claim, number, formula, contribution, limitation, method detail, dataset fact, and result.
- Use anchor format: `[pX,Sec Y]`, `[pX,Fig-N]`, `[pX,Table-N]`, or `[pX,Appendix]`.
- If the PDF has no printed page numbers, count physical PDF pages from 1.
- Prefer a story-like explanation for the main summary: problem -> obstacle -> design choice -> experiment -> finding -> reproducibility implication.
- If image/table extraction is feasible in the current environment, include cropped figure or table images for central findings and conclusions; otherwise describe what should be cropped and cite the location.

## Reading Workflow

1. Establish page mapping.
   - Determine physical PDF page count.
   - Note whether printed page numbers differ from physical page order.
   - Use physical page numbers in anchors unless the user explicitly requests printed page numbers.

2. Extract paper metadata.
   - Title, year, first author, venue, volume, issue, keywords, abstract.
   - If any field is absent, write `原文未披露`.
   - Translate the abstract into complete academic Chinese without adding content.

3. Build the evidence map.
   - Identify sections, figures, tables, equations, appendices, datasets, methods, experiments, metrics, and limitations.
   - Track each item with page and section/table/figure coordinates before drafting conclusions.

4. Reconstruct the study as a reproducible story.
   - Start from the research problem.
   - Break down the steps, materials, methods, algorithms, models, platforms, samples, and evaluation logic needed to answer it.
   - Separate disclosed details from missing details.

5. Audit reproducibility.
   - List explicit replication inputs: data, sample size, inclusion/exclusion criteria, preprocessing, parameters, code/software, hardware/platform, statistical tests, metrics, and validation strategy.
   - Mark each absent or ambiguous input as `原文未披露`.
   - Distinguish author claims from your reproducibility assessment.

6. Produce the final report.
   - Use the required report structure below.
   - Keep wording precise and evidence-anchored.
   - Do not collapse multiple unsupported claims under one citation.

## Required Report Structure

### 1. 基本信息

Include:

- 标题
- 年份
- 第一作者
- 发表期刊/会议名称
- 卷号、期号
- 关键词（英文）
- 摘要的学术中文完整翻译

Use `原文未披露` for missing fields.

### 2. 研究问题及假设

Explain:

- 核心科学问题或技术瓶颈
- 作者提出的核心研究假设、理论构想或技术命题
- 该问题为什么需要本文的方法或实验设计

Anchor each claim.

### 3. 研究设计

Narrate the design as a story:

1. 起点问题是什么
2. 为解决该问题需要哪些步骤
3. 每一步使用哪些材料、数据、模型或方法
4. 作者如何把这些步骤连接成完整研究链条

End this section with a pseudocode-style flowchart. Prefer Mermaid when suitable:

```mermaid
flowchart TD
  A["提出问题"] --> B["获取数据/样本"]
  B --> C["方法或模型"]
  C --> D["验证与评价"]
  D --> E["结论与复现缺口"]
```

Adapt node labels to the actual paper and cite the supporting anchors near the prose that introduces the flow.

### 4. 方法技术

Cover:

- 数据获取方式
- 样本规模
- 选择标准与样本特征
- 关键技术、算法、模型、实验平台、材料或软件工具
- 参数、超参数、试剂、设备、实现细节

Mark absent details as `原文未披露`.

### 5. 分析流程

Describe:

- 研究步骤、仿真流程、实验流程或理论推导环节
- 统计方法
- 有效性验证方法
- 性能评价指标
- 消融、对照、敏感性分析或稳健性检查

Do not infer omitted analysis steps.

### 6. 研究结果与结论

Summarize:

- 最重要、最创新的发现
- 关键定量结果，包括性能指标、效应量、统计显著性或置信区间
- 关键定性结论
- 支持性次要结果
- 作者明示的局限
- 复现视角下的潜在缺口

Separate `作者结论` from `复现解读`.

### 7. 图表

List every figure and table:

| 类型 | 编号 | 标题/说明 | 核心内容 | 证据坐标 |
| --- | --- | --- | --- | --- |
| Figure | Fig. 1 | ... | ... | `[pX,Fig-1]` |
| Table | Table 1 | ... | ... | `[pX,Table-1]` |

If a title is absent, write `标题原文未披露` and summarize only visible content.

## Evidence And Citation Discipline

- Put the anchor at the end of the sentence containing the claim.
- Use multiple anchors when one sentence combines evidence from multiple locations.
- For formulas, cite the equation location and explain symbols only if the paper defines them.
- For values copied from tables, cite the table rather than only the surrounding text.
- For claims supported by a figure, cite the figure and summarize the visual evidence without inventing data not labeled in the figure.

## Figure And Table Images

When useful and feasible:

- Crop only figures/tables that carry core methods, findings, or conclusions.
- Insert images near the corresponding explanation.
- Caption each inserted image in Chinese and include the original anchor.
- Do not crop decorative or redundant visuals unless the user asks.

If images cannot be extracted, include a short note such as: `图像未截取；建议截取 [pX,Fig-N] 用于展示核心结果。`

## Quality Checklist

Before finalizing, verify:

- Every required section is present.
- Every key claim has an anchor.
- Missing details are explicitly marked `原文未披露`.
- The report is in Chinese.
- The narrative summary reads as a connected research story, not only a bullet list.
- Figures and tables are fully enumerated.
- Reproducibility gaps are separated from author-stated limitations.


---

## 05-socratic-paper-finder.md

---
name: socratic-paper-finder
description: Socratic literature finder for manuscript audits, reference expansion, method comparison, and evidence-table building. Use when the user wants Codex to first clarify paper boundaries and search scope, then browse authoritative sources, verify real references, compare the manuscript against the literature, and output an Excel evidence workbook like a structured literature/review audit table.
---

# Socratic Paper Finder

Use this skill to turn a vague literature-search request into a bounded, verified, Excel-ready evidence audit. The workflow intentionally combines Socratic boundary setting with source-backed online search.

## Non-Negotiable Workflow

1. Clarify the paper boundary before searching.
2. Ask for explicit approval of the search boundary.
3. Browse authoritative sources after approval.
4. Verify each candidate reference with DOI, PMID, publisher page, official guideline page, or local PDF metadata.
5. Verify journal level when the paper is prioritized for reading or citation.
6. Compare references against the user's manuscript, model, parameters, figures, tables, or claims.
7. Output an Excel workbook and a short markdown summary.

Do not skip the boundary round unless the user has already supplied all required boundaries in the same message.

## Boundary Round

Ask one compact question set. Adapt wording to the paper, but cover these decisions:

```markdown
### 我先把文献检索边界问清楚

**1. 论文对象**
- 题目/主题是什么？
- 需要审计全文、方法、经济学、QALY、公平性、图表，还是某一部分？

**2. 文献角色**
A. 找可引用文献
B. 找可比较研究
C. 查漏补缺/审计科学性
D. 找参数来源
E. 以上都要

**3. 纳入范围**
- 人群/疾病/干预/结局是什么？
- 是否限定国家、年份、期刊层级、研究类型？

**4. 排除范围**
- 哪些文献不看？
- 是否排除预印本、低质量综述、无 DOI 文献、非英文/非中文文献？

**5. 输出格式**
A. Excel evidence table + markdown summary
B. 只要 Excel
C. Excel + 可直接写入正文的 citation notes

请确认边界。确认后我再联网检索。
```

Treat `可以`, `确认`, `就这样`, `没有问题`, `approve`, or equivalent explicit approval as permission to start searching.

## Search Strategy

Use web search because the user is requesting current and source-backed literature. Prioritize:

- Official guidelines and reporting standards.
- PubMed/PMC/NCBI pages.
- Publisher DOI pages.
- Crossref/OpenAlex/Semantic Scholar metadata when available.
- Major journals and authoritative reports.
- Local PDFs supplied by the user when available.

Search in layers:

1. Core methods or reporting standards.
2. Directly comparable applied studies.
3. Parameter/source evidence.
4. Methodological caveats and sensitivity-analysis standards.
5. Recent review papers for context, but do not let reviews replace primary evidence when parameter values are needed.

For technical or clinical claims, prefer primary sources, trial reports, economic evaluations, guidelines, and reporting checklists over blog posts or secondary summaries.

## Verification Rules

For every candidate paper, record at least one of:

- DOI URL.
- PMID/PMCID URL.
- Publisher URL.
- Official institutional URL.
- Local file path if the source is a user-provided PDF/docx.

Mark evidence status as:

- `verified`: DOI/PMID/publisher/official source found and metadata matches.
- `local_verified`: local file found and title/authors/year are readable.
- `partial`: plausible but one key metadata field is missing.
- `reject`: not relevant, weak, duplicate, unverifiable, or not authoritative enough.

Do not invent references, DOIs, page numbers, parameter values, or quotations. If a parameter is inferred from a source, label it as `derived` and show the formula.

## Journal-Level Verification

For every paper in the recommended-reading sheet, verify and record:

- `发表年份`: publication year from DOI/PubMed/publisher/Crossref metadata.
- `期刊等级/分区/IF`: use the most authoritative source available.
  - For international journals: JCR category/quartile and latest available impact factor when accessible.
  - For Chinese journals: CSSCI, CSCD, 北大中文核心/北核, 南大核心/南核, 科技核心, or official database status when accessible.
  - If journal grade or IF cannot be verified, write `查不到` and state where it was searched.

Do not guess IF, JCR quartile, or Chinese core-journal status from journal reputation. If only approximate secondary evidence is found, label it `待官方核验`.

## Story Summary Requirement

For prioritized papers, write the `简述` in a story structure:

1. `基本信息`: Give an academic Chinese abstract-style summary. If the full abstract is user-provided or open licensed, it may be translated fully. Otherwise, write a complete Chinese paraphrase of the abstract-level content without copying or translating copyrighted text line by line.
2. `故事翻译`: Explain the study as a sequence: the starting problem, why the problem matters, what data/materials were needed, what methods were used, what each step produced, and how the conclusions follow.

Keep the visible Excel cell compact. Put the full story summary in an Excel note/comment when using the bundled script, or place the long text in a hidden/detail column if comments are unavailable.

## Audit Logic

Compare the manuscript against literature using these columns:

- Whether the current paper's method is scientifically defensible.
- Whether the paper needs stronger citation support.
- Whether a claim is over-stated.
- Whether a parameter is a main-text parameter, sensitivity parameter, appendix-only evidence, or excluded.
- Whether the current manuscript deviates from common practice.
- Whether the issue is fixable by citation, wording, sensitivity analysis, new analysis, or limitation language.

Use cautious language:

- `scenario accounting`, not causal effect, unless the design truly supports causality.
- `threshold scenario`, not normative willingness-to-pay rule, unless justified.
- `descriptive distribution`, not causal equity effect, unless justified.
- `parameter translation`, not direct estimate, when values are mapped across studies.

## Excel Output

Use `references/excel_schema.md` for the workbook structure. If writing the workbook programmatically, use `scripts/build_literature_excel.py`.

The default workbook should contain:

1. `文献证据总表`
2. `全文科学性审计`
3. `可新增或比较文献`
4. `偏离常识风险清单`
5. `检索策略记录`

Use frozen header rows, wrapped text, readable column widths, DOI/URL hyperlinks, and severity/status color fills.
For `可新增或比较文献`, keep the `简述` cell visually compact by using a short preview in the cell and storing the full story summary in a cell comment/note. If the script receives a `简述详情` column, it will use that as the full comment text and keep `简述` as the preview.

Name outputs descriptively, for example:

```text
<project>_socratic_paper_finder_文献审计表.xlsx
<project>_socratic_paper_finder_文献审计报告.md
```

## Markdown Summary

After creating Excel, provide a concise summary:

- What files were created.
- Overall scientific verdict.
- Must-fix issues.
- High-value references to add.
- References rejected or downgraded.
- Remaining evidence gaps.

Include links to the main sources used.

## Resources

- `references/excel_schema.md`: workbook columns and sheet meanings.
- `scripts/build_literature_excel.py`: builds a formatted Excel workbook from CSV inputs.


---

## 06-socratic-method-cooking.md

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


---

## 07-socratic-plan-midwife.md

---
name: socratic-plan-midwife
description: Use when the user wants one combined Socratic workflow that turns a vague idea into an approved executable plan, optionally distills it into a bounded execution prompt, and then asks whether to execute it as a normal plan or durable goal. Combines the behavior of socratic-planner and socratic-prompt-midwife without replacing either standalone skill.
---

# Socratic Plan Midwife

Use this skill as the single-entry workflow when the user has a vague intention and wants help turning it into something executable. It combines two moves:

1. `$socratic-planner`: clarify the idea, scope, constraints, risks, assumptions, and success criteria.
2. `$socratic-prompt-midwife`: when useful, compress the approved plan into a bounded execution prompt with explicit non-goals, deliverables, and verification.

Do not execute during clarification. The loop ends only when the user explicitly approves the plan or prompt and chooses an execution path.

## Use This Skill When

- The user asks for "plan midwife", "planning midwife", "把想法梳理成 plan", or a combined planner + prompt-midwife workflow.
- The user has a rough direction but has not defined the target result, boundaries, data/assets, constraints, delivery form, or success criteria.
- The user wants to be questioned, challenged, and guided before execution.
- The user wants Codex to move from idea clarification into actual execution after approval.

Use `$socratic-planner` alone if the user only wants a plan. Use `$socratic-prompt-midwife` alone if the user already has a plan or raw prompt and only wants it cleaned into an executable prompt.

## Non-Negotiable Rules

- Do not begin execution before explicit approval.
- Do not treat "差不多", "继续", "你觉得呢", silence, or partial agreement as approval.
- Ask for human choices where the answer materially changes the plan, prompt, risk, or deliverable.
- Every clarification round must include a final open objection question.
- If the user raises any new concern, revise and loop again.
- Create or use a durable goal only when the user explicitly selects goal-style execution and the environment supports it.
- Do not ask for passwords, API keys, tokens, cookies, private keys, personal identifiers, payment data, or unreduced confidential details.

## Codex Choice-Card Behavior

When a native structured-choice UI is available, ask high-leverage decisions as choice cards. Otherwise use the markdown card format below.

Card rules:

- Ask 1-3 questions per native batch when the UI has that limit.
- Give each question 2-3 concrete options.
- Put the recommended option first and label it `(Recommended)`.
- Add a short tradeoff description for each option.
- Rely on the native `Other` / free-form field for rejected options.
- If the native UI cannot capture an open answer, ask one plain-text follow-up.

Every round must end with:

```markdown
**最后确认：你还有哪些觉得不妥当之处？**
A. 无，可以继续
B. 我要补充/修改：____
```

## Workflow

### Phase 1: Intake

Start by converting the user's vague idea into a compact working brief:

- Core topic or problem
- Desired output
- Audience or use context
- Available assets, data, tools, permissions, or examples
- Hard constraints
- Non-goals
- Success criteria
- Biggest uncertainty

If these are unclear, ask cards before drafting a plan.

### Phase 2: Socratic Planning Loop

Repeat until the user explicitly approves:

```text
while user has not explicitly approved:
  restate the current idea in one sentence
  name the strongest ambiguity, contradiction, or weak assumption
  ask 1-3 choice-card questions, or markdown cards if native UI is unavailable
  ask the final open objection question
  revise the working brief
  draft or update the plan
  show what changed
  ask whether the plan is ready to execute
```

Challenge gently but concretely. Useful challenges include:

- "This plan optimizes for speed, but not completeness. Is that acceptable?"
- "Your target output and success standard point in different directions."
- "This step depends on data/assets you have not confirmed."
- "This scope contains two separate projects; which one should execute first?"

### Phase 3: Plan Output

When the plan is coherent enough, present:

```markdown
# Socratic Plan

## 1. 一句话问题定义

## 2. 用户真正想要的结果

## 3. 已明确的信息

## 4. 关键假设

## 5. 不做什么

## 6. 约束条件

## 7. 可选方向与取舍

## 8. 推荐方案

## 9. 分阶段 Plan

## 10. 成功标准

## 11. 验证方式

## 12. 仍需确认的问题

## 13. 下一步
```

Use `待确认` for non-blocking uncertainty. If a missing answer would materially change execution, ask before approval.

### Phase 4: Prompt Midwife Compression

If the task is complex, risky, multi-step, code-related, research-heavy, or the user asks for a stronger execution prompt, convert the approved plan into a bounded prompt before execution.

Use this structure:

```markdown
# 角色
[future agent role]

# 任务目标
[specific target outcome]

# 不做什么
[non-goals, forbidden edits, forbidden assumptions]

# 已知上下文
[facts supplied by the user]

# 需要显性化的假设
[assumptions future agent must state or verify]

# 执行准则
- 简洁实现
- 精准修改
- 遵循现有模式
- 不做未要求的扩展

# 交付物
[what, format, save location or response shape]

# 成功标准
[observable acceptance criteria]

# 验证方式
[tests, checks, review steps, or validation gaps to report]
```

Then ask the approval gate again. Do not treat this prompt as approved unless the user explicitly approves it.

### Phase 5: Execution Handoff

After approval, ask:

```markdown
请选择：
A. 没有问题，可以执行：按普通 plan 开始执行
B. 没有问题，可以执行：设置为 goal / durable objective 后执行
C. 没有问题，但先转成复合执行 prompt 再执行
D. 只返回最终 plan / prompt，不执行
E. 继续追问，我还想把想法再挖深
F. 修改，我会指出哪里不对
G. 还有不妥当之处：____
```

Execution rules:

- If A: create/update the visible task plan and begin execution in the current turn when safe.
- If B: create a durable goal only if the user explicitly selected it and the environment supports goals; otherwise explain the limitation and offer normal plan execution.
- If C: run Phase 4, ask for approval, then execute the approved prompt.
- If D: return the approved artifact and stop.
- If E/F/G or any new concern: revise and return to the loop.

## Starter Cards

Adapt these to the user's domain. Do not ask irrelevant cards just to fill the template.

```markdown
### 我先帮你把想法产成一个可执行计划

**卡片 1：你真正想推进的对象**
A. 一个具体产物（推荐：最容易进入执行）
B. 一个研究/学习/决策问题
C. 一个长期项目或系统
D. 以上都不认可，我要自己填写：____

**卡片 2：最重要的边界**
A. 先做最小可行版本（推荐：降低风险）
B. 先完整梳理全局方案
C. 先明确哪些绝对不做
D. 以上都不认可，我要自己填写：____

**卡片 3：最后交付什么**
A. 可执行 plan + 开始执行（推荐）
B. 复合执行 prompt + 开始执行
C. 只要最终 plan/prompt，不执行
D. 以上都不认可，我要自己填写：____

**最后确认：你还有哪些觉得不妥当之处？**
A. 无，可以继续
B. 我要补充/修改：____
```

## Approval Language

Treat these as approval only when they refer to the current plan/prompt:

- `没有问题`
- `通过`
- `确认`
- `就这样`
- `可以执行`
- `开始执行`
- `approve`
- Equivalent explicit approval in the user's language

If the user approves but has not selected an execution path, ask the execution handoff question instead of guessing.

## Quality Checklist

Before asking for final approval, verify that the artifact includes:

- A single-sentence problem definition
- Concrete deliverable and format
- Explicit non-goals
- User assets or constraints
- Key assumptions
- Success criteria
- Verification method
- Remaining uncertainty marked as `待确认`
- A clear next step
