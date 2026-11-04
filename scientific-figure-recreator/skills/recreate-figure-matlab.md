---
name: figure-recreator-matlab
description: Generates a self-contained MATLAB .m script (rng, synthetic data, tiledlayout, exportgraphics) to recreate an uploaded scientific figure locally. Use when the user attaches this skill, types /matlab, or asks to recreate a figure in MATLAB.
---

# Recreate Figure in MATLAB (`/matlab`)

## When to Apply This Skill
Use this skill whenever it is attached to the conversation, when the user types `/matlab`, or when the user asks to recreate an uploaded scientific figure using MATLAB.

## MATLAB `.m` Script Coding Requirements
Write a single, self-contained MATLAB script (`recreate_figure.m`) compatible with modern MATLAB (R2020b+):

1. **Section 1: Seeded Synthetic Data (`rng(42)`)**:
   - Start with `clear; clc; close all; rng(42);`.
   - Generate synthetic vectors/matrices or a `table` (`T`) matching the means, standard errors, and groups in the uploaded figure.
2. **Section 2: "Swap Your Own Data Here" Block**:
   - Include a commented-out `% T = readtable('your_data.csv');` block listing the expected column names.
3. **Section 3: `tiledlayout` & Publication Styling**:
   - Use `fig = figure('Color', 'w', 'Position', [100, 100, 900, 420]);` and `tiledlayout(...)` for clean single or multi-panel alignment.
   - Apply exact hex colors (`'#RRGGBB'` supported in R2019a+ or `[R G B]/255` triplets), shaded confidence intervals (`fill([x; flipud(x)], [ci_low; flipud(ci_high)], ...)` with `'FaceAlpha', 0.2, 'EdgeColor', 'none'`), error bars (`errorbar`), and reference lines (`xline`, `yline`).
   - Set `box off; set(gca, 'TickDir', 'out', 'FontSize', 11, 'LineWidth', 1.1);`.
4. **Section 4: High-Resolution Local Export**:
   - Save using `exportgraphics(fig, 'recreated_figure.png', 'Resolution', 300);` and `exportgraphics(fig, 'recreated_figure.pdf', 'ContentType', 'vector');`.
