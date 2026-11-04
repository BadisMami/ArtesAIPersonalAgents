---
name: figure-recreator-r
description: Generates a self-contained R script (ggplot2, dplyr, tidyr, patchwork) with seeded synthetic data to recreate an uploaded scientific figure locally. Use when the user attaches this skill, types /r, or asks to recreate a figure in R or ggplot2.
---

# Recreate Figure in R (`/r`)

## When to Apply This Skill
Use this skill whenever it is attached to the conversation, when the user types `/r`, or when the user asks to recreate an uploaded scientific figure using R (`ggplot2`).

## R Coding Requirements
Write a single, self-contained R script (`recreate_figure.R`) using `ggplot2`, `dplyr`, `tidyr`, and `patchwork` (for multi-panel figures):

1. **Section 1: Seeded Synthetic Data Generator (`set.seed(42)`)**:
   - Construct a tidy `tibble` / `data.frame` (`df`) whose group means, trajectories, and variances mirror the uploaded figure.
2. **Section 2: "Swap Your Own Data Here" Block**:
   - Include a commented-out `# df <- readr::read_csv("your_data.csv")` block documenting the required column names.
3. **Section 3: `ggplot2` Layering & Publication Theme**:
   - Use explicit hex color scales (`scale_color_manual(values = ...)` and `scale_fill_manual(values = ...)`).
   - Match geoms accurately (`geom_ribbon`, `geom_line`, `geom_pointrange`, `geom_errorbar`, `geom_violin`, `geom_boxplot`, `geom_jitter`, `geom_hline`, `geom_vline`).
   - Apply a clean publication theme (`theme_classic(base_size = 12)` or `theme_minimal(base_size = 12)`) with customized `theme(...)` settings for legend position, axis lines, and gridlines.
   - If the figure has multiple panels, combine them cleanly with `patchwork` (`p1 + p2 + plot_layout(...)`).
4. **Section 4: High-Resolution Local Export**:
   - Export both `recreated_figure.png` (`dpi = 300`) and vector `recreated_figure.pdf` using `ggsave(...)`.
