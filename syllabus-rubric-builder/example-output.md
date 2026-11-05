# Example Output: Syllabus & Rubric Builder

Below is an example of what your ArtesAI **Syllabus & Rubric Builder** agent should generate when given the prompt in [`example-input.md`](./example-input.md). Your exact wording will differ by model, but the structure, placeholders, and guardrails should match.

---

# Intro to Data Analysis for the Social Sciences: Syllabus (Draft)

## Course Info
| | |
| :--- | :--- |
| **Course** | Intro to Data Analysis for the Social Sciences `[Instructor to fill: course prefix and number]` |
| **Credits** | 3 |
| **Meetings** | Monday, Wednesday, Friday, 10:10 to 11:00 AM, `[Instructor to fill: room]` |
| **Instructor** | `[Instructor to fill: name, email, office location]` |
| **Office Hours** | `[Instructor to fill: days and times]` |
| **Course Site** | Canvas |

## Course Description
Data shows up in almost every question social scientists ask, from who votes to how neighborhoods change. In this course you will learn how to turn a question into something you can measure, describe and visualize data, use probability to reason about uncertainty, and test ideas with confidence intervals, hypothesis tests, and regression. You will do all of your analysis in R, and you will practice explaining results to people who are not statisticians. No prior statistics or programming experience is needed.

## Learning Objectives
By the end of this course, you will be able to:
1. **Formulate** a research question and **identify** the variables and level of measurement needed to answer it.
2. **Summarize** data numerically and graphically, and **choose** an appropriate chart for a given variable type.
3. **Explain** how sampling method affects what a survey can tell us about a population.
4. **Construct and interpret** confidence intervals and hypothesis tests for one and two groups.
5. **Fit and interpret** simple and multiple linear regression models in R.
6. **Communicate** statistical findings, including their limitations, to a non-expert audience.
7. **Evaluate** ethical and privacy concerns when collecting and sharing data.

## Required Materials
- **Software**: R and RStudio through Posit Cloud (free account). Setup instructions will be posted on Canvas.
- **Readings**: Open-access readings posted on Canvas. There is no textbook to buy.
- **Device**: A laptop for in-class activities. `[Instructor to fill: loaner laptop options, if any]`

## Assignments & Grading
| Component | Weight | Notes |
| :--- | :--- | :--- |
| Problem Sets (4) | 20% | 5% each. All four count; the lowest score is not dropped. |
| Midterm Exam | 20% | Covers Weeks 1 to 7. |
| Final Project (teams of 3) | 30% | Proposal 3%, Written Report 20%, Presentation 7%. |
| Final Exam | 20% | `[Instructor to fill: cumulative or not]` |
| Participation & In-Class Activities | 10% | `[Instructor to fill: how participation is recorded]` |
| **Total** | **100%** | |

**Grading Scale**: `[Instructor to fill: letter grade cutoffs]`

## Course Policies
- **Late Work**: Late assignments lose 10% per day and are not accepted more than 3 days after the due date.
- **Exams**: `[Instructor to fill: make-up exam policy]`
- **Team Work**: `[Instructor to fill: how team contribution is assessed, e.g. peer evaluation]`
- **Use of AI Tools**: `[Instructor to fill: your policy on AI tools for problem sets and the project]`

## Required University Statements
`[Insert FSU required statement: Academic Honor Policy]`

`[Insert FSU required statement: Americans with Disabilities Act]`

`[Insert FSU required statement: Syllabus Change Policy]`

`[Insert any other statements your department requires]`

## Open Questions
1. Course prefix and number, room, instructor contact info, and office hours.
2. Letter grade cutoffs.
3. Is the final exam cumulative?
4. How participation is recorded.
5. Make-up exam policy.
6. Team contribution and peer evaluation policy.
7. AI tool policy.

> Want more? Type `/rubric` for an assignment rubric or `/schedule` for a week-by-week calendar.

---

# Final Project Written Report Rubric (`/rubric`)

**Assignment**: Final Project Written Report (team of 3, 6 to 8 pages). **Total: 20 points** (20% of the course grade).

| Criterion (weight) | Exemplary | Proficient | Developing | Beginning |
| :--- | :--- | :--- | :--- | :--- |
| **Research Question & Data (3 pts)** | (3) Question is specific and answerable with the chosen public dataset; variables and their measurement are clearly defined. | (2) Question is answerable but somewhat broad; most variables are defined. | (1) Question is vague or only loosely matched to the data. | (0) No clear question, or data cannot address it. |
| **Analysis in R (6 pts)** | (6) Methods fit the question and variable types; code output is correct and the steps are documented. | (4-5) Methods are appropriate with minor errors or gaps in documentation. | (2-3) Methods are partly inappropriate or contain errors that affect results. | (0-1) Analysis is missing or does not address the question. |
| **Interpretation (5 pts)** | (5) Results are explained correctly in plain language, including what intervals, p-values, or coefficients mean in context. | (3-4) Interpretation is mostly correct but uses jargon or skips context. | (1-2) Interpretation has significant errors (e.g., treats correlation as causation). | (0) Results are reported without interpretation. |
| **Limitations & Ethics (3 pts)** | (3) Identifies specific limits of the data and sampling, and discusses at least one ethical or privacy issue. | (2) Lists limitations, but they are generic. | (1) Mentions limitations in one sentence. | (0) No limitations discussed. |
| **Visuals & Writing (3 pts)** | (3) Charts are well chosen and labeled; writing is organized and readable for a non-expert. | (2) Charts and writing are clear with minor issues. | (1) Charts are hard to read or writing is disorganized. | (0) No charts, or the report is hard to follow throughout. |

**Total: 3 + 6 + 5 + 3 + 3 = 20 points.**

## Learning Objective Alignment
- Research Question & Data: Objectives 1, 3
- Analysis in R: Objectives 2, 4, 5
- Interpretation: Objectives 4, 5, 6
- Limitations & Ethics: Objectives 3, 7
- Visuals & Writing: Objectives 2, 6

## Student Checklist
- [ ] Can someone outside this class tell what our question is from the first paragraph?
- [ ] Did we define every variable we used and say how it was measured?
- [ ] Does every chart have a title, labeled axes, and units?
- [ ] Did we explain every result in plain words, not just paste R output?
- [ ] Did we avoid claiming cause and effect from a correlation?
- [ ] Did we name at least two specific limitations and one ethical issue?

---

# Tentative Course Schedule (`/schedule`)

`[Instructor to fill: holidays / no-class days]`

| Week | Topic | Readings / Prep | Due This Week |
| :--- | :--- | :--- | :--- |
| 1 | Why data? Asking good questions | Canvas reading 1; create Posit Cloud account | |
| 2 | Variables and measurement | Canvas reading 2 | |
| 3 | Describing data: center, spread, plots | Canvas reading 3 | |
| 4 | Describing data (continued), plots in R | R lab handout | Problem Set 1 |
| 5 | Surveys and sampling | Canvas reading 4 | |
| 6 | Probability basics | Canvas reading 5 | Problem Set 2 |
| 7 | Confidence intervals | Canvas reading 6 | Project teams formed |
| 8 | Review and Midterm | Midterm study guide | **Midterm Exam** |
| 9 | Hypothesis tests | Canvas reading 7 | Project Proposal |
| 10 | Comparing two groups | Canvas reading 8 | |
| 11 | Correlation and simple regression | Canvas reading 9 | Problem Set 3 |
| 12 | Multiple regression | Canvas reading 10 | |
| 13 | Communicating results, making good charts | Canvas reading 11 | Problem Set 4 |
| 14 | Ethics and privacy with data | Canvas reading 12 | **Final Project Report** |
| 15 | Team presentations | Presentation slides | **Presentations** |
| 16 | Final exam week (no new content) | Final study guide | **Final Exam** |

## Workload Notes
- Weeks 14 and 15 are the heaviest for students (report, then presentations). Consider making Week 14 a lighter reading week.
- Problem Set 4 (Week 13) lands one week before the report. You could move it to Week 12 to give teams more room.
- Week 7 (confidence intervals) has no graded work right before the midterm; a short ungraded practice quiz would make a good review point.
- Week 9 has both a new topic and the project proposal. The proposal is only 3%, so this is manageable.

This schedule is tentative and may change; changes will be announced in class and on Canvas.
