---
name: veri-analitigi
description: Veri analitiği yetkinliği - (1) web üzerinde kaynak belirterek araştırma yapma, kaynak güvenilirliğini değerlendirme ve bulguları sentezleme; (2) CSV/Excel/JSON veri dosyalarını Python ile işleme, istatistiksel analiz ve görselleştirme. Use whenever the zettelkasten skill needs research for a literature note, when the user asks to research a topic with sources, or when the user provides a data file to analyze or visualize. Keywords - araştır, kaynak, literatür, veri analizi, CSV, Excel, pandas, grafik, istatistik, research, data analysis.
---

# Veri Analitiği

Two capabilities, two reference files. Load only the one you need:

| Need | Read |
|---|---|
| Web research for a literature note (sources, reliability, synthesis) | `references/research.md` |
| Analysis of a data file (CSV/XLSX/JSON/Parquet), stats, charts, upload to Notion | `references/data-analysis.md` |

## Shared rules

- User-facing output is Turkish; these instructions are English.
- **Sources are mandatory and must be real.** Every factual claim in a deliverable traces to
  a URL you actually fetched or a data file you actually loaded. Model memory may shape
  questions and hypotheses; it is never a citation.
- Prefer primary and institutional sources (standards bodies, official statistics,
  peer-reviewed papers, original documentation, the organisation's own site) over
  secondary summaries. Say when only secondary sources were available.
- Turkish-first: search in Turkish, then in English to fill gaps or when Turkish coverage is
  thin or outdated. The note is written in Turkish regardless of source language.
- 3–5 sources per literature note. Fewer than 3 usable sources → tell the user and ask
  whether to proceed.
- Separate **finding** (what the source/data says) from **interpretation** (what you make
  of it). Put interpretation under "Değerlendirme" / "Sonuç".
- Numbers: give the figure, the unit, the date/period and the source `[n]`. Never round
  away the uncertainty the source states.
- When sources conflict, report the conflict and which source is more credible and why;
  do not silently pick one.
- Keep working files in the scratchpad directory; never write into the plugin directory.

## Hand-off to Notion

This skill produces content; the `zettelkasten` skill owns saving. When done, return:
title proposal, body (Notion-flavored Markdown, template "Literatür Not"), numbered
source list for `Kaynak`, tag proposal, and, for data analysis, the list of chart
files to upload. Then the zettelkasten confirmation protocol applies.
