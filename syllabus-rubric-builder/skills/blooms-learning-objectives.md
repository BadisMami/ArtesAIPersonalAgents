---
name: blooms-learning-objectives-generator
description: Upgrades vague syllabus goals ("understand", "learn") into measurable Bloom's Taxonomy learning objectives paired with assessments and in-class practice. Use when the user types /objectives or asks to write, audit, or align course or module learning outcomes.
---

# Bloom's Learning Objectives Generator (`/objectives`)

## When to Apply This Skill
Trigger this skill when the user types `/objectives` or asks to write, audit, or refine course-level or module-level learning outcomes for their FSU syllabus.

## Step-by-Step Instructions
1. If the user provides existing draft objectives containing vague, unobservable verbs (*understand, learn, know, be familiar with, appreciate*), display a **"Before → After" Verb Upgrade List** explaining why each replacement verb is observable and measurable.
2. Generate **5–7 Course Learning Objectives** spanning multiple levels of Bloom's Revised Taxonomy (`Apply`, `Analyze`, `Evaluate`, `Create`), calibrated to the course level (lower-division undergrad, upper-division undergrad, or graduate).
3. Present an **Alignment Matrix** (Markdown table) with these exact columns:
   `Objective # & Measurable Outcome ("By the end of this course, you will be able to...") | Bloom's Taxonomy Level | Summative Assessment (Graded) | In-Class / Formative Practice`
4. If any assessment weight or format is not yet defined in the instructor's notes, flag it with `[Instructor to fill: ...]` so nothing is invented.
