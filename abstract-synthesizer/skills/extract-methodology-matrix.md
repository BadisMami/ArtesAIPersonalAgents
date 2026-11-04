---
name: methodology-matrix-extractor
description: Extracts study design, sample/dataset scale, variables/metrics, key findings, and limitations from provided papers into a side-by-side Markdown table. Use when the user types /matrix or asks to compare methods, datasets, or study designs across papers.
---

# Methodology Matrix Extractor (`/matrix`)

## When to Apply This Skill
Trigger this skill when the user types `/matrix` or asks to compare the methods, datasets, study designs, or limitations of the papers provided in the conversation.

## Step-by-Step Instructions
1. Review every paper, abstract, or reading note provided by the user in the current conversation.
2. Construct a Markdown comparison table with the following exact columns:
   - **Study (Author, Year)**
   - **Research Approach / Design** (e.g., Observational, Simulation, RCT, Qualitative Interview)
   - **Sample / Dataset & Scale** (e.g., N=450 students, 10-year MODIS satellite data; write `Not stated in abstract` if absent)
   - **Primary Metrics / Variables**
   - **Key Finding**
   - **Noted or Implied Limitation**
3. Below the table, add a short **"Methodological Takeaways"** bullet list (2–3 bullets) highlighting dominant methods in this group of papers and any methodological blind spots.
