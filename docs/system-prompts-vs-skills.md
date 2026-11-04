# System Prompts vs. Skills: What's the Difference?

[**⬅ Back to Main README**](../README.md)

When building AI assistants—whether in **FSU ArtesAI** or other agent platforms (like Claude Code, Antigravity, or Cursor)—you will work with two core building blocks: **System Prompts** and **Skills**.

At first glance, both look like Markdown text files containing instructions for the AI. However, separating them makes your agents **more accurate, less cluttered, and much easier to reuse**.

---

## 1. The 30-Second Mental Model

- **System Prompt (`system-prompt.md`) = *Who the Agent Is***
  Think of the System Prompt as a **job description and code of conduct**. It defines the agent's persona, tone, domain expertise, default behavior, and non-negotiable guardrails (e.g., *"Never invent citations"*, *"Generate seeded synthetic data with zero external file dependencies"*). It is active on every single message in that agent's chat.
- **Skill File (`skills/*.md`) = *A Specialized Playbook the Agent Loads on Demand***
  Think of a Skill as a **standard operating procedure (SOP) binder on a shelf**. Instead of forcing the agent to memorize 10 different workflows at once, a skill teaches the AI how to perform **one specific task or output format** (e.g., building a Methodology Matrix table, identifying research gaps, or writing a Stata `.do` file) only when you attach or trigger it.

---

## 2. Side-by-Side Comparison

| Feature | System Prompt (`system-prompt.md`) | Skill File (`skills/*.md`) |
| :--- | :--- | :--- |
| **Core Purpose** | Defines **identity, persona, tone, and permanent guardrails**. | Defines a **specific, repeatable workflow, template, or output format**. |
| **When Is It Active?** | **Always active** for every message sent to that specific Personal Agent. | **Loaded on demand** (when attached via **`+` → `Skills >`** or triggered mid-conversation). |
| **Scope in ArtesAI** | Belongs to **one Personal Agent** (`Agents → Create → 1. Instructions → Specific Instructions`; remove default `Platform Instructions` to save context). | Lives in your global library (`Settings → My Skills`) and can be attached to **any agent or regular chat**. |
| **File Structure** | Plain Markdown instructions (`Role`, `Guardrails`, `Default Workflow`). | Standard YAML frontmatter (`---` with `name:` and `description:`) followed by step-by-step Markdown instructions. |
| **Why Not Put Everything Here?** | Stuffing 5 different workflows into one huge System Prompt causes the AI to mix up instructions or lose focus ("prompt bloat"). | A skill without a good System Prompt lacks overarching domain guardrails or persona consistency. |

---

## 3. Concrete Examples from This Repository

### Example A: The "One Agent, Multiple Languages" Pattern ([`Scientific Figure Recreator`](../scientific-figure-recreator/README.md))
- **What goes in `system-prompt.md`**:
  Instructions on how to visually inspect an uploaded figure image (identifying panel ratios, axes, error bars, and hex colors) and the rule that every script must generate seeded synthetic data with zero external file dependencies.
- **What goes in `skills/`**:
  Four separate language skills (`figure-recreator-python`, `figure-recreator-r`, `figure-recreator-stata`, `figure-recreator-matlab`).
- **Why this separation works**:
  A Python researcher never needs their agent cluttered with Stata or MATLAB syntax rules, and an R user only attaches `figure-recreator-r`. Even better, you can attach `figure-recreator-r` in *other* chats whenever you want publication-styled `ggplot2` code!

### Example B: The "Core Synthesizer + Specialized Deliverables" Pattern ([`Abstract Synthesizer`](../abstract-synthesizer/README.md))
- **What goes in `system-prompt.md`**:
  The academic research persona, the strict guardrail against hallucinating external citations or DOIs, and the default thematic synthesis narrative structure.
- **What goes in `skills/`**:
  - `methodology-matrix-extractor` (`/matrix`): Builds a structured 6-column comparison table of study designs, sample sizes, metrics, and limitations.
  - `research-gap-identifier` (`/gaps`): Categorizes contradictions, under-studied contexts, and concrete follow-up research questions.
- **Why this separation works**:
  When you just want a quick thematic narrative across 3 abstracts, the agent writes a synthesis without dumping a full methodology matrix and research gap blueprint on every turn. When you *do* want the comparison matrix or gap analysis, you attach or trigger those skills.

---

## 4. Anatomy of Each File

### Anatomy of a `system-prompt.md`
A clean System Prompt is usually 15–35 lines long and answers three questions:
1. **Role & Objective**: Who are you and who are you helping?
2. **Core Guardrails**: What rules must you *never* break (e.g., no hallucinated citations, zero external data dependencies)?
3. **Default Workflow**: What should you do when the user pastes input without asking for a specific skill?

### Anatomy of a Standard `skills/*.md` File
Standard skill files work across ArtesAI and other modern agent platforms because they have two parts:

```markdown
---
name: methodology-matrix-extractor
description: Extracts study design, sample/dataset scale, variables/metrics, key findings, and limitations from provided papers into a side-by-side Markdown table. Use when the user types /matrix or asks to compare methods, datasets, or study designs across papers.
---

# Methodology Matrix Extractor (`/matrix`)

## When to Apply This Skill
Trigger this skill when the user types `/matrix` or asks to compare the methods...

## Step-by-Step Instructions
1. Review every paper or abstract provided...
2. Construct a Markdown comparison table with these exact columns...
```

- **The YAML Frontmatter (`---` block at the top)**:
  - `name`: A short kebab-case identifier (`methodology-matrix-extractor`).
  - `description`: A concise summary (**under 300 characters**) stating **what the skill does and when to use it**. The AI model reads this description to decide whether to activate the skill mid-conversation.
- **The Markdown Body (below `---`)**:
  - The step-by-step recipe, exact table columns, or coding standards the AI follows once the skill is loaded.
- **Tip for Saving Context Tokens**:
  - Keep platform/UI setup instructions out of both `system-prompt.md` and `skills/*.md`. When configuring an agent in ArtesAI, paste `system-prompt.md` into **Specific Instructions** and delete the default pre-filled **Platform Instructions** so every context token is dedicated to your task and skills.

---

## 5. Quick Decision Checklist: System Prompt or Skill?

Ask yourself these four questions when designing a new agent:

1. **Should this rule apply to 100% of messages in this agent?**
   - *Yes* (e.g., *"Never invent citations"*, *"Use an encouraging Socratic tone"*) → **Put it in `system-prompt.md`**.
   - *No, only when the user wants a specific deliverable* → **Make it a Skill**.
2. **Does this instruction define a strict multi-step template or code format?**
   - *Yes* (e.g., *"Build a 6-column Methodology Matrix table"*, *"Write a self-contained Stata `.do` script"*) → **Make it a Skill**.
3. **Could this workflow be useful inside *other* agents or general chats too?**
   - *Yes* (e.g., you might want to use `methodology-matrix-extractor` or `figure-recreator-r` in a regular ArtesAI chat without opening a special agent) → **Make it a Skill**.
4. **Are you offering mutually exclusive options (like Python vs. R vs. Stata)?**
   - *Yes* → Keep the shared logic in `system-prompt.md` and make each option its own **Skill**.

