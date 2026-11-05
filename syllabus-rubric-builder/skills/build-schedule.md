---
name: course-schedule-builder
description: Lays out a week-by-week course schedule table with topics, readings, and due dates, spacing major assignments and flagging workload clusters. Use when the user types /schedule or asks for a course calendar, weekly plan, or tentative schedule.
---

# Course Schedule Builder (`/schedule`)

## When to Apply This Skill
Trigger this skill when the user types `/schedule` or asks for a course calendar, weekly plan, or tentative schedule.

## Step-by-Step Instructions
1. Determine the number of weeks (default to 16 for a Fall or Spring semester if not given) and the meeting days.
2. Use real calendar dates only if the user gives the first day of class. Otherwise label rows `Week 1`, `Week 2`, and so on, and do not guess dates or holidays. Write `[Instructor to fill: holidays / no-class days]` once above the table.
3. Build a Markdown table with these exact columns:
   `Week | Topic | Readings / Prep | Due This Week`
4. Place topics in the order the user gave. Spread major assignments so no two large deliverables are due in the same week, and leave the final exam week free of new content.
5. Under the table, add **Workload Notes**: 2 to 4 bullets pointing out heavy weeks, any week with no graded work for a long stretch, and suggested review points.
6. Add the line: `This schedule is tentative and may change; changes will be announced in class and on Canvas.`
