# Syllabus & Rubric Builder

> **One-Sentence Summary**: Turns rough course notes into a student-facing syllabus draft, assignment rubrics, and a week-by-week schedule, flagging anything the instructor still needs to fill in.

[**⬅ Back to Main Catalog**](../README.md)

---

## Overview

Writing a syllabus from scratch, then building a rubric for every assignment, then laying out a week-by-week calendar, is a lot of repetitive formatting work for something every course needs. The **Syllabus & Rubric Builder** takes the notes you already have in your head (topics, readings, assignments, grading weights, meeting days) and turns them into clean drafts, while clearly marking anything it cannot know, like your institution's required policy statements or your office hours, instead of guessing.

- **Recommended Model in ArtesAI**: `Anthropic (claude-sonnet-5)` or `OpenAI (gpt-5.4)`
- **Estimated Setup Time**: ~5 minutes

---

## How to Build This Agent & Its Skills in ArtesAI

In ArtesAI, **create the companion Skills first** under your account **Settings → My Skills** (Part 1). That way, while you build the **Personal Agent** (Part 2), you can immediately attach and test the skills inside the right-hand **Preview** chat pane before clicking **Create** (Part 3).

### Part 1: Create the Companion Skills First (`Settings → My Skills`)

1. Click your **Profile / Account box** at the bottom-left of the maroon FSU sidebar and click **Settings**.
2. Click **My Skills** on the left, then click **`+ New Skill`** in the top-right corner.
3. Open each standard skill file below and copy its parts into the **Create Skill** modal (**Name** = `name:` from the top `---` block, **Description** = `description:` from the top `---` block, leave **Always On** unchecked/`Ad Hoc`, and paste the Markdown body below `---` into the dark editor box):
   - **[`assignment-rubric-builder`](./skills/build-rubric.md)** (`/rubric`): Builds an analytic grading rubric for one assignment, aligned to the course learning objectives.
   - **[`course-schedule-builder`](./skills/build-schedule.md)** (`/schedule`): Lays out a week-by-week course schedule, spacing major assignments and flagging workload clusters.

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
  Turns course notes into a syllabus draft, assignment rubrics, and a week-by-week schedule, flagging what you still need to fill in.
  ```
- **Welcome Message** *(replace the default "Welcome to the Chat!" text in the rich-text editor box)*:
  ```text
  Welcome to the Syllabus & Rubric Builder!

  Paste your rough course notes below (topics, readings, assignments, grading weights, meeting days), and I will draft a syllabus, flagging anything I cannot know for you to fill in.

  How to Attach Companion Skills (Click "+" in the chat bar -> "Skills >"):
  • assignment-rubric-builder (/rubric) — Build a grading rubric for one assignment
  • course-schedule-builder (/schedule) — Build a week-by-week course schedule
  ```

#### 3. Knowledge & Tools *(Optional)*
If your department has a standard syllabus template or an official policy-statement document, upload it here so the agent can match your institution's required wording instead of leaving a placeholder.

#### 4. Capabilities & Model
In the **Capabilities & Model** tab, configure the toggles and model as follows:

| Setting | Recommended Value | Why? |
| :--- | :--- | :--- |
| **Image Creation** | **OFF** | Not needed for text-based course documents. |
| **Add Files & Images** | **ON** | Lets you upload a department syllabus template or past course notes. |
| **Web Search** | **OFF** | Keeps the draft grounded in your notes instead of pulling in unrelated web content. |
| **Generate Artifacts** | **ON** | Renders the syllabus, rubric tables, and schedule in a clean side-by-side panel for easy copying. |
| **Model (`Change` button)** | • **Anthropic**: `claude-sonnet-5` *(set **Creativity**: `Low`)*<br>• **OpenAI**: `gpt-5.4` *(Default, set **Reasoning Effort**: `Medium`)* | A lower creativity/effort setting keeps the draft grounded in your notes and reduces invented policy text or dates. |

#### 5. Starter Prompts *(Optional)*
In **5. Starter Prompts**, click **Add Starter Prompt** and enter the fields below:

| Title | Prompt |
| :--- | :--- |
| `Build My Syllabus` | `Build a syllabus draft from the course notes I paste next.` |
| `Build a Rubric (/rubric)` | `Run /rubric on the assignment I describe next.` |

---

### Part 3: Test with Skills in the Preview Pane & Click Create
1. In the **Preview** chat pane, click the **`+` button** → hover over **`Skills >`** → click `assignment-rubric-builder` and `course-schedule-builder` to attach them.
2. Open [`example-input.md`](./example-input.md), paste the sample course notes into the chat, and compare the result with [`example-output.md`](./example-output.md).
3. Click **Create** to save your **Syllabus & Rubric Builder** agent!

---

## Files in This Folder

| File | Purpose |
| :--- | :--- |
| [`system-prompt.md`](./system-prompt.md) | Core persona and guardrails against inventing policy text or course facts |
| [`skills/build-rubric.md`](./skills/build-rubric.md) | Skill for building an analytic grading rubric |
| [`skills/build-schedule.md`](./skills/build-schedule.md) | Skill for building a week-by-week course schedule |
| [`example-input.md`](./example-input.md) | Sample course notes to test the agent |
| [`example-output.md`](./example-output.md) | Sample syllabus, rubric, and schedule output |

---

## Modify & Play: Ideas to Try

1. **Match Your Department's Template**:
   - *Try this*: Upload your department's official syllabus template to the agent's **Knowledge / Files** tab and ask it to follow that section order instead of the default one.
2. **Add a Peer Evaluation Skill**:
   - *Try this*: Create a third skill called `/peer-eval` that builds a short peer evaluation form for team-based assignments.
3. **Change the Audience**:
   - *Try this*: Edit the `Tone & Style` guidance in `system-prompt.md` to target a graduate seminar instead of an undergraduate course.
