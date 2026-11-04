# [Agent Name]

> **One-Sentence Summary**: Describe what this agent does and who at FSU (faculty, researchers, students, staff) benefits from it.

[**⬅ Back to Main Catalog**](../README.md)

---

## Overview

Explain the problem this agent solves in 2–3 sentences. Mention what inputs it expects (e.g., rough notes, article abstracts, data tables) and what outputs it produces.

- **Recommended Model in ArtesAI**: I.e. `OpenAI (gpt-5.4)` (Default) or `Anthropic (claude-sonnet-5)`
- **Estimated Setup Time**: ~5 minutes

---

## How to Build This Agent & Its Skills in ArtesAI

In ArtesAI, **create the companion Skills first** under your account **Settings → My Skills** (Part 1). That way, when you build the **Personal Agent** (Part 2), you can immediately attach and test the skills inside the right-hand **Preview** pane before clicking **Create** (Part 3).

### Part 1: Create the Companion Skills First (`Settings → My Skills`)

1. Click your **Profile / Account name** in the bottom-left corner of the maroon FSU sidebar and click **Settings**.
2. Select **My Skills** on the left, then click **`+ New Skill`** in the top-right corner.
3. Open each standard skill file below and copy its sections into the **Create Skill** modal:
   - **Name**: Copy the `name:` value from the top `---` frontmatter.
   - **Description**: Copy the `description:` value from the top `---` frontmatter (`< 300 chars`).
   - **Always On**: Leave **Unchecked (`Ad Hoc`)**.
   - **Dark Editor Box**: Copy **only the Markdown body below the second `---` line** *(do not paste the `---` YAML frontmatter block into the dark editor, and never include platform/UI instructions inside the skill text—this saves context window tokens!)*.
   - **[`skill-name-slug`](./skills/skill-template.md)**: Briefly explain what this skill does and when to attach it.

---

### Part 2: Create the Personal Agent

#### 0. Launch "Quick Create"
1. In the left maroon FSU sidebar, click **Explore Agents** (or switch to the **Agents** tab).
2. Under **My Agents** (*Agents created by me*), click the **`+ Create`** button next to the **My Agents** heading (or click the dashed **`+ Create`** card).
3. In the **Quick Create** box that appears, type **`[Agent Name]`** into the **Agent Name** field and click **`Let's go`**.

#### 1. Instructions (System Prompt)
1. Open [`system-prompt.md`](./system-prompt.md), copy the text, and paste it into the **Specific Instructions** box.
2. **Remove the Platform Instructions**: Delete/clear the default pre-filled **Platform Instructions** in ArtesAI to save on context tokens and prevent generic instructions from diluting your agent's behavior.

#### 2. Name & Identity
In the **Name & Identity** panel, fill in the three fields below (you can see your changes live in the right-hand **Preview** pane):

- **Name**:
  ```text
  [Agent Name]
  ```
- **Short Description**:
  ```text
  [1-sentence summary of what the agent does and who it helps.]
  ```
- **Welcome Message** *(replace the default "Welcome to the Chat!" text in the rich-text editor box)*:
  ```markdown
  Welcome to the **[Agent Name]**!

  **How to use this agent:**
  Paste [describe what the user should paste or upload] into the chat below.

  **How to Attach Companion Skills (Click `+` → `Skills >` in the chat bar):**
  - `[skill-1-name]` (`/[skill-1]`) — [Short description of Skill 1]
  - `[skill-2-name]` (`/[skill-2]`) — [Short description of Skill 2]
  ```

#### 3. Knowledge & Tools *(Optional)*
Describe any optional reference PDFs, templates, or style guides the user can upload here.

#### 4. Capabilities & Model
In the **Capabilities & Model** tab, configure the toggles and model as follows:

| Setting | Recommended Value | Why? |
| :--- | :--- | :--- |
| **Image Creation** | `Off` (or `On`) | Explain whether image generation is needed. |
| **Add Files & Images** | `On` | Allows users to upload documents/data directly in chat. |
| **Web Search** | `Off` (or `On`) | Keep `Off` for strict grounding in user text, or `On` for live web lookups. |
| **Generate Artifacts** | `On` | Renders tables, code, and structured drafts in a side-by-side window. |
| **Model (`Change` button)** | • **OpenAI**: `gpt-5.4` *(Default)* or `gpt-6-luna`<br>• **Anthropic**: `claude-sonnet-5` or `claude-opus-4-7` | In **Model Options**, set **Creativity** (`Low`/`Medium`) for Anthropic or **Verbosity & Reasoning Effort** (`Auto`/`Medium`/`High`) for OpenAI, then click **Save**. |

#### 5. Starter Prompts
*(Optional)* In **5. Starter Prompts**, click **Add Starter Prompt** and add 1–2 quick-start prompts using the **Title** and **Prompt** fields, then click **Create**:

| Title | Prompt |
| :--- | :--- |
| `[Short Button Title 1]` | `[Full starter prompt text 1]` |
| `[Short Button Title 2]` | `[Full starter prompt text 2]` |

---

### Part 3: Test with Skills in the Preview Pane & Click Create
1. In the **Preview** chat pane on the right side of the Agent Builder (or after clicking **Create**), click the **`+` button** inside the message bar (`+ Type a message...`) → hover over **`Skills >`** → click the skill(s) you created in Part 1 to attach them.
2. Open [`example-input.md`](./example-input.md), paste the sample prompt into the chat, and compare the result with [`example-output.md`](./example-output.md).
3. Click **Create** at the bottom of the screen to save your Personal Agent!

---

## Files in This Folder

| File | Purpose |
| :--- | :--- |
| [`system-prompt.md`](./system-prompt.md) | Core persona, tone, and formatting rules for the agent |
| [`skills/skill-template.md`](./skills/skill-template.md) | Copy-pasteable skill definition |
| [`example-input.md`](./example-input.md) | Sample user input to test the agent |
| [`example-output.md`](./example-output.md) | Sample response showing what a good run looks like |

---

## Context-Saving Checklist (For Agent Creators)

When building a new agent from this template, keep your prompts and skills lean so you don't waste the model's context window (especially on models with `4,096` or `8,192` token limits):

1. **Strip All Platform & UI Instructions from `system-prompt.md` and `skills/*.md`**:
   - Never put human setup directions (e.g., *"Copy and paste this into ArtesAI"*, *"Click the `+` button in the chat bar to attach a skill"*) inside `system-prompt.md` or `skills/*.md`.
   - Put human UI navigation instructions in `README.md` or in the **Step 2: Name & Identity → Welcome Message** box (which displays to the user on the chat start screen without cluttering your prompt files).
2. **Omit the `---` YAML Frontmatter When Pasting into ArtesAI**:
   - The `---` block (`name:` and `description:`) at the top of `skills/*.md` allows the file to work as-is in file-based agent systems. When pasting into ArtesAI's dark **Skill Editor**, only copy the lines *below* the second `---` so you don't duplicate the name and description inside the model's context.
3. **Keep `system-prompt.md` Under ~250 Words**:
   - Only include rules that must apply to **100% of turns** (role, tone, core guardrails). Move specific output templates, long rubrics, or language-specific code rules into `skills/*.md` so they are only loaded into context when needed.

---

## Modify & Play: Ideas to Try

Once you have the baseline agent working, try customizing it:

1. **Change the Audience or Tone**:
   - *Try this*: Edit the `Tone & Style` section of `system-prompt.md` to target undergraduate students instead of faculty reviewers.
2. **Add Department-Specific Context**:
   - *Try this*: Upload a sample PDF or rubric into your ArtesAI agent's **Knowledge / Files** section so the agent grounds its feedback in your department's standards.
3. **Create a New Skill**:
   - *Try this*: Duplicate [`skills/skill-template.md`](./skills/skill-template.md) and create a command like `/checklist` that outputs a final verification table.

