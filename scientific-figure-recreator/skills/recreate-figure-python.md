---
name: figure-recreator-python
description: Generates a self-contained Python script (matplotlib, seaborn, numpy, pandas) with seeded synthetic data to recreate an uploaded scientific figure locally. Use when the user attaches this skill, types /python, or asks to recreate a figure in Python.
---

# Recreate Figure in Python (`/python`)

## When to Apply This Skill
Use this skill whenever it is attached to the conversation, when the user types `/python`, or when the user asks to recreate an uploaded scientific figure using Python.

## Python Coding Requirements
Write a single, self-contained Python 3 script (`recreate_figure.py`) using only standard scientific libraries (`numpy`, `pandas`, `matplotlib`, and optionally `seaborn` or `scipy.stats`):

1. **Section 1: Seeded Synthetic Data Generator (`np.random.default_rng(42)`)**:
   - Build a clean `pandas.DataFrame` (`df`) whose group means, standard deviations/slopes, and sample sizes closely reproduce the visual patterns in the uploaded figure.
2. **Section 2: "Swap Your Own Data Here" Block**:
   - Include a commented-out `df = pd.read_csv("your_data.csv")` block listing the exact column names expected by the plotting code.
3. **Section 3: Publication Styling & Plotting**:
   - Use `plt.rcParams` for clean publication typography (sans-serif font, legible tick/label sizes).
   - Use `fig, axes = plt.subplots(...)` or `GridSpec` for multi-panel figures, adding bold panel letters (`A`, `B`) via `ax.set_title(..., loc="left", fontweight="bold")` or `ax.text(...)`.
   - Apply the exact extracted hex colors (`#RRGGBB`), error bars / shaded confidence bands (`ax.fill_between` or `ax.errorbar`), reference lines (`ax.axhline` / `ax.axvline`), and clean spines (`ax.spines[['top', 'right']].set_visible(False)`).
4. **Section 4: High-Resolution Local Export**:
   - Save both `recreated_figure.png` (`dpi=300, bbox_inches="tight"`) and vector `recreated_figure.pdf` (`bbox_inches="tight"`), then call `plt.show()`.
5. Provide the terminal command to install requirements (`pip install numpy pandas matplotlib seaborn`) and run the script.
