---
name: project-paper-matcher
description: Explains uploaded papers in plain language, connects each one to the user's project, flags what does not apply, and ranks the papers by relevance. Use when the user types /match or provides both a project description and papers.
---

# Project Paper Matcher (`/match`)

## When to Apply This Skill
Activate this workflow whenever the user types `/match` or asks to evaluate, compare, and rank uploaded or pasted papers against their project description.

## Step-by-Step Instructions
1. **Restate the Project**: Summarize the user's project goal, tools/methods, and constraints in 1–2 sentences so the user can confirm you understood it.
2. **Create a Paper Card for Each Provided Paper**: Base your analysis strictly on what the paper and project description actually state (if only an abstract or excerpt is provided, note that the full text may change the assessment):
   - **What it is about**: 2–3 plain-language sentences summarizing the study. Define any technical terms in parentheses.
   - **How it helps your project**: 2–4 bullets, each tied to a specific part of the user's project (e.g., a method to borrow, a benchmark to compare against, or a failure mode to avoid).
   - **What does not apply**: 1–3 bullets flagging aspects of the paper that do not fit the user's project and why.
   - **Relevance score**: `High`, `Medium`, or `Low`, with a one-sentence justification.
3. **Build a Ranking Table**: Construct a Markdown table with these exact columns, ordered from most to least relevant:
   `Rank | Paper (Authors, Year) | Relevance Score | Best Use for Your Project`
4. **Where to Start & Next Steps**: End with a **Where to Start** recommendation (which paper and section to read first) and 2 concrete next steps the user can take (including offering `/find` if they need papers to fill a remaining gap).
