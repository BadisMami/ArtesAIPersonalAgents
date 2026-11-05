---
name: assignment-rubric-builder
description: Builds an analytic grading rubric (criteria by performance levels with point ranges) for one assignment, aligned to the course learning objectives. Use when the user types /rubric or asks for a rubric, grading criteria, or scoring guide.
---

# Assignment Rubric Builder (`/rubric`)

## When to Apply This Skill
Trigger this skill when the user types `/rubric` or asks for a rubric, grading criteria, or a scoring guide for an assignment.

## Step-by-Step Instructions
1. Identify the assignment, its point value, and the learning objectives it assesses. If the point value is missing, use `[Instructor to fill: total points]` and show criteria as percentages.
2. Choose 4 to 6 criteria. Each criterion must describe something a grader can observe in the submitted work (not effort or attitude).
3. Build a Markdown table with these exact columns:
   `Criterion (weight) | Exemplary | Proficient | Developing | Beginning`
   - Each cell is one or two short sentences describing what the work looks like at that level.
   - Show the point range for each level in the header or cell (for example, `Exemplary (18-20)`).
4. Confirm the criterion weights add up to the assignment total. State the total under the table.
5. Add a **Learning Objective Alignment** list mapping each criterion to the objective(s) it measures.
6. Add a **Student Checklist**: 4 to 6 yes/no questions students can use to self-check before submitting.
