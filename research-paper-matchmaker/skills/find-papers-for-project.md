---
name: project-paper-finder
description: Finds real, relevant research papers for a user's project using web search and returns a link, a one-line summary, and why each fits. Suggests search terms if search is unavailable. Use when the user types /find or describes a project with no papers.
---

# Project Paper Finder (`/find`)

## When to Apply This Skill
Activate this workflow whenever the user types `/find` or describes a research project without providing papers and asks for literature recommendations.

## Step-by-Step Instructions
1. **Extract Search Themes**: Pull 3–5 key topics from the user's project description (the core problem, the method/tools, and the application domain).
2. **Search or Provide Search Strategy**:
   - **When Web Search Is Enabled**:
     - Search for peer-reviewed papers and reputable preprints (journal sites, Google Scholar, arXiv, PubMed, IEEE Xplore, or university repositories).
     - **Strict Verification Rule**: Only list a paper if web search returned it with a working link. Never construct a citation, URL, or DOI from memory; if any metadata detail is unclear from search results, mark it `[Needs Verification]`.
     - Present 5–8 verified papers in a Markdown table grouped into **Start Here (Direct Method/Problem Fit)** and **Good Background (Helpful Context)** with these exact columns:
       `Paper (Title, Authors, Year) | Link | One-Line Summary | Why It Fits Your Project`
   - **When Web Search Is Off / Unavailable**:
     - Do **not** list or guess paper titles from memory. Instead, provide:
       1. **5–8 copy-pasteable search queries** (with Boolean `AND`/`OR` combinations) tailored to the project's sub-problems.
       2. **Recommended databases** for the user's discipline (e.g., Google Scholar, Web of Science, PubMed, IEEE Xplore, arXiv).
       3. **Inclusion/Exclusion Checklist**: 2–3 quick criteria for judging whether a search hit actually fits their setup.
3. **Concrete Next Steps**: End with 2 concrete next steps, including 3 follow-up search terms and an invitation to upload or paste the best papers they find to run `/match`.
