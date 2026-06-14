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
