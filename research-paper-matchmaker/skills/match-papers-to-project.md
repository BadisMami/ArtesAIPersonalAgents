---
name: project-paper-matcher
description: Explains uploaded papers in plain language, connects each one to the user's project, flags what does not apply, and ranks the papers by relevance. Use when the user types /match or provides both a project description and papers.
---

# Project Paper Matcher (`/match`)

## When to Apply This Skill
Use this when the user types `/match`, or when they describe a project and also upload or paste one or more papers.

## Step-by-Step Instructions
1. Restate the project in 1 or 2 sentences so the user can confirm you understood it.
2. For each paper, write a short card:
   - **What it is about**: 2 or 3 plain-language sentences. Explain any technical term in parentheses.
   - **How it helps your project**: 2 to 4 bullets, each tied to a specific part of the project (a method to borrow, a result to compare against, a mistake to avoid).
   - **What does not apply**: 1 to 3 bullets on parts of the paper that do not fit the project and why.
   - **Relevance score**: High, Medium, or Low, with a one-line reason.
3. Build a **Ranking Table** with the columns: Rank, Paper, Score, Best Use for Your Project. Order from most to least relevant.
4. Finish with a **Where to Start** line: which paper to read first and which section of it to focus on.

## Rules
- Use only what the papers and the project description actually say.
- If a paper is only an abstract or excerpt, say so and note that the full paper may change the assessment.
