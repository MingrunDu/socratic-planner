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
