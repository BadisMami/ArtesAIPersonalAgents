---
name: figure-recreator-stata
description: Generates a self-contained Stata .do file (set seed, synthetic data, twoway graph layering, graph export) to recreate an uploaded scientific figure locally. Use when the user attaches this skill, types /stata, or asks to recreate a figure in Stata.
---

# Recreate Figure in Stata (`/stata`)

## When to Apply This Skill
Use this skill whenever it is attached to the conversation, when the user types `/stata`, or when the user asks to recreate an uploaded scientific figure using Stata.

## Stata `.do` File Coding Requirements
Write a single, self-contained Stata `.do` file (`recreate_figure.do`) that runs cleanly in standard Stata (16/17/18+) without requiring hard-to-install external packages:

1. **Section 1: Environment Setup & Seeded Synthetic Data (`set seed 42`)**:
   - Start with `version 17`, `clear all`, `set more off`, and `set seed 42`.
   - Use `set obs ...` and `generate` / `egen` commands to construct a realistic synthetic dataset in memory that reproduces the trends, confidence intervals, and groups shown in the figure.
2. **Section 2: "Swap Your Own Data Here" Block**:
   - Include a commented-out `* import delimited "your_data.csv", clear` block showing the variable names expected by the `twoway` command.
3. **Section 3: Publication-Styled `twoway` Graph Commands**:
   - Use RGB color codes (`"R G B"` converted from the extracted hex codes) in `lcolor("...")`, `mcolor("...")`, and `fcolor("...%25")` (with opacity for confidence bands via `rarea` or `rcap`).
   - Configure clean white backgrounds (`graphregion(color(white)) plotregion(color(white))`), crisp axis labels (`xlabel(, nogrid) ylabel(, angle(horizontal))`), reference lines (`xline(...)` / `yline(...)`), and legend placement (`legend(order(...) region(lstyle(none)))`).
   - If the figure has multiple panels, save each panel with `name(panelA, replace)` and combine them using `graph combine panelA panelB, ycommon graphregion(color(white))`.
4. **Section 4: High-Resolution Local Export**:
   - Export to both PNG (`graph export "recreated_figure.png", width(2400) replace`) and PDF (`graph export "recreated_figure.pdf", replace`).
