# Socratic Codex Skills

`Socratic Codex Skills` is a small suite of Codex skills built around Socratic questioning, explicit boundaries, evidence, and human approval before execution.

`Socratic Codex Skills` 是一组面向 Codex 的苏格拉底式 skill 套件。它们的共同目标不是让 AI 更快地“替你下结论”，而是让 AI 先学会追问、澄清边界、暴露假设、建立证据，再在用户明确认可后进入执行。

## 一句话概览 / One-Line Overview

| 中文 | English |
| --- | --- |
| 当你的想法还很模糊时，这套 skill 会像一位严格但耐心的合作者：先问清楚问题，再整理成计划、提示词、文献线索、方法流或教学解释。 | When your idea is still vague, this suite acts like a strict but patient collaborator: it clarifies the problem before turning it into a plan, prompt, literature trail, methodology flow, or teaching explanation. |

## 包含哪些 skill / Included Skills

| Skill | 中文用途 | English purpose |
| --- | --- | --- |
| `$socratic-planner` | 用选择题卡片和追问，把模糊想法梳理成可执行 plan；循环到用户明确认可才结束。 | Turns vague ideas into executable plans through choice cards and Socratic iteration, stopping only after explicit approval. |
| `$socratic-prompt-midwife` | 把模糊 prompt 或已认可的 plan 清洗成边界清楚、交付明确、可验证的执行 prompt。 | Cleans vague prompts or approved plans into bounded, deliverable-specific, verifiable execution prompts. |
| `$socratic-plan-midwife` | 独立整合 planner 和 prompt midwife：从模糊想法到 plan，再可选压缩成执行 prompt，最后选择 plan/goal 执行。 | A combined workflow: vague idea to plan, optional prompt compression, then normal plan or durable goal execution. |
| `$socratic-knowledge-teacher` | 用故事、提问、类比和完整例子，从零基础讲解一个知识点。 | Teaches a concept from first principles using story, questions, analogies, and a complete worked example. |
| `$socratic-paper-reading-agent` | 面向复现研究阅读论文 PDF，输出中文、证据锚定、可复现线索导向的深度报告。 | Reads academic PDFs for Chinese, evidence-anchored, reproducibility-focused analysis reports. |
| `$socratic-paper-finder` | 先澄清检索边界，再联网查找和核验文献，形成结构化证据表。 | Clarifies literature-search boundaries, verifies papers online, and builds structured evidence tables. |
| `$socratic-method-cooking` | 针对实证论文主题，先明确核心主题和数据资产，再循证寻找 gap，并匹配传统或组合创新的方法流。 | For empirical-paper ideas, clarifies theme and data assets, finds evidence-backed gaps, and matches conventional or recombined methodology flows. |

## 命名说明 / Naming Note

| 中文 | English |
| --- | --- |
| `$socratic-planner` 没有被改名。它仍然是独立的规划器，负责通过循环提问把模糊想法整理成可执行 plan。 | `$socratic-planner` has not been renamed. It remains the standalone planner that turns vague ideas into executable plans through iterative questioning. |
| `$socratic-plan-midwife` 是另一个独立 skill。它把 planner 与 prompt midwife 的能力合并起来，适合从模糊想法一路推进到 plan、执行 prompt，并在用户确认后进入 plan 或 goal 执行。 | `$socratic-plan-midwife` is a separate skill. It combines the planner and prompt midwife workflows, moving from vague idea to plan, execution prompt, and then plan or goal execution after user approval. |
| 简单说：planner 是“先把事情想清楚”，plan midwife 是“从想清楚到准备执行的一体化产婆”。 | In short: planner helps clarify the work; plan midwife carries the clarified idea all the way toward execution readiness. |

## 目录结构 / Repository Structure

```text
dist/
  codex/
    skills/
      socratic-planner/
        SKILL.md
        agents/openai.yaml
      socratic-prompt-midwife/
        SKILL.md
        agents/openai.yaml
      socratic-plan-midwife/
        SKILL.md
        agents/openai.yaml
      socratic-knowledge-teacher/
        SKILL.md
        agents/openai.yaml
      socratic-paper-reading-agent/
        SKILL.md
        agents/openai.yaml
      socratic-paper-finder/
        SKILL.md
        agents/openai.yaml
        references/excel_schema.md
        scripts/build_literature_excel.py
      socratic-method-cooking/
        SKILL.md
        agents/openai.yaml
  markdown/
    01-socratic-planner.md
    02-socratic-prompt-midwife.md
    03-socratic-knowledge-teacher.md
    04-socratic-paper-reading-agent.md
    05-socratic-paper-finder.md
    06-socratic-method-cooking.md
    07-socratic-plan-midwife.md
```

`dist/codex/skills/*` is the recommended Codex flat-suite install layout.

`dist/codex/skills/*` 是推荐的 Codex 扁平 suite 安装布局。

## 安装方式 / Installation

Copy all skills into your Codex skills directory:

把所有 skill 复制到 Codex 的 skills 目录：

```bash
cp -R dist/codex/skills/* ~/.codex/skills/
```

Or install one skill at a time:

也可以单独安装某一个：

```bash
cp -R dist/codex/skills/socratic-plan-midwife ~/.codex/skills/
```

Then invoke a skill in Codex:

然后在 Codex 中调用：

```text
$socratic-plan-midwife
```

## 验证方式 / Validation

If your Codex installation includes `skill-creator`, validate a skill with:

如果你的 Codex 已安装 `skill-creator`，可以这样校验：

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ~/.codex/skills/socratic-plan-midwife
```

Expected result:

```text
Skill is valid!
```

## 使用建议 / Suggested Workflow

| 中文 | English |
| --- | --- |
| 如果你只有一个方向，还不知道该做什么，先用 `$socratic-plan-midwife`。它会问你，直到形成可执行 plan 或 prompt。 | If you only have a direction and do not know what to do yet, start with `$socratic-plan-midwife`. It asks until an executable plan or prompt emerges. |
| 如果你已经有初步需求，只是 prompt 很乱，用 `$socratic-prompt-midwife`。 | If you already have rough requirements but the prompt is messy, use `$socratic-prompt-midwife`. |
| 如果你在读论文，用 `$socratic-paper-reading-agent`。 | If you are reading a paper, use `$socratic-paper-reading-agent`. |
| 如果你要找文献证据，用 `$socratic-paper-finder`。 | If you need literature evidence, use `$socratic-paper-finder`. |
| 如果你要把实证论文想法变成 gap 和方法流，用 `$socratic-method-cooking`。 | If you want to turn an empirical-paper idea into gaps and methodology flows, use `$socratic-method-cooking`. |

## 安全与隐私复查 / Security And Privacy Review

| 中文 | English |
| --- | --- |
| 本仓库主体是 Markdown 指令文件和 Codex UI 元信息。唯一的脚本是 `socratic-paper-finder/scripts/build_literature_excel.py`，用于把本地 CSV 整理成 Excel 工作簿；脚本不联网、不读取环境变量、不处理凭证。 | The repository is mainly Markdown instructions and Codex UI metadata. The only script is `socratic-paper-finder/scripts/build_literature_excel.py`, which turns local CSV files into an Excel workbook; it does not access the network, read environment variables, or handle credentials. |
| 仓库中没有 API key、token、cookie、私钥、账户、论文 PDF、聊天记录、`.omx` 日志或本地环境配置。 | It contains no API keys, tokens, cookies, private keys, accounts, paper PDFs, chat logs, `.omx` logs, or local environment configuration. |
| 大多数 skill 是纯对话工作流，不会自行联网。`socratic-paper-finder` 和 `socratic-method-cooking` 会在用户明确需要文献检索时要求 Codex 使用在线来源；这属于用户发起的检索工作流，不是 skill 自带的隐藏网络行为。 | Most skills are dialogue-only workflows and do not access the network by themselves. `socratic-paper-finder` and `socratic-method-cooking` ask Codex to use online sources when the user explicitly needs literature search; this is user-initiated retrieval, not hidden network behavior embedded in the skill. |
| 主要风险不是代码攻击，而是用户在对话中主动粘贴敏感信息。因此多个 skill 都写入了隐私护栏：不要提供密码、密钥、内部 URL、身份信息或不可公开数据；需要时只提供脱敏摘要。 | The main risk is not code-level attack, but a user voluntarily pasting sensitive information into a conversation. The skills therefore include privacy guardrails: do not provide passwords, keys, internal URLs, identity information, or non-public data; use redacted summaries when needed. |

## License / 许可证

No license has been added yet.

暂未添加许可证。
