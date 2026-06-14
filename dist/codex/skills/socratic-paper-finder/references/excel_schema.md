# Socratic Paper Finder Excel Schema

Use this schema when the user asks for a literature audit workbook.

## Sheet 1: 文献证据总表

Purpose: all candidate sources, including accepted, appendix-only, and rejected papers.

Required columns:

- `模块`: manuscript area, e.g. introduction, methods, QALY, cost, equity, reporting standard.
- `文献标题`
- `作者年份`
- `期刊/机构`
- `文献类型`: guideline, trial, model, economic evaluation, systematic review, method paper, report.
- `研究对象/场景`
- `关键结果或参数`
- `与本文关系`: main citation, comparison, parameter source, sensitivity, limitation, reject.
- `证据状态`: verified, local_verified, partial, reject.
- `DOI/PMID/URL`
- `本地文件路径`
- `备注`

## Sheet 2: 全文科学性审计

Purpose: line-by-line or module-by-module assessment of whether the manuscript is scientifically defensible.

Required columns:

- `模块`
- `全文当前做法`
- `可比较/可引用文献`
- `科学性判断`
- `潜在风险/常识偏离`
- `优化建议`
- `优先级`: high, medium, low.
- `建议处理`: keep, revise wording, add citation, add sensitivity, appendix only, remove.

## Sheet 3: 可新增或比较文献

Purpose: prioritized recommended reading list and references most useful for manuscript revision.

Required columns:

- `推荐顺位`
- `文献标题`
- `发表年份`
- `作者年份`
- `期刊`
- `期刊等级/分区/IF`: JCR quartile and impact factor for international journals; CSSCI/CSCD/北核/南核/科技核心 for Chinese journals; write `查不到` when not verified.
- `为什么适合本文`
- `建议引用位置`
- `简述`: compact visible preview. Store the full story summary in the cell comment when using the bundled script.
- `DOI/PMID/URL`
- `证据状态`

Optional columns:

- `简述详情`: full story summary placed into the `简述` cell comment/note by the bundled script.
- `期刊等级来源`: official JCR, journal website, CNKI/Wanfang/CSSCI/CSCD, or other source used to verify the journal grade.

`简述详情` should follow this structure:

```text
【基本信息】
用学术中文完整转述摘要层面的研究目的、设计、数据、主要结果和结论。若摘要由用户提供或具有开放许可，可完整翻译；否则不要逐句复制/翻译受版权保护的摘要。

【故事翻译】
Step 1: 从什么问题出发？
Step 2: 为解决问题需要哪些材料、数据或人群？
Step 3: 用了哪些方法？
Step 4: 得到了什么核心发现？
Step 5: 这篇文献如何帮助当前论文？
```

## Sheet 4: 偏离常识风险清单

Purpose: issues a reviewer may challenge even if the math is internally consistent.

Required columns:

- `风险点`
- `为什么可能被质疑`
- `如何修正或解释`
- `严重性`: high, medium, low.

## Sheet 5: 检索策略记录

Purpose: reproducibility record for the literature search.

Required columns:

- `检索时间`
- `数据库/来源`
- `检索式或关键词`
- `筛选规则`
- `命中数量`
- `纳入数量`
- `备注`

## Formatting Expectations

- Freeze the first row.
- Use wrapped text and vertical top alignment.
- Hyperlink DOI/URL fields.
- Use color fills only for status/severity, not decorative color.
- Keep one reference per row.
- Keep formulas visible in notes when a parameter is derived.
- Keep `简述` rows compact. Prefer Excel comments/notes for long story summaries instead of increasing row height.
