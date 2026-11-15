# Syllabus & Rubric Builder

> **One-Sentence Summary**: Turns rough course notes into an FSU Simple Syllabus draft, measurable Bloom's Taxonomy learning objectives, an `ai.fsu.edu`-aligned generative AI policy, analytic assignment rubrics, and a week-by-week schedule—flagging every FSU-required field the instructor still needs to fill in.

[**⬅ Back to Main Catalog**](../README.md)

---

## Overview

Designing a new course—or updating an existing one for FSU's **Simple Syllabus** (`fsu.simplesyllabus.com` / Canvas)—requires aligning measurable learning objectives, required textbook entries, grading scales, generative AI policies, assignment rubrics, and a 16-week calendar.

The **Syllabus & Rubric Builder** combines **Backward Design** principles with strict grounding: it turns your rough notes (topics, readings, assignments, grading weights, meeting days) into clean, student-facing drafts while explicitly separating **FSU Required Instructor-Filled Fields** from **Pre-Populated / Locked FSU Institutional Policy Statements** (`fda.fsu.edu`) so it never invents course facts or rewrites university policy text.

- **Recommended Model in ArtesAI**: `Anthropic (claude-sonnet-5)` or `OpenAI (gpt-5.6-luna)`
- **Estimated Setup Time**: ~5 minutes

---

## Reference: FSU Simple Syllabus Requirements (What You Fill In vs. Pre-Populated)

Under **FSU Regulation 5.098** and **Florida Board of Governors (BOG) Regulation 8.003**, syllabi are published in **Simple Syllabus** (with required textbook/syllabus information due **at least 45 days before the start of the term**). This agent tracks both categories below and flags missing instructor items under **Open Questions**:

| Simple Syllabus Section | Who Provides It? | What the Instructor Needs to Know / Fill In |
| :--- | :--- | :--- |
| **1. Instructor Information** | **Instructor Fills** *(Name & FSU email auto-populate)* | Must fill in **Department / Office Location** (faculty may enter their Department name or `"N/A"` if they do not have a private office), **Office Hours**, and **Contact Preferences**. |
| **2. Course Information** | **Auto-Populated + Instructor Verifies** | Verify meeting days, times, building/room, delivery mode, and prerequisites. *(Note: Simple Syllabus does not merge cross-listed Canvas sections—each section must be submitted individually).* |
| **3. Course Objectives** | **Instructor Fills (Required)** | Must enter **actionable, observable, measurable** student learning outcomes (no vague verbs like *understand, learn, appreciate*). Use `/objectives` to upgrade rough goals. |
| **4. Required Textbooks & Materials** | **Instructor Fills (Required — 45-Day Rule)** | Requires an active entry via the Simple Syllabus textbook lookup (ISBN, title, author, edition, required chapters or `"ALL"`). **Even if no textbook is used**, you must select *"No textbook required"* and enter `"N/A"`. |
| **5. Evaluation & Grading Scale** | **Instructor Fills (Required)** | Assignment weights totaling **100%**, late/make-up policies, and explicit **letter-grade percentage cutoffs** (`A`, `A-`, `B+`, etc.). FSU grade appeals rely strictly on the evaluation standard published in the syllabus at the start of the term. |
| **6. Generative AI Course Policy** | **Instructor Fills (`ai.fsu.edu`)** | Strongly recommended by the FSU Office of Faculty Development and Advancement (`fda.fsu.edu` / `ai.fsu.edu`) because AI rules vary by course under the Academic Honor Policy. Use `/ai-policy` to generate a Traffic-Light policy. |
| **7. Weekly Schedule & Due Dates** | **Instructor Fills (Required)** | Week-by-week topical outline, readings, major assignment due dates, official FSU holidays, and Registrar Final Exam date/time. Use `/schedule` to generate. |
| **8. Mandatory FSU Policy Statements** | **Pre-Populated & Locked in Simple Syllabus** *(or copy verbatim from `fda.fsu.edu`)* | **University Attendance Policy**, **Academic Honor Policy**, **Americans with Disabilities Act (ADA / OAS)**, and **State University System Free Expression Statement** are locked in Simple Syllabus. Recommended `fda.fsu.edu` blocks include **Syllabus Change Policy**, **Confidential Campus Resources (VAP, CAPS, UHS)**, **Free Tutoring from FSU (`tutoring.fsu.edu`)**, and **Recording Class Lectures**. |

---

## How to Build This Agent & Its Skills in ArtesAI

In ArtesAI, **create the companion Skills first** under your account **Settings → My Skills** (Part 1). That way, while you build the **Personal Agent** (Part 2), you can immediately attach and test the skills inside the right-hand **Preview** chat pane before clicking **Create** (Part 3).

### Part 1: Create the Companion Skills First (`Settings → My Skills`)

1. Click your **Profile / Account box** at the bottom-left of the maroon FSU sidebar and click **Settings**.
2. Click **My Skills** on the left, then click **`+ New Skill`** in the top-right corner.
3. Open each standard skill file below and copy its parts into the **Create Skill** modal (**Name** = `name:` from the top `---` block, **Description** = `description:` from the top `---` block, leave **Always On** unchecked/`Ad Hoc`, and paste the Markdown body below `---` into the dark editor box):
   - **[`blooms-learning-objectives-generator`](./skills/blooms-learning-objectives.md)** (`/objectives`): Upgrades vague syllabus goals ("understand", "learn") into measurable Bloom's Taxonomy learning objectives paired with summative and formative assessments.
   - **[`course-ai-policy-drafter`](./skills/ai-policy-drafter.md)** (`/ai-policy`): Drafts an FSU-aligned **Simple Syllabus** generative AI policy following **[ai.fsu.edu](https://ai.fsu.edu)** (Green/Yellow/Red Traffic-Light table, FSU Academic Honor Policy mapping for plagiarism/cheating/falsification, and FSU-approved enterprise tools like ArtesAI, Copilot, and Gemini).
   - **[`assignment-rubric-builder`](./skills/build-rubric.md)** (`/rubric`): Builds a 4-level analytic grading rubric (`Exemplary`, `Proficient`, `Developing`, `Beginning`) with point ranges, objective alignment, and a student self-check list.
   - **[`course-schedule-builder`](./skills/build-schedule.md)** (`/schedule`): Lays out a backward-designed week-by-week course schedule, spacing major assignments and flagging workload clusters and FSU holiday placeholders.

---

### Part 2: Create the Personal Agent

#### 0. Launch "Quick Create"
1. In the left maroon FSU sidebar, click **Explore Agents** (or switch to the **Agents** tab).
2. Under **My Agents** (*Agents created by me*), click the **`+ Create`** button next to the **My Agents** heading (or click the dashed **`+ Create`** card).
3. In the **Quick Create** popup box, enter **`Syllabus & Rubric Builder`** as the **Agent Name** and click **`Let's go`**.

#### 1. Instructions (System Prompt)
1. Open [`system-prompt.md`](./system-prompt.md), copy the text, and paste it into the **Specific Instructions** field.
2. **Remove the Platform Instructions**: Delete/clear the default pre-filled **Platform Instructions** to save on context tokens.

#### 2. Name & Identity
In the **Name & Identity** panel, copy and paste the fields below:

- **Name**:
  ```text
  Syllabus & Rubric Builder
  ```
- **Short Description**:
  ```text
  Turns rough course notes into an FSU Simple Syllabus draft, measurable Bloom's objectives, ai.fsu.edu Traffic-Light AI policies, analytic rubrics, and a 16-week schedule.
  ```
- **Welcome Message** *(replace the default "Welcome to the Chat!" text in the rich-text editor box)*:
  ```text
  Welcome to the Syllabus & Rubric Builder!

  Paste your rough course notes below (topics, rough goals, readings, assignments, grading weights, meeting days), and I will draft an FSU Simple Syllabus—flagging every required FSU field you still need to fill in.

  How to Attach Companion Skills (Click "+" in the chat bar -> "Skills >"):
  • blooms-learning-objectives-generator (/objectives) — Upgrade vague goals into measurable Bloom's Taxonomy objectives & assessment alignment
  • course-ai-policy-drafter (/ai-policy) — Draft a Green/Yellow/Red Traffic-Light generative AI syllabus policy aligned with ai.fsu.edu
  • assignment-rubric-builder (/rubric) — Build a 4-level analytic grading rubric for an assignment
  • course-schedule-builder (/schedule) — Build a 16-week course calendar with workload notes
  ```

#### 3. Knowledge & Tools *(Optional)*
If your department or college has a supplemental syllabus template or standard grading scale, upload it here so the agent automatically incorporates your department's required sections and cutoffs.

#### 4. Capabilities & Model
In the **Capabilities & Model** tab, configure the toggles and model as follows:

| Setting | Recommended Value | Why? |
| :--- | :--- | :--- |
| **Image Creation** | **OFF** | Not needed for text-based course documents. |
| **Add Files & Images** | **ON** | Lets you upload a department syllabus template or past semester's syllabus PDF for modernization. |
| **Web Search** | **OFF** *(or ON)* | Keep **OFF** to ground drafts strictly in your notes, or toggle **ON** to look up current FSU academic calendar dates or OER textbooks. |
| **Generate Artifacts** | **ON** | Renders the Simple Syllabus draft, Bloom's matrix, AI policy, rubric tables, and 16-week schedule in a side-by-side panel ready to copy into Canvas. |
| **Model (`Change` button)** | • **Anthropic**: `claude-sonnet-5` *(set **Creativity**: `Low`)*<br>• **OpenAI**: `gpt-5.6-luna` *(Default, `128,000` max tokens, set **Reasoning Effort**: `Auto`)* | A lower creativity setting keeps the draft grounded in your notes and prevents invented policy text or dates, while high max output tokens ensure full 16-week schedules never get cut off. |

#### 5. Starter Prompts *(Optional)*
In **5. Starter Prompts**, click **Add Starter Prompt** and enter the fields below:

| Title | Prompt |
| :--- | :--- |
| `Build My FSU Simple Syllabus` | `Build an FSU Simple Syllabus draft from the course notes I paste next and flag any required FSU fields I still need to fill in.` |
| `Upgrade Learning Objectives (/objectives)` | `Run /objectives to rewrite my rough course goals into measurable Bloom's Taxonomy learning objectives mapped to assessments.` |
| `Draft FSU AI Policy (/ai-policy)` | `Run /ai-policy to create a Green/Yellow/Red Traffic-Light generative AI syllabus policy aligned with ai.fsu.edu.` |
| `Build Assignment Rubric (/rubric)` | `Run /rubric on the assignment I describe next.` |
| `Build 16-Week Schedule (/schedule)` | `Run /schedule to lay out a 16-week semester calendar and workload check from my topics and assignments.` |

---

### Part 3: Test with Skills in the Preview Pane & Click Create
1. In the **Preview** chat pane, click the **`+` button** → hover over **`Skills >`** → attach `blooms-learning-objectives-generator`, `course-ai-policy-drafter`, `assignment-rubric-builder`, and `course-schedule-builder`.
2. Open [`example-input.md`](./example-input.md), paste the sample course notes into the chat, and compare the result with [`example-output.md`](./example-output.md).
3. Click **Create** to save your **Syllabus & Rubric Builder** agent!

---

## Files in This Folder

| File | Purpose |
| :--- | :--- |
| [`system-prompt.md`](./system-prompt.md) | Core Backward Design persona, FSU Simple Syllabus structure, and anti-hallucination guardrails |
| [`skills/blooms-learning-objectives.md`](./skills/blooms-learning-objectives.md) | Skill (`/objectives`) for converting vague goals into measurable Bloom's objectives and alignment tables |
| [`skills/ai-policy-drafter.md`](./skills/ai-policy-drafter.md) | Skill (`/ai-policy`) for drafting `ai.fsu.edu` Traffic-Light generative AI syllabus policies |
| [`skills/build-rubric.md`](./skills/build-rubric.md) | Skill (`/rubric`) for building a 4-level analytic grading rubric and student checklist |
| [`skills/build-schedule.md`](./skills/build-schedule.md) | Skill (`/schedule`) for building a 16-week thematic course schedule with workload notes |
| [`example-input.md`](./example-input.md) | Sample course notes and rough goals to test the agent and all four skills |
| [`example-output.md`](./example-output.md) | Sample FSU Simple Syllabus draft, Bloom's matrix, AI policy, rubric, and 16-week schedule |

---

## Modify & Play: Ideas to Try

1. **Adapt from 16-Week Fall/Spring to 6-Week FSU Summer A/B Intensive**:
   - *Try this*: Ask `/schedule` in chat (or edit `skills/build-schedule.md`) to pace modules for a compressed 6-week FSU Summer A or B term with twice-weekly deliverables.
2. **Match Your Department's Custom Syllabus Sections**:
   - *Try this*: Upload your college or department's official syllabus checklist to the agent's **Knowledge / Files** tab so it automatically includes department-specific laboratory safety, studio, or clinical policies.
3. **Compare All Three FSU AI Policy Tiers**:
   - *Try this*: Run `/ai-policy` three times on the same course—once asking for **Option A (Red Light: AI Prohibited)**, once for **Option B (Yellow Light: Conditional & Cited)**, and once for **Option C (Green Light: AI Integrated & Critiqued)**—to see how the assignment expectations shift.
4. **Add a Team Peer Evaluation Skill (`/peer-eval`)**:
   - *Try this*: Create a fifth skill called `/peer-eval` that builds a structured peer evaluation form and accountability policy for team-based projects.
