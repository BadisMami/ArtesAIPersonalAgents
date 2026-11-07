# Research Paper Matchmaker Agent

> **One-Sentence Summary**: Connects research papers to your specific project in plain language, explaining what each paper offers, what does not apply, and how they rank, for faculty and students starting new research or reading outside their field.

[**⬅ Back to Main Catalog**](../README.md)

---

## Overview

When you start a new project or read outside your field, it is hard to tell which papers actually matter for *your* work. The **Research Paper Matchmaker** reads your project description and either:

- **Project + Papers**: explains the papers you upload, shows how each one helps your project, flags what does not apply, and ranks them by relevance, or
- **Project Only**: finds real, relevant papers and returns a link, a one-line summary, and why each one fits.

It never invents papers or links, and it bases its explanations only on your papers and project description. No technical background needed.

- **Recommended Model in ArtesAI**: `Anthropic → claude-sonnet-5` or `OpenAI → gpt-5.4` (Default)
- **Estimated Setup Time**: ~5 minutes

---

## How to Build This Agent & Its Skills in ArtesAI

In ArtesAI, **create the companion Skills first** under your account **Settings → My Skills** (Part 1). That way, when you build the **Personal Agent** (Part 2), you can immediately attach and test the skills inside the right-hand **Preview** pane before clicking **Create** (Part 3).

### Part 1: Create the Companion Skills First (`Settings → My Skills`)

1. Click your **Profile / Account box** at the bottom-left of the maroon FSU sidebar and click **Settings**.
2. Click **My Skills** on the left, then click **`+ New Skill`** in the top-right corner.
3. Open each skill file below and copy its parts into the **Create Skill** modal (**Name** = `name:` from the top `---` block, **Description** = `description:` from the top `---` block, leave **Always On** unchecked/`Ad Hoc`, and paste only the Markdown body below the second `---` into the dark editor box):
   - **[`project-paper-matcher`](./skills/match-papers-to-project.md)** (`/match`): Explains each uploaded paper, connects it to your project, flags what does not apply, and builds a ranking table.
   - **[`project-paper-finder`](./skills/find-papers-for-project.md)** (`/find`): Searches for real papers that fit your project. If web search is off, it suggests search terms and databases instead.

---

### Part 2: Create the Personal Agent

#### 0. Launch "Quick Create"
1. In the left maroon FSU sidebar, click **Explore Agents** (or switch to the **Agents** tab).
2. Under **My Agents** (*Agents created by me*), click the **`+ Create`** button next to the **My Agents** heading (or click the dashed **`+ Create`** card).
3. In the **Quick Create** popup box, enter **`Research Paper Matchmaker`** as the **Agent Name** and click **`Let's go`**.

#### 1. Instructions (System Prompt)
1. Open [`system-prompt.md`](./system-prompt.md), copy the text, and paste it into the **Specific Instructions** field.
2. **Remove the Platform Instructions**: Delete/clear the default pre-filled **Platform Instructions** to save on context tokens.

#### 2. Name & Identity
- **Name**:
  ```text
  Research Paper Matchmaker
  ```
- **Short Description**:
  ```text
  Connects research papers to your project in plain language: what each paper offers, what does not apply, and how they rank.
  ```
- **Welcome Message** *(replace the default "Welcome to the Chat!" text)*:
  ```text
  Welcome to the Research Paper Matchmaker!

  Describe your research project in a few sentences. Then either:
  • Upload or paste papers, and I will explain how each one fits your project and rank them, or
  • Send just your project, and I will find relevant papers with links.

  How to Attach Companion Skills (Click "+" in the chat bar -> "Skills >"):
  • project-paper-matcher (/match): Explain and rank the papers you upload
  • project-paper-finder (/find): Find real papers that fit your project
  ```

#### 3. Knowledge & Tools *(Optional)*
If you always work on the same project, upload a one-page project summary here so you do not have to describe it every time. Otherwise, leave this blank.

#### 4. Capabilities & Model

| Setting | Recommended Value | Why? |
| :--- | :--- | :--- |
| **Image Creation** | **OFF** | Not needed for reading and ranking papers. |
| **Add Files & Images** | **ON** | Lets you upload paper PDFs directly into the chat. |
| **Web Search** | **ON** | Required for `/find` (Project Only mode). If you turn it **OFF**, `/find` suggests search terms instead of papers, and `/match` still works fully. |
| **Generate Artifacts** | **ON** | Shows the ranking table and paper cards in a clean side panel. |
| **Model (`Change` button)** | • **Anthropic**: `claude-sonnet-5` *(set **Creativity**: `Low`)*<br>• **OpenAI**: `gpt-5.4` *(set **Reasoning Effort**: `Medium`)* | Low creativity keeps explanations grounded in the papers and reduces made-up details. |

#### 5. Starter Prompts *(Optional)*

| Title | Prompt |
| :--- | :--- |
| `Match My Papers (/match)` | `/match Here is my project description. I am attaching the papers I want you to explain and rank.` |
| `Find Papers for My Project (/find)` | `/find Here is my project description. Find relevant papers with links and explain why each one fits.` |

---

### Part 3: Test with Skills in the Preview Pane & Click Create
1. In the **Preview** chat pane, click the **`+` button** in the message bar → hover over **`Skills >`** → click `project-paper-matcher` and `project-paper-finder` to attach them.
2. Open [`example-input.md`](./example-input.md), attach the CRESt paper, paste the sample prompt, and compare the result with [`example-output.md`](./example-output.md).
3. Click **Create** at the bottom of the screen to save your **Research Paper Matchmaker** agent!

---

## Files in This Folder

| File | Purpose |
| :--- | :--- |
| [`system-prompt.md`](./system-prompt.md) | Core role, the two modes, and the no-fake-papers guardrails |
| [`skills/match-papers-to-project.md`](./skills/match-papers-to-project.md) | Skill for explaining and ranking uploaded papers (`/match`) |
| [`skills/find-papers-for-project.md`](./skills/find-papers-for-project.md) | Skill for finding real papers with links (`/find`) |
| [`example-input.md`](./example-input.md) | Sample project (robotic lab fault detection) plus the CRESt paper |
| [`example-output.md`](./example-output.md) | Sample paper card and ranking table |

---

## Modify & Play: Ideas to Try

1. **Change the Reading Level**:
   - *Try this*: In `system-prompt.md`, change "plain language" to "technical language for an expert in the field" for a faster, denser review.
2. **Add a Reading Plan Skill**:
   - *Try this*: Create a `/plan` skill that turns the ranking table into a one-week reading schedule with specific sections to read each day.
3. **Test the Guardrails**:
   - *Try this*: Turn **Web Search** off and type `/find`. The agent should give you search terms instead of making up papers.
