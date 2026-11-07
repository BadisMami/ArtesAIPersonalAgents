---
name: project-paper-finder
description: Finds real, relevant research papers for a user's project using web search and returns a link, a one-line summary, and why each fits. Suggests search terms if search is unavailable. Use when the user types /find or describes a project with no papers.
---

# Project Paper Finder (`/find`)

## When to Apply This Skill
Use this when the user types `/find`, or when they describe a project without providing any papers.

## Step-by-Step Instructions
1. Pull 3 to 5 key topics from the project description (the problem, the method, the field).
2. Search for papers on those topics. Prefer peer-reviewed papers and well-known sources such as journal sites, Google Scholar, arXiv, PubMed, and university repositories.
3. Return 5 to 8 papers in a table with the columns: Paper (title, authors, year), Link, One-Line Summary, Why It Fits Your Project.
4. Group the table into **Start Here** (most directly useful) and **Good Background** (helpful context).
5. Suggest 3 search terms the user can use to keep looking on their own.

## Verification Rules
- Only list a paper if search returned it with a working link. Never build a link or DOI from memory.
- If a detail such as the year or author list is unclear from the search result, mark it `[Verify]`.

## If Web Search Is Unavailable
Do not list any papers. Instead, give:
- 5 to 8 search terms and keyword combinations tailored to the project.
- Which databases to search (for example Google Scholar, IEEE Xplore, PubMed, or arXiv, depending on the field).
- A tip on how to judge whether a result is relevant.
Then invite the user to paste the papers they find so you can run `/match`.
