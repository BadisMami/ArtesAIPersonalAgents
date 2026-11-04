# FSU ArtesAI Personal Agent Examples

Welcome to the **FSU ArtesAI Personal Agent Examples** repository! This collection provides ready-to-use blueprints for building Personal Agents in Florida State University's **ArtesAI** platform.

Each folder in this repository contains everything you need to build a specialized AI assistant in minutes:
- **Step-by-step setup instructions** (`README.md`)
- **A copy-pasteable System Prompt** (`system-prompt.md`)
- **Modular Skills** (`skills/`) to copy into your ArtesAI account
- **Sample Input & Output** (`example-input.md` and `example-output.md`) so you can test your agent right away
- **"Modify & Play" ideas** to customize the agent for your own department, lab, or workflow

> **New to System Prompts & Skills?** Read our quick guide: [**System Prompts vs. Skills: What's the Difference? (`docs/system-prompts-vs-skills.md`)**](./docs/system-prompts-vs-skills.md) to learn how they work together and when to put instructions in a System Prompt vs. a reusable Skill.

---

## Example Agents Catalog

| Agent | Focus Area | Included Skills | Difficulty |
| :--- | :--- | :--- | :--- |
| [**Abstract Synthesizer**](./abstract-synthesizer/README.md) | Academic & Research | • `methodology-matrix-extractor`<br>• `research-gap-identifier` | Beginner |
| [**Scientific Figure Recreator**](./scientific-figure-recreator/README.md) | Data Visualization & Plotting | • `figure-recreator-python`<br>• `figure-recreator-r`<br>• `figure-recreator-stata`<br>• `figure-recreator-matlab` | Beginner / Intermediate |

---

## Quick Start: How to Build an Agent & Its Skills in ArtesAI

In FSU's ArtesAI, **Skills** and **Personal Agents** are created in two separate places. **Create the Skills first** (`Settings → My Skills`) so that when you open the Personal Agent builder, you can immediately attach and test your skills right inside the right-hand **Preview** chat pane as you build the agent!

### Part 1: Create the Skills First (`Settings → My Skills`)
Every file in an agent's `skills/` folder is a **standard, platform-agnostic skill file** (YAML frontmatter `---` at the top with `name:` and `description:`, followed by the Markdown instructions below `---`).
1. Click your **Profile / Account box** at the bottom-left of the maroon FSU sidebar and select **Settings**.
2. In the Account sidebar, click **My Skills** and then click the **`+ New Skill`** button in the top right.
3. Open each skill `.md` file in the agent's `skills/` folder and copy its sections into the **Create Skill** modal:
   - **Name**: Copy the `name:` value from the top frontmatter (e.g., `methodology-matrix-extractor`).
   - **Description (`0/300` characters)**: Copy the `description:` value from the top frontmatter (pre-sized `< 300 chars` to tell the model what the skill is for and when to apply it).
   - **Always On**: Leave **Unchecked (`Ad Hoc`)** *(ArtesAI allows a maximum of 5 `Always On` skills across your entire account, so keeping agent-specific skills `Ad Hoc` saves your global slots)*.
   - **Skill Instructions (`0/30,000` dark editor)**: Copy the Markdown body below the second `---` line into the dark editor and click **Create**.

### Part 2: Create the Personal Agent (Quick Create + 5-Step Builder)
1. **Open the Agent Builder (`Quick Create`)**:
   - In the left maroon FSU sidebar, click **Explore Agents** (or select the **Agents** tab).
   - Scroll to the **My Agents** (*Agents created by me*) section and click the **`+ Create`** button next to **My Agents** (or the dashed **`+ Create`** card).
   - In the **Quick Create** popup box, enter the **Agent Name** from the agent's `README.md` and click **`Let's go`**.
2. **Step 1 — Instructions (`system-prompt.md`)**:
   - Open the agent's `system-prompt.md` file, copy the text, and paste it into the **Specific Instructions** field.
   - **Remove the Platform Instructions**: Delete/clear the default pre-filled **Platform Instructions** in ArtesAI to save on context window tokens and keep the model focused strictly on your agent's instructions and skills.
3. **Step 2 — Name & Identity**:
   - **Name**: Pre-filled from Quick Create (verify it matches the agent title).
   - **Short Description**: Copy the 1-sentence summary into the **Short Description** box.
   - **Welcome Message (Rich Text Box)**: Replace the default *"Welcome to the Chat!"* boilerplate text with the custom **Welcome Message** provided in each agent's `README.md`. This text appears on the start screen of your agent chat, reminding you what to paste and which skills to attach!
4. **Step 3 — Knowledge & Tools**:
   - *(Optional)* Upload any static reference files you want the agent to always know (e.g., your lab style guide, department syllabus template, or agency solicitation PDF).
5. **Step 4 — Capabilities & Model**:
   - Set the four capability toggles (**Image Creation**, **Add Files & Images**, **Web Search**, and **Generate Artifacts**) and click **Change** next to **Model** to select your preferred **Model Type** (`OpenAI`, `Anthropic`, `xAI`, `Mistral`, or `Meta`) and **Model** (such as `gpt-5.4`, `gpt-6-luna`, `claude-sonnet-5`, or `claude-opus-4-7`) using the recommended table in each agent's `README.md`.
6. **Step 5 — Starter Prompts**:
   - *(Optional)* Click **Add Starter Prompt** and enter the **Title** and **Prompt** pairs listed in each agent's `README.md`, then click **Create**.

### Part 3: Test with Skills in the Preview Pane & Click Create
1. While still in the Agent Builder (or after clicking **Create**), look at the **Preview** chat pane on the right.
2. Click the **`+` button** on the left side of the message input bar (`+ Type a message...`).
3. Hover over **`Skills >`** in the popup menu and click the skill(s) you created in Part 1 to attach them.
4. Copy the sample prompt from `example-input.md` into the chat, verify the response against `example-output.md`, and click **Create** at the bottom to save your agent!

---

## Understanding "Capabilities & Model" (Step 4)

In step **4. Capabilities & Model**, ArtesAI lets you toggle four features and pick a base model. Here is a quick guide to when to turn each toggle **On** or **Off**:

| Capability / Setting | What It Does in ArtesAI | When to Turn It **ON** vs. **OFF** |
| :--- | :--- | :--- |
| **Image Creation** | Allows the agent to generate images from text prompts. | Keep **OFF** for academic writing, coding, and data agents (prevents accidental image generation). Turn **ON** only if brainstorming visual/graphical concepts. |
| **Add Files & Images** | Lets users attach PDFs, CSVs, scripts, or screenshots directly inside a chat session. | Turn **ON** for almost all research, teaching, and coding agents so you can drop papers, syllabi, or `.py`/`.csv` files into the chat. |
| **Web Search** | Lets the agent search the live internet during a conversation. | Keep **OFF** when you want strict grounding in *only* the text/data you provide (e.g., `Abstract Synthesizer`). Turn **ON** when checking live funder websites or current policy dates. |
| **Generate Artifacts** | Opens long tables, polished drafts, and code scripts in a dedicated side-by-side preview/copy window. | Turn **ON** for all agents in this repo—it makes Markdown matrices, syllabi, and Python/R scripts much easier to read and copy. |
| **Model (`Change` button)** | Opens the **Model Options** dialog to choose a **Model Type**, specific **Model**, **Max Response Tokens**, and tuning controls (**Creativity** or **Verbosity / Reasoning Effort**). | Defaults to `OpenAI (gpt-5.4)`. See the table below for every available model in ArtesAI and when to use each. |

### Available Models in ArtesAI (`Model Options` Dialog)

Clicking **Change** next to **Model** opens the **Model Options** window where you can choose from 5 **Model Types**:

| Model Type | Available Models in Dropdown | Default Max Response Tokens | Tuning Controls | Best Used For |
| :--- | :--- | :--- | :--- | :--- |
| **OpenAI** | • `gpt-5.4` *(Default)*<br>• `gpt-5.4-mini`<br>• `gpt-5.6-luna`<br>• `gpt-5.6-terra`<br>• `gpt-6-luna` | `128,000` | • **Verbosity**: `Auto` \| `Low` \| `Medium` \| `High`<br>• **Reasoning Effort**: `Auto` \| `Low` \| `Medium` \| `High` | All-around academic work, vision/figure analysis, complex multi-step reasoning (`gpt-6-luna` with `High` Reasoning Effort), or fast everyday tasks (`gpt-5.4-mini`). |
| **Anthropic** | • `claude-haiku-4-5`<br>• `claude-opus-4-7`<br>• `claude-sonnet-4-6`<br>• `claude-sonnet-5` | `64,000` | • **Creativity**: `None` \| `Low` \| `Medium` \| `High` *(+ Precise Value)* | Nuanced academic writing, grant editing, literature synthesis, and clean scientific code (`claude-sonnet-5` and `claude-opus-4-7` are top choices; use `Low` Creativity for code/citations). |
| **xAI** | • `grok-4.3` | `8,192` | • **Creativity**: `None` \| `Low` \| `Medium` \| `High` *(+ Precise Value)* | Fast brainstorming, course ideation, and direct analytical Q&A. |
| **Mistral** | • `Mistral-Large-3` | `4,096` | • **Creativity**: `None` \| `Low` \| `Medium` \| `High` *(+ Precise Value)* | Concise European/multilingual text tasks and lightweight structured summaries (note the `4,096` output token cap). |
| **Meta** | • `Llama-3.3-70B-Instruct` | `4,096` | • **Creativity**: `None` \| `Low` \| `Medium` \| `High` *(+ Precise Value)* | Open-weights baseline comparisons and short instructional tasks (note the `4,096` output token cap). |

---

## Tips for Getting the Most Out of ArtesAI Agents

- **Start Simple, Then Layer Skills**: Test the agent with just its `system-prompt.md` first, then add skills one at a time so you can see how each skill shapes the output.
- **Attach Reference Files**: ArtesAI allows you to upload reference documents (such as your lab style guide, agency solicitation PDFs, or department syllabus templates) directly to your Personal Agent's knowledge base.
- **Experiment with "Modify & Play"**: At the bottom of every agent's `README.md`, you'll find concrete ideas for tweaking tone, output formats, and domain rules.

---

## Adding Your Own Agent Example

Want to share an agent you built for your FSU course, lab, or office?
1. Duplicate the [`_agent-template`](./_agent-template/README.md) folder and rename it (e.g., `your-agent-name`).
2. Fill in `system-prompt.md`, add your `skills/`, and include a realistic `example-input.md` and `example-output.md`.
3. Add a link to your new folder in the **Example Agents Catalog** table above.

