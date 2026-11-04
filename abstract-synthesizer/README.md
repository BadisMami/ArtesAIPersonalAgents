# Abstract Synthesizer Agent

> **One-Sentence Summary**: Turns collections of paper abstracts, reading notes, or PDF excerpts into structured synthesis narratives, comparison tables, and research gap analyses without inventing citations.

[**⬅ Back to Main Catalog**](../README.md)

---

## Overview

Whether you are preparing a related-work section, onboarding into a new research area, or writing a comprehensive exam review, reading dozens of abstracts is only half the battle—synthesizing how they agree, disagree, and leave open questions is the hardest part.

The **Abstract Synthesizer** takes raw abstracts or reading notes you paste into ArtesAI and organizes them by theme, methodology, and open research questions while strictly relying **only** on the sources you provide.

- **Recommended Model in ArtesAI**: `Anthropic → claude-sonnet-5` (Creativity: `Low`) or `OpenAI → gpt-5.4` / `gpt-6-luna`
- **Estimated Setup Time**: ~5 minutes

---

## How to Build This Agent & Its Skills in ArtesAI

In ArtesAI, **create the companion Skills first** under your account **Settings → My Skills** (Part 1). That way, while you are building the **Personal Agent** (Part 2), you can immediately attach and test the skills inside the right-hand **Preview** chat pane before clicking **Create** (Part 3).

### Part 1: Create the Companion Skills First (`Settings → My Skills`)

1. Click your **Profile / Account box** at the bottom-left of the maroon FSU sidebar and click **Settings**.
2. Click **My Skills** on the left, then click **`+ New Skill`** in the top-right corner.
3. Open each standard skill file below and copy its parts into the **Create Skill** modal (**Name** = `name:` from the top `---` block, **Description** = `description:` from the top `---` block, leave **Always On** unchecked/`Ad Hoc`, and paste the Markdown body below `---` into the dark editor box):
   - **[`methodology-matrix-extractor`](./skills/extract-methodology-matrix.md)** (`/matrix`): Builds a side-by-side Markdown comparison table of study designs, datasets/samples, key metrics, and limitations across all pasted papers.
   - **[`research-gap-identifier`](./skills/identify-research-gaps.md)** (`/gaps`): Identifies contradictions, under-studied populations/conditions, and concrete follow-up study ideas grounded in the provided papers.

---

### Part 2: Create the Personal Agent

#### 0. Launch "Quick Create"
1. In the left maroon FSU sidebar, click **Explore Agents** (or switch to the **Agents** tab).
2. Under **My Agents** (*Agents created by me*), click the **`+ Create`** button next to the **My Agents** heading (or click the dashed **`+ Create`** card).
3. In the **Quick Create** popup box, enter **`Abstract Synthesizer`** as the **Agent Name** and click **`Let's go`**.

#### 1. Instructions (System Prompt)
1. Open [`system-prompt.md`](./system-prompt.md), copy the text, and paste it into the **Specific Instructions** field.
2. **Remove the Platform Instructions**: Delete/clear the default pre-filled **Platform Instructions** to save on context tokens.

#### 2. Name & Identity
In the **Name & Identity** panel, copy and paste the fields below (you'll see them update live in the right-hand **Preview** pane):

- **Name**:
  ```text
  Abstract Synthesizer
  ```
- **Short Description**:
  ```text
  Synthesizes paper abstracts and reading notes into thematic reviews, methodology matrices, and research gaps without inventing citations.
  ```
- **Welcome Message** *(replace the default "Welcome to the Chat!" text in the rich-text editor box)*:
  ```text
  Welcome to the Abstract Synthesizer!

  Paste 2 or more paper abstracts, reading notes, or excerpts below, and I will synthesize how they agree, where they differ, and what open questions remain—strictly citing only the sources you provide.

  How to Attach Companion Skills (Click "+" in the chat bar -> "Skills >"):
  • methodology-matrix-extractor (/matrix) — Build a side-by-side Methodology & Dataset Comparison Table
  • research-gap-identifier (/gaps) — Identify research gaps, contradictions, and follow-up study questions
  ```

#### 3. Knowledge & Tools *(Optional)*
If you are working on a specific thesis chapter or grant proposal, you can upload 3–10 core open-access PDFs here so the agent always has them in its background knowledge. Otherwise, leave this blank and paste abstracts directly into the chat.

#### 4. Capabilities & Model
In the **Capabilities & Model** tab, configure the toggles and model as follows:

| Setting | Recommended Value | Why? |
| :--- | :--- | :--- |
| **Image Creation** | **OFF** | Not needed for academic text synthesis and citation tables. |
| **Add Files & Images** | **ON** | Lets you drag-and-drop paper PDFs or reading notes directly into a chat session. |
| **Web Search** | **OFF** *(Recommended)* | Keeping Web Search **OFF** guarantees the agent strictly synthesizes *only* the verified abstracts/PDFs you provide without pulling in unverified web results. |
| **Generate Artifacts** | **ON** | Renders the `/matrix` comparison table and thematic literature review in a clean side-by-side artifact panel for easy copying. |
| **Model (`Change` button)** | • **Anthropic**: `claude-sonnet-5` or `claude-opus-4-7` *(set **Creativity**: `Low`)*<br>• **OpenAI**: `gpt-5.4` *(Default)* or `gpt-6-luna` *(set **Reasoning Effort**: `Medium`)* | Setting **Creativity** to `Low` (Anthropic) or **Reasoning Effort** to `Medium` (OpenAI) keeps synthesis strictly grounded in your pasted abstracts and prevents citation drift. |

#### 5. Starter Prompts *(Optional)*
In **5. Starter Prompts**, click **Add Starter Prompt** and enter the **Title** and **Prompt** fields below, then click **Create**:

| Title | Prompt |
| :--- | :--- |
| `Synthesize Abstracts + Matrix & Gaps` | `Synthesize the abstracts I paste next and run /matrix and /gaps.` |
| `Compare Study Designs (/matrix)` | `Run /matrix to compare the study designs, sample sizes, and limitations of the papers I paste next.` |
| `Find Research Gaps (/gaps)` | `Run /gaps on the abstracts I paste next to identify contradictions and 3 follow-up research questions.` |

---

### Part 3: Test with Skills in the Preview Pane & Click Create
1. In the **Preview** chat pane on the right side of the Agent Builder (or after clicking **Create**), click the **`+` button** on the left side of the message input bar (`+ Type a message...`) → hover over **`Skills >`** → click `methodology-matrix-extractor` and `research-gap-identifier` to attach them.
2. Open [`example-input.md`](./example-input.md), copy the sample prompt containing 4 paper abstracts on urban heat islands, paste it into the chat, and compare the result with [`example-output.md`](./example-output.md).
3. Click **Create** at the bottom of the screen to save your **Abstract Synthesizer** agent!

---

## Files in This Folder

| File | Purpose |
| :--- | :--- |
| [`system-prompt.md`](./system-prompt.md) | Core persona and strict anti-hallucination citation rules |
| [`skills/extract-methodology-matrix.md`](./skills/extract-methodology-matrix.md) | Skill for building structured methodology comparison tables |
| [`skills/identify-research-gaps.md`](./skills/identify-research-gaps.md) | Skill for spotting contradictions and proposing new research questions |
| [`example-input.md`](./example-input.md) | Sample prompt with 4 paper abstracts to test the agent |
| [`example-output.md`](./example-output.md) | Sample output showing thematic synthesis + both skills in action |

---

## Modify & Play: Ideas to Try

Once you've built and tested the agent, try experimenting with these modifications:

1. **Switch the Citation Format**:
   - *Try this*: In `system-prompt.md`, change the citation rule from `(Author, Year)` APA style to numbered IEEE style `[1], [2]` or MLA style to match your target journal.
2. **Ground in a specific RFP with ArtesAI Knowledge**:
   - *Try this*: If you want this agent to be specific to a grant call, add the RFP website into your ArtesAI Personal Agent's **Files / Knowledge** tab and ask about how these abstracts would relate to the call.
3. **Add a "Grant Background Paragraph" Skill**:
   - *Try this*: Create a third skill called `/background-pitch` that condenses the thematic synthesis and research gap into a single 250-word paragraph suitable for an NSF or NIH introduction for you to edit and build upon.
4. **Test the Guardrails**:
   - *Try this*: Ask the agent to "Add 3 more recent papers from 2026 on this topic." Watch how its anti-hallucination guardrail reminds you that it only cites papers you explicitly provide!

