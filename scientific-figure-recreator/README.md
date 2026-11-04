# Scientific Figure Recreator Agent

> **One-Sentence Summary**: Takes a screenshot or image of a figure from a research paper and generates a complete, self-contained script (with realistic synthetic data) to reproduce that exact figure style on your local computer in **Python**, **R**, **Stata**, or **MATLAB**.

[**⬅ Back to Main Catalog**](../README.md)

---

## Overview

We have all seen a figure in a journal article—a clean multi-panel event-study plot, a raincloud distribution, or a grouped regression coefficient plot—and wished we had the exact code to make that style of figure for our own data.

The **Scientific Figure Recreator** lets you drag-and-drop a screenshot of any published figure into ArtesAI. The agent deconstructs the visual layout, axes, error bars, annotations, and hex color palette, and then—based on which **Language Skill** you attach (`Python`, `R`, `Stata`, or `MATLAB`)—writes a self-contained script that **generates realistic synthetic data matching the figure** and saves a high-resolution (`300 DPI` PNG + vector PDF) plot on your local machine. Every generated script includes a clearly marked **`"SWAP YOUR OWN CSV HERE"`** block so you can plug in your real dataset in one line.

- **Recommended Model in ArtesAI**: `OpenAI → gpt-5.4` / `gpt-6-luna` or `Anthropic → claude-sonnet-5` / `claude-opus-4-7` (Creativity: `Low`)
- **Estimated Setup Time**: ~5 minutes

---

## How to Build This Agent & Its Skills in ArtesAI

In ArtesAI, **create your preferred Language Skill(s) first** under your account **Settings → My Skills** (Part 1). That way, while you are building the **Personal Agent** (Part 2), you can immediately attach your preferred language skill (`Python`, `R`, `Stata`, or `MATLAB`) inside the right-hand **Preview** chat pane and test it with a figure screenshot before clicking **Create** (Part 3).

### Part 1: Create Your Preferred Language Skill(s) First (`Settings → My Skills`)

You can add just the language(s) you use in your research, or all four:

1. Click your **Profile / Account box** at the bottom-left of the maroon FSU sidebar and click **Settings**.
2. Click **My Skills** on the left, then click **`+ New Skill`** in the top-right corner.
3. Open each standard skill file you want below and copy its parts into the **Create Skill** modal (**Name** = `name:` from the top `---` block, **Description** = `description:` from the top `---` block, leave **Always On** unchecked/`Ad Hoc`, and paste the Markdown body below `---` into the dark editor box):
   - **[`figure-recreator-python`](./skills/recreate-figure-python.md)** (`/python`): Recreates the figure using `matplotlib`, `seaborn`, `numpy`, and `pandas`.
   - **[`figure-recreator-r`](./skills/recreate-figure-r.md)** (`/r`): Recreates the figure using `ggplot2`, `dplyr`, `tidyr`, and `patchwork`.
   - **[`figure-recreator-stata`](./skills/recreate-figure-stata.md)** (`/stata`): Recreates the figure as a self-contained Stata `.do` file using `twoway` graph layers.
   - **[`figure-recreator-matlab`](./skills/recreate-figure-matlab.md)** (`/matlab`): Recreates the figure as a self-contained MATLAB `.m` script using `tiledlayout` and `exportgraphics`.

---

### Part 2: Create the Personal Agent

#### 0. Launch "Quick Create"
1. In the left maroon FSU sidebar, click **Explore Agents** (or switch to the **Agents** tab).
2. Under **My Agents** (*Agents created by me*), click the **`+ Create`** button next to the **My Agents** heading (or click the dashed **`+ Create`** card).
3. In the **Quick Create** popup box, enter **`Scientific Figure Recreator`** as the **Agent Name** and click **`Let's go`**.

#### 1. Instructions (System Prompt)
1. Open [`system-prompt.md`](./system-prompt.md), copy the text, and paste it into the **Specific Instructions** field.
2. **Remove the Platform Instructions**: Delete/clear the default pre-filled **Platform Instructions** to save on context tokens.

#### 2. Name & Identity
In the **Name & Identity** panel, copy and paste the fields below (you'll see them update live in the right-hand **Preview** pane):

- **Name**:
  ```text
  Scientific Figure Recreator
  ```
- **Short Description**:
  ```text
  Takes a screenshot of a figure from a paper and writes runnable code + synthetic data to recreate the plot locally in Python, R, Stata, or MATLAB.
  ```
- **Welcome Message** *(replace the default "Welcome to the Chat!" text in the rich-text editor box)*:
  ```text
  Welcome to the Scientific Figure Recreator!

  1. Click the "+" button in the chat bar -> "Add Files & Images" to upload a screenshot of a figure from a paper.
  2. Click the "+" button -> "Skills >" to attach your preferred coding language skill:
     • figure-recreator-python (/python) — Matplotlib + Seaborn + Pandas
     • figure-recreator-r (/r) — ggplot2 + tidyverse + patchwork
     • figure-recreator-stata (/stata) — Stata .do file (twoway graphs)
     • figure-recreator-matlab (/matlab) — MATLAB .m script (tiledlayout)

  I will deconstruct the figure's design, generate realistic synthetic data, and give you a self-contained script you can run on your computer (with a 1-line block to swap in your own CSV!).
  ```

#### 3. Knowledge & Tools *(Optional)*
If your journal or lab has a specific figure style guide (e.g., *Nature*, *Science*, *JAMA*, or FSU Garnet & Gold presentation colors), you can upload it here.

#### 4. Capabilities & Model
In the **Capabilities & Model** tab, configure the toggles and model as follows:

| Setting | Recommended Value | Why? |
| :--- | :--- | :--- |
| **Image Creation** | **OFF** | Keep **OFF**! We want the agent to write **reproducible local code** (`Python`/`R`/`Stata`/`MATLAB`), not generate an AI raster image. |
| **Add Files & Images** | **ON** *(Required)* | **Must be ON** so you can upload screenshots or images of published figures into the chat! |
| **Web Search** | **OFF** | Not needed; standard plotting libraries are built into the model's training weights. |
| **Generate Artifacts** | **ON** | Places the generated `.py`, `.R`, `.do`, or `.m` script in a dedicated side-by-side code panel for one-click copying. |
| **Model (`Change` button)** | • **OpenAI**: `gpt-5.4` *(Default)* or `gpt-6-luna` *(set **Reasoning Effort**: `Medium`/`High`)*<br>• **Anthropic**: `claude-sonnet-5` or `claude-opus-4-7` *(set **Creativity**: `Low`)* | Both OpenAI (`gpt-5.4`/`gpt-6-luna`) and Anthropic (`claude-sonnet-5`/`claude-opus-4-7`) have strong vision capabilities for reading axes, legends, and hex color palettes from figure screenshots. |

#### 5. Starter Prompts *(Optional)*
In **5. Starter Prompts**, click **Add Starter Prompt** and enter the **Title** and **Prompt** fields below, then click **Create**:

| Title | Prompt |
| :--- | :--- |
| `Recreate Figure with Attached Skill` | `Recreate the figure I upload next using my attached language skill (/python, /r, /stata, or /matlab) with realistic synthetic data.` |
| `Recreate Figure in Python (/python)` | `Deconstruct the visual design of the figure I upload next and generate a self-contained Python (matplotlib/seaborn) script (/python) with synthetic data.` |
| `Recreate Figure in R ggplot2 (/r)` | `Deconstruct the visual design of the figure I upload next and generate a self-contained R (ggplot2/patchwork) script (/r) with synthetic data.` |

---

### Part 3: Test with a Figure Image & Language Skill in the Preview Pane
1. In the **Preview** chat pane on the right side of the Agent Builder (or after clicking **Create**):
   - Click **`+` → `Add Files & Images`** and upload [`sample-paper-figure.png`](./sample-paper-figure.png) included in this folder (or any figure screenshot from a paper on your computer).
   - Click **`+` → `Skills >`** and attach your preferred language skill (e.g., `figure-recreator-python` or `figure-recreator-r`).
2. Paste the prompt from [`example-input.md`](./example-input.md) and compare your result with [`example-output.md`](./example-output.md).
3. Click **Create** at the bottom of the screen to save your **Scientific Figure Recreator** agent!

---

## Files in This Folder

| File | Purpose |
| :--- | :--- |
| [`system-prompt.md`](./system-prompt.md) | Core visual deconstruction and synthetic-data generation instructions |
| [`skills/recreate-figure-python.md`](./skills/recreate-figure-python.md) | Skill for Python (`matplotlib` + `seaborn` + `pandas`) |
| [`skills/recreate-figure-r.md`](./skills/recreate-figure-r.md) | Skill for R (`ggplot2` + `tidyverse` + `patchwork`) |
| [`skills/recreate-figure-stata.md`](./skills/recreate-figure-stata.md) | Skill for Stata (`.do` file with `twoway` graph layers) |
| [`skills/recreate-figure-matlab.md`](./skills/recreate-figure-matlab.md) | Skill for MATLAB (`.m` script with `tiledlayout`) |
| [`sample-paper-figure.png`](./sample-paper-figure.png) | Ready-to-upload sample publication figure image to test the agent |
| [`example-input.md`](./example-input.md) | Sample prompt to pair with `sample-paper-figure.png` |
| [`example-output.md`](./example-output.md) | Sample output showing visual deconstruction + Python, R, and Stata scripts |

---

## Modify & Play: Ideas to Try

1. **Test the Same Figure Across Multiple Languages**:
   - *Try this*: Upload [`sample-paper-figure.png`](./sample-paper-figure.png), attach `figure-recreator-python` and `figure-recreator-r` in the same chat, and ask the agent to output both side-by-side so you can compare how `seaborn` vs. `ggplot2` builds the exact same visual!
2. **Swap the Palette to Accessibility / Colorblind-Safe Okabe-Ito or FSU Colors**:
   - *Try this*: After the agent recreates the paper's original colors, reply: *"Now keep the exact same layout, but update the color palette to the colorblind-safe Okabe-Ito palette (or FSU Garnet `#782F40` and Gold `#CEB888`)."*
3. **Upload a Hand-Drawn Whiteboard Sketch**:
   - *Try this*: You don't even need a published paper! Snap a photo of a rough figure sketch on a whiteboard or notepad, upload it with **`+` → `Add Files & Images`**, and attach your language skill to turn your sketch into publication-ready code.

