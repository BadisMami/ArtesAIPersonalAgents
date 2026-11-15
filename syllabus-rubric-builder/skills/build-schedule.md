---
name: course-schedule-builder
description: Lays out a week-by-week course schedule table with topics, readings, and due dates, spacing major assignments and flagging workload clusters. Use when the user types /schedule or asks for a course calendar, weekly plan, or tentative schedule.
---

# Course Schedule Builder (`/schedule`)

## When to Apply This Skill
Trigger this skill when the user types `/schedule` or asks for a course calendar, weekly plan, or tentative schedule.

## Step-by-Step Instructions
1. Determine the number of weeks (default to 15 weeks + Final Exam week = 16 weeks for an FSU Fall/Spring semester, or 6/12 weeks for FSU Summer A/B/C if specified) and the meeting days.
2. Use real calendar dates only if the user gives the first day of class. Otherwise label rows `Week 1`, `Week 2`, and so on, and do not guess dates or holidays. Write `[Instructor to fill (FSU Required): official FSU holidays / no-class days (e.g., Labor Day, Homecoming, Veterans Day, Thanksgiving / Spring Break) and Final Exam date/time from registrar schedule]` once above the table.
3. Group weeks into 3–4 **Thematic Units** (Backward Design) and build a Markdown table with these exact columns:
   `Week | Unit & Topic | Readings / Prep & In-Class Activity | Due This Week`
4. Place topics in the order the user gave. Scaffold formative practice before high-stakes summative assessments, spread major assignments so no two large deliverables are due in the same week, and leave the final exam week free of new content.
5. Under the table, add **Workload & Scaffolding Notes**: 2 to 4 bullets pointing out heavy weeks, any long stretch without formative feedback before a major exam/project, and suggested review points.
6. Add the FSU Syllabus Change Policy reminder line: `Except for changes that substantially affect implementation of the evaluation (grading) statement, this schedule is a guide for the course and is subject to change with advance notice in class and on Canvas.`
