# Example Output: Scientific Figure Recreator

Below is the expected output when you upload [`sample-paper-figure.png`](./sample-paper-figure.png) and run the prompt from [`example-input.md`](./example-input.md). Depending on which **Language Skill** you attach via **`+` → `Skills >`**, the agent will generate the a script (**Python**, **R**, **Stata**, or **MATLAB**) below the Visual Anatomy Blueprint.

This example output was generated with ArtesAI using gpt-5.6-luna on 11/04/2026
---

## Figure anatomy
* Panel A: Event-study line plot from years −4 to +5, with treated and control county trajectories, shaded 95% confidence ribbons, a dashed zero reference, and a red dashed policy-adoption marker.
* Panel B: Jittered observations over boxplots for control, treated-inland, and treated-coastal subgroups, with a dashed zero reference.
* Approximate palette: Burgundy #984653, slate blue-gray #78878E, and warm sand #DCC89B, with pale matching fills.
* The script generates seeded synthetic data and includes a CSV swap-in block. The recreated values are approximations, not the original paper’s data.

I created the self-contained R script, which exports a 300-dpi PNG and a vector PDF: recreate_figure.R. It uses ggplot2, dplyr, tidyr, and patchwork.

```r
# Recreate the two-panel event-study figure
# Required packages: ggplot2, dplyr, tidyr, patchwork
# Install if needed: install.packages(c("ggplot2", "dplyr", "tidyr", "patchwork", "readr"))

library(ggplot2)
library(dplyr)
library(tidyr)
library(patchwork)

# -----------------------------------------------------------------------------
# 1. Seeded synthetic data generator
# -----------------------------------------------------------------------------
set.seed(42)

# Panel A target event-time means approximate the plotted trajectories.
event_times <- -4:5
treated_means <- c(-0.08, -0.02, 0.04, -0.01, 0.00, 0.85, 1.42, 1.78, 1.95, 2.05)
control_means <- c(-0.04,  0.01, -0.02, 0.015, 0.00, 0.04, 0.02, 0.05, 0.03, 0.06)
treated_sds   <- c(0.62, 0.62, 0.62, 0.62, 0.38, 0.68, 0.74, 0.79, 0.83, 0.86)
control_sds   <- rep(0.66, length(event_times))

# Generate county-level observations around each target mean. Residuals are
# centered/scaled at each event time so the synthetic sample matches the
# specified trajectory and approximate uncertainty closely.
make_event_group <- function(group_name, n_counties, target_means, target_sds) {
  pieces <- lapply(seq_along(event_times), function(j) {
    residuals <- rnorm(n_counties)
    residuals <- residuals - mean(residuals)
    residuals <- residuals / sd(residuals) * target_sds[j]
    tibble(
      county_id = paste0(ifelse(group_name == "Treated Counties", "T", "C"),
                         sprintf("%02d", seq_len(n_counties))),
      group = group_name,
      event_time = event_times[j],
      outcome = target_means[j] + residuals
    )
  })
  bind_rows(pieces)
}

df_event <- bind_rows(
  make_event_group("Treated Counties", 28, treated_means, treated_sds),
  make_event_group("Control Counties", 34, control_means, control_sds)
)

# Panel B: synthetic individual post-policy effects for three subgroups.
df_subgroup <- bind_rows(
  tibble(subgroup = "Control Counties", effect = rnorm(18, mean = 0.00, sd = 0.34)),
  tibble(subgroup = "Treated (Inland)", effect = rnorm(17, mean = 1.34, sd = 0.43)),
  tibble(subgroup = "Treated (Coastal)", effect = rnorm(18, mean = 2.08, sd = 0.52))
) %>%
  group_by(subgroup) %>%
  mutate(observation_id = row_number()) %>%
  ungroup() %>%
  mutate(subgroup = factor(
    subgroup,
    levels = c("Control Counties", "Treated (Inland)", "Treated (Coastal)")
  ))

# -----------------------------------------------------------------------------
# Swap Your Own Data Here
# df_event <- readr::read_csv("your_event_study.csv")  # columns: county_id, group, event_time, outcome
# df_subgroup <- readr::read_csv("your_subgroup_data.csv")  # columns: subgroup, observation_id, effect
# Keep the column names above; then rerun the summary and plotting sections.
# -----------------------------------------------------------------------------

# Summarize Panel A for the point estimates and 95% t-based confidence ribbons.
event_summary <- df_event %>%
  group_by(group, event_time) %>%
  summarise(
    estimate = mean(outcome),
    sd = sd(outcome),
    n = n(),
    se = sd / sqrt(n),
    ci = qt(0.975, df = n - 1) * se,
    .groups = "drop"
  ) %>%
  mutate(group = factor(group, levels = c("Treated Counties", "Control Counties")))

# Palette sampled/approximated from the source figure.
col_treated <- "#984653"  # muted burgundy
col_control <- "#78878E"  # slate gray-blue
col_inland  <- "#DCC89B"  # warm sand
fill_treated <- "#E8DADD"
fill_control <- "#E1E4E6"

series_cols <- c("Treated Counties" = col_treated,
                 "Control Counties" = col_control)
series_fills <- c("Treated Counties" = fill_treated,
                  "Control Counties" = fill_control)
subgroup_cols <- c("Control Counties" = col_control,
                   "Treated (Inland)" = col_inland,
                   "Treated (Coastal)" = col_treated)

# -----------------------------------------------------------------------------
# 2. Panel A: event-study treatment trajectory
# -----------------------------------------------------------------------------
p1 <- ggplot(event_summary,
             aes(x = event_time, y = estimate, color = group, fill = group,
                 group = group)) +
  geom_ribbon(aes(ymin = estimate - ci, ymax = estimate + ci),
              alpha = 0.95, color = NA) +
  geom_hline(yintercept = 0, color = "#9E9E9E", linewidth = 0.55,
             linetype = "dashed") +
  geom_vline(xintercept = -0.5, color = "#F02B24", linewidth = 0.7,
             linetype = "dashed") +
  geom_line(aes(linetype = group), linewidth = 1.05) +
  geom_point(aes(shape = group), size = 2.6, stroke = 0.6) +
  annotate("text", x = 0.65, y = 2.23, label = "Policy Adoption",
           color = "#E51C16", fontface = "italic", size = 3.7, hjust = 0) +
  scale_color_manual(values = series_cols, name = NULL) +
  scale_fill_manual(values = series_fills, guide = "none") +
  scale_shape_manual(values = c("Treated Counties" = 16,
                                "Control Counties" = 15), name = NULL,
                     labels = c("Treated Counties (n = 28)",
                                "Control Counties (n = 34)")) +
  scale_linetype_manual(values = c("Treated Counties" = "solid",
                                   "Control Counties" = "solid"),
                        name = NULL,
                        labels = c("Treated Counties (n = 28)",
                                   "Control Counties (n = 34)")) +
  scale_x_continuous(breaks = -4:5, limits = c(-4.3, 5.3),
                     expand = expansion(mult = 0)) +
  scale_y_continuous(breaks = seq(-0.5, 2.5, by = 0.5),
                     limits = c(-0.6, 2.5), expand = expansion(mult = 0)) +
  labs(
    title = "A. Event-Study Treatment Effect Trajectory",
    x = "Years Relative to Policy Adoption (t = 0)",
    y = "Change in Wetland Canopy Index (SD)"
  ) +
  guides(color = "none", fill = "none",
         shape = guide_legend(override.aes = list(
           color = c(col_treated, col_control),
           linetype = c("solid", "solid"),
           size = 2.6
         )),
         linetype = "none") +
  theme_classic(base_size = 11) +
  theme(
    plot.title = element_text(face = "bold", size = 12, hjust = 0),
    axis.title = element_text(size = 10.5, color = "#222222"),
    axis.text = element_text(size = 9.5, color = "#222222"),
    axis.line = element_line(linewidth = 0.6, color = "#222222"),
    axis.ticks = element_line(linewidth = 0.6, color = "#222222"),
    legend.position = c(0.03, 0.96),
    legend.justification = c(0, 1),
    legend.text = element_text(size = 9),
    legend.key = element_blank(),
    legend.background = element_blank(),
    plot.margin = margin(8, 14, 8, 8)
  )

# -----------------------------------------------------------------------------
# 3. Panel B: subgroup distributions
# -----------------------------------------------------------------------------
p2 <- ggplot(df_subgroup, aes(x = subgroup, y = effect, fill = subgroup,
                              color = subgroup)) +
  geom_hline(yintercept = 0, color = "#9E9E9E", linewidth = 0.55,
             linetype = "dashed") +
  geom_boxplot(width = 0.40, outlier.shape = NA, linewidth = 0.75,
               alpha = 0.78, color = "#3B3B3B") +
  geom_jitter(width = 0.14, height = 0, size = 2.2, alpha = 0.95,
              shape = 21, stroke = 0.55, color = "white") +
  scale_fill_manual(values = subgroup_cols, guide = "none") +
  scale_color_manual(values = subgroup_cols, guide = "none") +
  scale_x_discrete(labels = c("Control\nCounties", "Treated\n(Inland)",
                               "Treated\n(Coastal)"),
                   expand = expansion(add = 0.55)) +
  scale_y_continuous(breaks = -1:3, limits = c(-1, 3.5),
                     expand = expansion(mult = 0)) +
  labs(
    title = "B. Post-Policy Effect by Subgroup",
    x = NULL,
    y = "Mean Post-Treatment Effect (SD)"
  ) +
  theme_classic(base_size = 11) +
  theme(
    plot.title = element_text(face = "bold", size = 12, hjust = 0),
    axis.title = element_text(size = 10.5, color = "#222222"),
    axis.text = element_text(size = 9.5, color = "#222222"),
    axis.line = element_line(linewidth = 0.6, color = "#222222"),
    axis.ticks = element_line(linewidth = 0.6, color = "#222222"),
    plot.margin = margin(8, 8, 8, 14)
  )

# -----------------------------------------------------------------------------
# 4. Assemble and export: high-resolution PNG and vector PDF
# -----------------------------------------------------------------------------
recreated_figure <- p1 + p2 + plot_layout(widths = c(1.5, 1))

# Preview in an interactive R session:
print(recreated_figure)

ggsave("recreated_figure.png", plot = recreated_figure,
       width = 12, height = 5.2, units = "in", dpi = 300, bg = "white")
ggsave("recreated_figure.pdf", plot = recreated_figure,
       width = 12, height = 5.2, units = "in", device = "pdf", bg = "white")

```

# Option B: Code generated with the python skill instead


```python
"""Recreate a two-panel event-study and subgroup-effects figure.

Requirements: numpy, pandas, matplotlib
Run: python recreate_figure.py
The script generates seeded synthetic data, then saves PNG and PDF outputs.
"""

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt


# -----------------------------------------------------------------------------
# Section 1: seeded synthetic data generator
# Unified long-format schema:
#   panel       : "trajectory" or "subgroup"
#   group       : group label
#   event_time  : event time for trajectory rows; NaN for subgroup rows
#   value       : outcome / effect value
# -----------------------------------------------------------------------------
rng = np.random.default_rng(42)

# Event-study target means closely follow the figure.
event_times = np.arange(-4, 6)
trajectory_targets = {
    "Treated Counties": np.array([-0.08, -0.02, 0.04, -0.01, 0.00, 0.85, 1.42, 1.78, 1.95, 2.05]),
    "Control Counties": np.array([-0.03, 0.01, -0.02, 0.02, 0.00, 0.04, 0.02, 0.05, 0.03, 0.06]),
}
trajectory_sds = {
    "Treated Counties": np.array([0.62, 0.64, 0.62, 0.61, 0.60, 0.70, 0.78, 0.78, 0.82, 0.82]),
    "Control Counties": np.array([0.54, 0.56, 0.55, 0.56, 0.55, 0.54, 0.55, 0.56, 0.55, 0.57]),
}
county_counts = {"Treated Counties": 28, "Control Counties": 34}

rows = []
for group, target_means in trajectory_targets.items():
    n = county_counts[group]
    for t, target, sd in zip(event_times, target_means, trajectory_sds[group]):
        # Center and rescale each simulated cross-section so its sample mean and
        # SD track the target trajectory while retaining realistic variation.
        draws = rng.normal(size=n)
        draws = (draws - draws.mean()) / draws.std(ddof=1)
        values = target + sd * draws
        rows.extend({"panel": "trajectory", "group": group,
                     "event_time": int(t), "value": float(v)} for v in values)

# Subgroup observations for the boxplots and overlaid county-level points.
# Target centers/spreads reproduce the near-zero control and positive treated effects.
subgroup_spec = {
    "Control Counties": (0.02, 0.31, 16),
    "Treated (Inland)": (1.32, 0.48, 16),
    "Treated (Coastal)": (2.08, 0.52, 16),
}
for group, (target, sd, n) in subgroup_spec.items():
    draws = rng.normal(size=n)
    draws = (draws - draws.mean()) / draws.std(ddof=1)
    values = target + sd * draws
    rows.extend({"panel": "subgroup", "group": group,
                 "event_time": np.nan, "value": float(v)} for v in values)

df = pd.DataFrame(rows, columns=["panel", "group", "event_time", "value"])


# -----------------------------------------------------------------------------
# Section 2: Swap Your Own Data Here
# Your CSV must contain: panel, group, event_time, value.
# Use panel="trajectory" for event-time observations; panel="subgroup" for effects.
# Uncomment the next line to replace the seeded synthetic data with your CSV.
# df = pd.read_csv("your_data.csv")
# -----------------------------------------------------------------------------


# -----------------------------------------------------------------------------
# Section 3: publication styling and plotting
# -----------------------------------------------------------------------------
plt.rcParams.update({
    "font.family": "DejaVu Sans",
    "font.size": 10.5,
    "axes.labelsize": 11.5,
    "axes.titlesize": 12.5,
    "xtick.labelsize": 9.5,
    "ytick.labelsize": 9.5,
    "axes.linewidth": 1.2,
    "pdf.fonttype": 42,
    "ps.fonttype": 42,
})

COLORS = {
    "treated": "#974457",       # muted burgundy
    "treated_band": "#E8DADD",  # pale burgundy CI ribbon
    "control": "#74838A",       # blue-gray
    "control_band": "#E2E5E7",  # pale blue-gray CI ribbon
    "inland": "#DCC697",        # warm sand
    "inland_band": "#F1E8D7",
    "coastal_band": "#D9BCC3",
    "zero": "#A5A5A5",
    "black": "#222222",
}

fig, (ax1, ax2) = plt.subplots(
    1, 2, figsize=(14.0, 5.35), gridspec_kw={"width_ratios": [1.48, 1.08]}
)
fig.subplots_adjust(left=0.075, right=0.985, bottom=0.17, top=0.86, wspace=0.27)

# Panel A: means and pointwise 95% confidence intervals.
trajectory = df[df["panel"] == "trajectory"]
for group, color, band in [
    ("Control Counties", COLORS["control"], COLORS["control_band"]),
    ("Treated Counties", COLORS["treated"], COLORS["treated_band"]),
]:
    sub = trajectory[trajectory["group"] == group]
    summary = sub.groupby("event_time")["value"].agg(["mean", "std", "count"]).reindex(event_times)
    half_width = 1.96 * summary["std"] / np.sqrt(summary["count"])
    means = summary["mean"].to_numpy()
    lower = (summary["mean"] - half_width).to_numpy()
    upper = (summary["mean"] + half_width).to_numpy()
    ax1.fill_between(event_times, lower, upper, color=band, linewidth=0, zorder=1)
    marker = "s" if group == "Control Counties" else "o"
    ax1.plot(event_times, means, color=color, linewidth=2.2, marker=marker,
             markersize=5.2, label=f"{group} (n = {county_counts[group]})", zorder=3)

ax1.axhline(0, color=COLORS["zero"], linestyle=(0, (4, 3)), linewidth=1.0, zorder=0)
ax1.axvline(-0.5, color="#E31A1C", linestyle=(0, (2, 2)), linewidth=1.0, zorder=2)
ax1.text(-0.36, 2.23, "Policy Adoption", color="#E31A1C", fontsize=9.5,
         fontstyle="italic", va="center")
ax1.set_xlim(-4.3, 5.3)
ax1.set_ylim(-0.6, 2.5)
ax1.set_xticks(event_times)
ax1.set_yticks(np.arange(-0.5, 2.51, 0.5))
ax1.set_xlabel("Years Relative to Policy Adoption (t = 0)", labelpad=15)
ax1.set_ylabel("Change in Wetland Canopy Index (SD)", labelpad=9)
ax1.set_title("A. Event-Study Treatment Effect Trajectory", loc="left",
              fontweight="bold", pad=23)
ax1.legend(loc="upper left", bbox_to_anchor=(0.015, 0.97), frameon=False,
           fontsize=9.5, handlelength=2.0, labelspacing=0.55)

# Panel B: boxplots with the individual observations jittered on top.
subgroup_order = ["Control Counties", "Treated (Inland)", "Treated (Coastal)"]
subgroup_colors = [COLORS["control"], COLORS["inland"], COLORS["treated"]]
subgroup_fills = [COLORS["control_band"], COLORS["inland_band"], COLORS["coastal_band"]]
subgroup = df[df["panel"] == "subgroup"]
box_data = [subgroup.loc[subgroup["group"] == g, "value"].to_numpy() for g in subgroup_order]
positions = np.arange(1, len(subgroup_order) + 1)

bp = ax2.boxplot(
    box_data, positions=positions, widths=0.40, patch_artist=True, showfliers=False,
    medianprops={"color": COLORS["black"], "linewidth": 1.6},
    whiskerprops={"linewidth": 1.2}, capprops={"linewidth": 1.2},
    boxprops={"linewidth": 1.2},
)
for patch, edge, fill in zip(bp["boxes"], subgroup_colors, subgroup_fills):
    patch.set_facecolor(fill)
    patch.set_edgecolor(edge)
for whisker, cap, edge in zip(bp["whiskers"], bp["caps"],
                               np.repeat(subgroup_colors, 2)):
    whisker.set_color(edge)
    cap.set_color(edge)

jitter_rng = np.random.default_rng(314)
for x, group, color in zip(positions, subgroup_order, subgroup_colors):
    vals = subgroup.loc[subgroup["group"] == group, "value"].to_numpy()
    jitter = jitter_rng.uniform(-0.14, 0.14, size=len(vals))
    ax2.scatter(x + jitter, vals, s=28, facecolor=color, edgecolor="white",
                linewidth=0.75, alpha=0.92, zorder=3)

ax2.axhline(0, color=COLORS["zero"], linestyle=(0, (4, 3)), linewidth=1.0, zorder=0)
ax2.set_xlim(0.35, 3.65)
ax2.set_ylim(-1.0, 3.5)
ax2.set_yticks(np.arange(-1, 3.1, 1))
ax2.set_xticks(positions)
ax2.set_xticklabels(["Control\nCounties", "Treated\n(Inland)", "Treated\n(Coastal)"])
ax2.set_ylabel("Mean Post-Treatment Effect (SD)", labelpad=9)
ax2.set_title("B. Post-Policy Effect by Subgroup", loc="left",
              fontweight="bold", pad=23)

# Open L-shaped publication frame on both panels.
for ax in (ax1, ax2):
    ax.spines["top"].set_visible(False)
    ax.spines["right"].set_visible(False)
    ax.spines["left"].set_color(COLORS["black"])
    ax.spines["bottom"].set_color(COLORS["black"])
    ax.tick_params(direction="out", length=4, width=1.0, color=COLORS["black"])

# Section 4: high-resolution raster and vector exports.
fig.savefig("recreated_figure.png", dpi=300, bbox_inches="tight", facecolor="white")
fig.savefig("recreated_figure.pdf", bbox_inches="tight", facecolor="white")
plt.show()
```
