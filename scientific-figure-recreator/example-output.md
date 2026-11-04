# Example Output: Scientific Figure Recreator

Below is the expected output when you upload [`sample-paper-figure.png`](./sample-paper-figure.png) and run the prompt from [`example-input.md`](./example-input.md). Depending on which **Language Skill** you attach via **`+` → `Skills >`**, the agent will generate the matching script (**Python**, **R**, **Stata**, or **MATLAB**) below the Visual Anatomy Blueprint.

---

## Step 1 — Visual Anatomy Blueprint

### 1. Chart Architecture & Layout
- **Overall Layout**: Horizontal 2-panel figure (`1 row × 2 columns`), with Panel A slightly wider than Panel B (`~1.35 : 1` width ratio) and open L-shaped axes (top and right spines removed).
- **Panel A (`A. Event-Study Treatment Effect Trajectory`)**:
  - **Type**: Difference-in-Differences (DiD) / Event-Study line plot with shaded 95% confidence interval ribbons (`alpha ≈ 0.20`).
  - **X-Axis**: `Years Relative to Policy Adoption (t = 0)`, integer ticks from `-4` to `5`.
  - **Y-Axis**: `Change in Wetland Canopy Index (SD)`, ticks from `-0.5` to `2.5` by `0.5`.
  - **Reference Lines**: Horizontal dashed gray baseline at `y = 0.0`; vertical dotted red line at `x = -0.5` labeled *"Policy Adoption"* in italic red text.
  - **Series**:
    - `Treated Counties (n = 28)`: Deep burgundy/garnet line with circular markers (`o`), flat near `0` pre-policy (`t = -4..0`), rising nonlinearly to `+2.05 SD` by `t = +5`.
    - `Control Counties (n = 34)`: Slate-gray line with square markers (`s`), flat near `0.0` across all years (`-4..5`).
- **Panel B (`B. Post-Policy Effect by Subgroup`)**:
  - **Type**: 3-group boxplot overlaid with horizontally jittered individual county observations (white-edged circular points).
  - **X-Axis Categories**: `Control Counties`, `Treated (Inland)`, `Treated (Coastal)`.
  - **Y-Axis**: `Mean Post-Treatment Effect (SD)`, ticks from `-1.0` to `3.0` by `1.0`, with a horizontal dashed baseline at `y = 0.0`.

### 2. Extracted Hex Color Palette
| Visual Element | Hex Code | RGB Triplet (for Stata/MATLAB) |
| :--- | :--- | :--- |
| **Treated Counties / Coastal Subgroup (Garnet)** | `#782F40` | `120 47 64` |
| **Control Counties (Slate Gray)** | `#5C6B73` | `92 107 115` |
| **Treated Inland Subgroup (Warm Gold)** | `#CEB888` | `206 184 136` |
| **Policy Adoption Vertical Line (Crimson)** | `#B22222` | `178 34 34` |
| **Zero Reference Baseline (Neutral Gray)** | `#8C8C8C` | `140 140 140` |

### 3. Synthetic Data Schema
To reproduce both panels from your own data later, your CSV files only need:
- **Panel A (`event_study_data.csv`)**: `year` (`-4` to `5`), `group` (`"Treated"`, `"Control"`), `mean_effect`, `ci_low`, `ci_high`
- **Panel B (`subgroup_data.csv`)**: `county_id`, `subgroup` (`"Control Counties"`, `"Treated (Inland)"`, `"Treated (Coastal)"`), `post_effect_sd`

---

## Step 2 — Reproducible Local Code (By Attached Language Skill)

### Option A: If You Attached `figure-recreator-python` (`/python`)

Save as `recreate_figure.py` and run with `python3 recreate_figure.py`:

```python
"""
Reproducible Recreation of Two-Panel Event-Study & Subgroup Figure
Saves: recreated_figure.png (300 DPI) and recreated_figure.pdf (Vector)
"""

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# =============================================================================
# 1. SEEDED SYNTHETIC DATA GENERATOR (Runs out-of-the-box)
# =============================================================================
rng = np.random.default_rng(42)
years = np.arange(-4, 6)

df_panel_a = pd.DataFrame({
    "year": np.tile(years, 2),
    "group": ["Control Counties (n = 34)"] * 10 + ["Treated Counties (n = 28)"] * 10,
    "mean_effect": [
        -0.05, 0.02, -0.01, 0.03, 0.00, 0.04, 0.02, 0.05, 0.03, 0.06,  # Control
        -0.08, -0.02, 0.04, -0.01, 0.00, 0.85, 1.42, 1.78, 1.95, 2.05, # Treated
    ],
    "ci_halfwidth": [
        0.22, 0.22, 0.22, 0.22, 0.22, 0.22, 0.22, 0.22, 0.22, 0.22,
        0.24, 0.23, 0.22, 0.21, 0.05, 0.26, 0.28, 0.30, 0.31, 0.32,
    ],
})
df_panel_a["ci_low"] = df_panel_a["mean_effect"] - df_panel_a["ci_halfwidth"]
df_panel_a["ci_high"] = df_panel_a["mean_effect"] + df_panel_a["ci_halfwidth"]

df_panel_b = pd.DataFrame({
    "subgroup": (
        ["Control\nCounties"] * 34
        + ["Treated\n(Inland)"] * 14
        + ["Treated\n(Coastal)"] * 14
    ),
    "post_effect_sd": np.concatenate([
        rng.normal(loc=0.04, scale=0.35, size=34),
        rng.normal(loc=1.34, scale=0.45, size=14),
        rng.normal(loc=2.14, scale=0.52, size=14),
    ]),
})

# =============================================================================
# 2. SWAP YOUR OWN DATA HERE (Uncomment to load your own CSVs)
# =============================================================================
# df_panel_a = pd.read_csv("my_event_study_data.csv")  # cols: year, group, mean_effect, ci_low, ci_high
# df_panel_b = pd.read_csv("my_subgroup_data.csv")     # cols: subgroup, post_effect_sd

# =============================================================================
# 3. PUBLICATION STYLING & MULTI-PANEL PLOTTING
# =============================================================================
PALETTE = {
    "garnet": "#782F40",
    "slate": "#5C6B73",
    "gold": "#CEB888",
    "crimson": "#B22222",
    "gray": "#8C8C8C",
}

fig, (ax1, ax2) = plt.subplots(
    1, 2, figsize=(11, 4.6), gridspec_kw={"width_ratios": [1.35, 1]}
)

# --- Panel A: Event-Study Trajectory ---
ax1.axhline(0, color=PALETTE["gray"], linestyle="--", linewidth=1.1, zorder=1)
ax1.axvline(-0.5, color=PALETTE["crimson"], linestyle=":", linewidth=1.4, zorder=1)
ax1.text(-0.35, 2.18, "Policy Adoption", color=PALETTE["crimson"], fontsize=9.5, style="italic")

series_specs = [
    ("Treated Counties (n = 28)", PALETTE["garnet"], "o"),
    ("Control Counties (n = 34)", PALETTE["slate"], "s"),
]
for label, color, marker in series_specs:
    sub = df_panel_a[df_panel_a["group"] == label]
    ax1.fill_between(sub["year"], sub["ci_low"], sub["ci_high"], color=color, alpha=0.20)
    ax1.plot(
        sub["year"], sub["mean_effect"],
        marker=marker, color=color, linewidth=2.2, markersize=6, label=label
    )

ax1.set_title("A. Event-Study Treatment Effect Trajectory", loc="left", fontsize=12, fontweight="bold", pad=10)
ax1.set_xlabel("Years Relative to Policy Adoption (t = 0)", fontsize=10.5)
ax1.set_ylabel("Change in Wetland Canopy Index (SD)", fontsize=10.5)
ax1.set_xticks(years)
ax1.set_ylim(-0.6, 2.5)
ax1.legend(frameon=False, loc="upper left", fontsize=9.5)
ax1.spines[["top", "right"]].set_visible(False)

# --- Panel B: Subgroup Boxplot + Jittered Points ---
groups_order = ["Control\nCounties", "Treated\n(Inland)", "Treated\n(Coastal)"]
group_colors = [PALETTE["slate"], PALETTE["gold"], PALETTE["garnet"]]
grouped_vals = [df_panel_b.loc[df_panel_b["subgroup"] == g, "post_effect_sd"].values for g in groups_order]

ax2.axhline(0, color=PALETTE["gray"], linestyle="--", linewidth=1.1, zorder=1)
bp = ax2.boxplot(
    grouped_vals, positions=[1, 2, 3], widths=0.45, patch_artist=True,
    showfliers=False, medianprops={"color": "#191919", "linewidth": 2.0}
)
for patch, whisker_pair, cap_pair, col in zip(
    bp["boxes"], np.reshape(bp["whiskers"], (3, 2)), np.reshape(bp["caps"], (3, 2)), group_colors
):
    patch.set_facecolor(col)
    patch.set_alpha(0.38)
    patch.set_edgecolor(col)
    patch.set_linewidth(1.6)
    for w, c in zip(whisker_pair, cap_pair):
        w.set(color=col, linewidth=1.4)
        c.set(color=col, linewidth=1.4)

for idx, (vals, col) in enumerate(zip(grouped_vals, group_colors), start=1):
    jitter = rng.uniform(-0.14, 0.14, size=len(vals))
    ax2.scatter(
        np.full_like(vals, idx) + jitter, vals,
        color=col, alpha=0.85, s=28, edgecolors="white", linewidth=0.6, zorder=3
    )

ax2.set_title("B. Post-Policy Effect by Subgroup", loc="left", fontsize=12, fontweight="bold", pad=10)
ax2.set_xticks([1, 2, 3])
ax2.set_xticklabels(groups_order, fontsize=10)
ax2.set_ylabel("Mean Post-Treatment Effect (SD)", fontsize=10.5)
ax2.set_ylim(-1.0, 3.5)
ax2.spines[["top", "right"]].set_visible(False)

# =============================================================================
# 4. HIGH-RESOLUTION LOCAL EXPORT
# =============================================================================
plt.tight_layout(pad=1.8)
plt.savefig("recreated_figure.png", dpi=300, bbox_inches="tight")
plt.savefig("recreated_figure.pdf", bbox_inches="tight")
print("Saved recreated_figure.png (300 DPI) and recreated_figure.pdf")
plt.show()
```

---

### Option B: If You Attached `figure-recreator-r` (`/r`)

Save as `recreate_figure.R` and run in RStudio or via `Rscript recreate_figure.R`:

```r
# Reproducible Recreation of Two-Panel Figure in R (ggplot2 + patchwork)
library(ggplot2)
library(dplyr)
library(patchwork)

set.seed(42)

# =============================================================================
# 1. SEEDED SYNTHETIC DATA GENERATOR
# =============================================================================
years <- -4:5
df_panel_a <- tibble(
  year = rep(years, 2),
  group = factor(
    rep(c("Treated Counties (n = 28)", "Control Counties (n = 34)"), each = 10),
    levels = c("Treated Counties (n = 28)", "Control Counties (n = 34)")
  ),
  mean_effect = c(
    -0.08, -0.02, 0.04, -0.01, 0.00, 0.85, 1.42, 1.78, 1.95, 2.05,
    -0.05,  0.02, -0.01, 0.03, 0.00, 0.04, 0.02, 0.05, 0.03, 0.06
  ),
  ci_half = c(
    0.24, 0.23, 0.22, 0.21, 0.05, 0.26, 0.28, 0.30, 0.31, 0.32,
    rep(0.22, 10)
  )
) |>
  mutate(ci_low = mean_effect - ci_half, ci_high = mean_effect + ci_half)

df_panel_b <- tibble(
  subgroup = factor(
    c(rep("Control\nCounties", 34), rep("Treated\n(Inland)", 14), rep("Treated\n(Coastal)", 14)),
    levels = c("Control\nCounties", "Treated\n(Inland)", "Treated\n(Coastal)")
  ),
  post_effect_sd = c(
    rnorm(34, mean = 0.04, sd = 0.35),
    rnorm(14, mean = 1.34, sd = 0.45),
    rnorm(14, mean = 2.14, sd = 0.52)
  )
)

# =============================================================================
# 2. SWAP YOUR OWN DATA HERE
# =============================================================================
# df_panel_a <- readr::read_csv("my_event_study_data.csv")
# df_panel_b <- readr::read_csv("my_subgroup_data.csv")

# =============================================================================
# 3. GGPLOT2 LAYERING & PATCHWORK ASSEMBLY
# =============================================================================
p_a <- ggplot(df_panel_a, aes(x = year, y = mean_effect, color = group, fill = group, shape = group)) +
  geom_hline(yintercept = 0, linetype = "dashed", color = "#8C8C8C", linewidth = 0.5) +
  geom_vline(xintercept = -0.5, linetype = "dotted", color = "#B22222", linewidth = 0.7) +
  annotate("text", x = -0.35, y = 2.2, label = "Policy Adoption", color = "#B22222", fontface = "italic", hjust = 0, size = 3.5) +
  geom_ribbon(aes(ymin = ci_low, ymax = ci_high), alpha = 0.20, color = NA) +
  geom_line(linewidth = 1.0) +
  geom_point(size = 2.6) +
  scale_color_manual(values = c("#782F40", "#5C6B73")) +
  scale_fill_manual(values = c("#782F40", "#5C6B73")) +
  scale_shape_manual(values = c(16, 15)) +
  scale_x_continuous(breaks = -4:5) +
  coord_cartesian(ylim = c(-0.6, 2.5)) +
  labs(
    title = "A. Event-Study Treatment Effect Trajectory",
    x = "Years Relative to Policy Adoption (t = 0)",
    y = "Change in Wetland Canopy Index (SD)",
    color = NULL, fill = NULL, shape = NULL
  ) +
  theme_classic(base_size = 12) +
  theme(
    plot.title = element_text(face = "bold", size = 12),
    legend.position = c(0.28, 0.88),
    legend.background = element_blank()
  )

p_b <- ggplot(df_panel_b, aes(x = subgroup, y = post_effect_sd, fill = subgroup, color = subgroup)) +
  geom_hline(yintercept = 0, linetype = "dashed", color = "#8C8C8C", linewidth = 0.5) +
  geom_boxplot(width = 0.45, alpha = 0.38, outlier.shape = NA, median.colour = "#191919", fatten = 1.8) +
  geom_jitter(width = 0.14, size = 2.2, alpha = 0.85, shape = 21, stroke = 0.4, color = "white") +
  scale_fill_manual(values = c("#5C6B73", "#CEB888", "#782F40")) +
  scale_color_manual(values = c("#5C6B73", "#CEB888", "#782F40")) +
  coord_cartesian(ylim = c(-1.0, 3.5)) +
  labs(
    title = "B. Post-Policy Effect by Subgroup",
    x = NULL,
    y = "Mean Post-Treatment Effect (SD)"
  ) +
  theme_classic(base_size = 12) +
  theme(
    plot.title = element_text(face = "bold", size = 12),
    legend.position = "none"
  )

combined_fig <- p_a + p_b + plot_layout(widths = c(1.35, 1))
ggsave("recreated_figure.png", combined_fig, width = 11, height = 4.6, dpi = 300)
ggsave("recreated_figure.pdf", combined_fig, width = 11, height = 4.6)
```

---

### Option C: If You Attached `figure-recreator-stata` (`/stata`)

Save as `recreate_figure.do` and run in Stata (`do recreate_figure.do`):

```stata
* ==============================================================================
* Reproducible Recreation of Event-Study & Subgroup Figure in Stata
* ==============================================================================
version 17
clear all
set more off
set seed 42

* --- 1. Synthetic Data for Panel A (Event-Study) ---
set obs 10
gen int year = _n - 5

gen double ctrl_mean  = cond(year == -4, -0.05, cond(year == -3, 0.02, cond(year == -2, -0.01, cond(year == -1, 0.03, cond(year == 0, 0.00, 0.04)))))
gen double ctrl_low   = ctrl_mean - 0.22
gen double ctrl_high  = ctrl_mean + 0.22

gen double treat_mean = 0
replace treat_mean = -0.08 if year == -4
replace treat_mean = -0.02 if year == -3
replace treat_mean =  0.04 if year == -2
replace treat_mean = -0.01 if year == -1
replace treat_mean =  0.00 if year ==  0
replace treat_mean =  0.85 if year ==  1
replace treat_mean =  1.42 if year ==  2
replace treat_mean =  1.78 if year ==  3
replace treat_mean =  1.95 if year ==  4
replace treat_mean =  2.05 if year ==  5

gen double treat_ci   = cond(year == 0, 0.05, 0.25)
gen double treat_low  = treat_mean - treat_ci
gen double treat_high = treat_mean + treat_ci

* SWAP YOUR OWN DATA HERE:
* import delimited "my_event_study_data.csv", clear

twoway ///
    (rarea ctrl_low ctrl_high year, color("92 107 115%20") lwidth(none)) ///
    (rarea treat_low treat_high year, color("120 47 64%22") lwidth(none)) ///
    (connected ctrl_mean year, lcolor("92 107 115") mcolor("92 107 115") msymbol(square) lwidth(medthick)) ///
    (connected treat_mean year, lcolor("120 47 64") mcolor("120 47 64") msymbol(circle) lwidth(medthick)), ///
    yline(0, lpattern(dash) lcolor("140 140 140")) ///
    xline(-0.5, lpattern(dot) lcolor("178 34 34") lwidth(medthick)) ///
    text(2.2 -0.35 "{it:Policy Adoption}", place(e) color("178 34 34") size(small)) ///
    title("{bf:A. Event-Study Treatment Effect Trajectory}", pos(11) size(medsmall)) ///
    xtitle("Years Relative to Policy Adoption (t = 0)") ///
    ytitle("Change in Wetland Canopy Index (SD)") ///
    xlabel(-4(1)5, nogrid) ylabel(-0.5(0.5)2.5, angle(horizontal) nogrid) ///
    legend(order(4 "Treated Counties (n = 28)" 3 "Control Counties (n = 34)") pos(11) ring(0) cols(1) region(lstyle(none))) ///
    graphregion(color(white)) plotregion(color(white)) ///
    name(panelA, replace)

graph export "recreated_figure_panelA.png", width(2400) replace
```

