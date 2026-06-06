# Socratic Planner

## 中文介绍

`Socratic Planner` 是一个面向 Codex 的苏格拉底式规划 skill，用来把模糊想法、粗略方向、早期项目构想或不清晰的问题，逐步梳理成结构化的问题定义和可执行计划。

它不会直接执行任务，也不会直接生成最终 prompt。它的职责是通过提问、回应、辩论和迭代，帮助用户澄清：

- 真正要解决的问题是什么
- 用户想要的结果是什么
- 哪些信息已经明确
- 哪些是假设
- 哪些事情明确不做
- 有哪些约束和取舍
- 应该采用什么分阶段 plan
- 成功标准如何验证

核心机制是一个强制迭代循环：只有当用户明确表示“没有问题”“通过”“确认”“就这样”“可以”或等价表达时，规划循环才结束。否则，skill 会继续追问、指出弱假设、修订 plan，并再次请求确认。

适合场景：

- “我有个想法，但还没想清楚”
- “帮我把这个项目方向梳理成计划”
- “我想做一个东西，但不知道怎么拆解”
- “先不要执行，先问我问题，把需求问完整”
- “把模糊研究/产品/学习/工作流问题整理成 plan”

和 `$socratic-prompt-midwife` 的关系：

- `$socratic-planner`：把模糊想法整理成完整 plan
- `$socratic-prompt-midwife`：把已成形的 plan 转成可执行 prompt

## English Introduction

`Socratic Planner` is a Codex skill for turning vague ideas, rough directions, early project concepts, or unclear problems into structured problem definitions and actionable plans.

It does not execute the task and does not directly produce a final execution prompt. Its job is to clarify the user's intent through Socratic questioning, reflection, challenge, and iteration.

It helps clarify:

- The real problem to solve
- The user's desired outcome
- What is already known
- What remains an assumption
- Explicit non-goals
- Constraints and tradeoffs
- A phased plan
- Observable success criteria

Its core mechanism is a mandatory iteration loop: the planning process ends only when the user explicitly approves the plan, for example by saying “no problem,” “approved,” “confirmed,” or an equivalent phrase. Otherwise, the skill continues asking questions, challenging weak assumptions, revising the plan, and requesting approval again.

Use it when the user says things like:

- “I have an idea but it is still vague.”
- “Help me organize this project direction into a plan.”
- “I want to build something but do not know how to break it down.”
- “Do not execute yet; ask me questions until the requirement is clear.”
- “Turn this vague research/product/learning/workflow idea into a plan.”

Relationship with `$socratic-prompt-midwife`:

- `$socratic-planner`: turns a vague idea into a complete plan
- `$socratic-prompt-midwife`: turns an approved plan into an executable prompt

## Installation

Copy the skill folder into your Codex skills directory:

```bash
cp -R socratic-planner ~/.codex/skills/
```

Then invoke it in Codex:

```text
$socratic-planner
```

## Repository Structure

```text
socratic-planner/
  SKILL.md
  agents/
    openai.yaml
```

## Validation

Validate with Codex's skill validator:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ~/.codex/skills/socratic-planner
```

Expected result:

```text
Skill is valid!
```
