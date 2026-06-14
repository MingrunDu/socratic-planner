# Security Notes

## 中文

这个仓库是一个 Codex skill 指令包，不是软件运行时。

已检查的安全边界：

- 不包含二进制文件。
- 不包含依赖安装逻辑。
- 不包含 API key、token、cookie、私钥、账户信息或本地配置。
- 不包含论文 PDF、用户数据、聊天日志、`.omx` 运行日志或临时缓存。
- 大部分 skill 目录只有 `SKILL.md` 和 `agents/openai.yaml`。
- `socratic-paper-finder` 额外包含一个本地 Excel 生成脚本：`scripts/build_literature_excel.py`。该脚本只读取本地 CSV 并写出 `.xlsx`，不联网、不调用 shell、不读取环境变量、不处理凭证。

使用时仍需注意：

- 不要把密码、密钥、内部系统地址、身份证件、银行卡、未脱敏数据贴给 AI。
- 需要文献检索的 skill 可能会让 Codex 访问公开网页或学术数据库；请先确认检索主题可以公开。
- 如果你的研究项目、数据资产或商业计划敏感，请只提供脱敏摘要和可公开讨论的边界。

## English

This repository is a Codex skill instruction pack, not a software runtime.

Reviewed security boundaries:

- No binaries.
- No dependency-install logic.
- No API keys, tokens, cookies, private keys, account details, or local configuration.
- No paper PDFs, user datasets, chat logs, `.omx` runtime logs, or temporary cache files.
- Most skill folders contain only `SKILL.md` and `agents/openai.yaml`.
- `socratic-paper-finder` additionally includes one local Excel formatter script: `scripts/build_literature_excel.py`. It reads local CSV files and writes `.xlsx`; it does not access the network, call the shell, read environment variables, or handle credentials.

Usage cautions:

- Do not paste passwords, keys, internal system URLs, identity documents, payment details, or unredacted private data into AI conversations.
- Literature-search skills may ask Codex to access public web pages or academic databases when the user requests evidence retrieval; confirm the search topic is safe to disclose.
- For sensitive research projects, data assets, or business plans, provide only redacted summaries and public-safe boundaries.
