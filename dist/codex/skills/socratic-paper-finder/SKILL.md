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
