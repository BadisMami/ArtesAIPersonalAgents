---
name: course-ai-policy-drafter
description: Drafts an FSU-aligned syllabus generative AI policy (following ai.fsu.edu & FDA guidelines) with official FSU template language, a Green/Yellow/Red Traffic-Light table, Academic Honor Policy mapping, and disclosure template. Use when the user types /ai-policy.
---

# Course AI Policy Drafter (`/ai-policy`)

## When to Apply This Skill
Trigger this skill when the user types `/ai-policy` or asks for a syllabus statement governing generative AI usage in their course.

## Official FSU Guidelines (`ai.fsu.edu`, AIEAC, & Office of Faculty Development and Advancement)
Every generated policy must adhere to the requirements and sample syllabus language from the **FSU Artificial Intelligence in Education Advisory Committee (AIEAC)** and **Office of Faculty Development and Advancement (`fda.fsu.edu` / `ai.fsu.edu`)**:

1. **Course-by-Course Syllabus Primacy**: Because AI policies vary across courses and disciplines at FSU, the syllabus is the governing rule for the course. Students must consult the instructor **before** using AI tools if boundaries are unclear.
2. **Verbatim FSU Foundation & Responsibility Language**: Incorporate FSU's standard responsibility clause:
   > *"All work submitted for this course must reflect your own learning and must adhere to the FSU Academic Honor Policy. You are responsible for the information you submit based on an AI query and for assuring that it does not contain misinformation or unethical content and that it does not violate intellectual property laws."*
3. **FSU Academic Honor Policy Misconduct Mapping**: Explicitly map unauthorized or unacknowledged AI use to the three relevant **FSU Academic Honor Policy** categories:
   - **Plagiarism**: Presenting AI-generated text, code, or ideas as one's own original work without required acknowledgement or citation.
   - **Cheating**: Using unauthorized AI tools or applications during an exam, quiz, or restricted assessment.
   - **Falsification**: Using AI to fabricate data, sources, or nonexistent citations (the "citation trap").
4. **University-Approved Tools, Data Privacy (FERPA), & Required Materials Rule**:
   - Direct students to university-approved enterprise tools accessed with FSU credentials (**FSU ArtesAI**, **Microsoft Copilot**, **Google Gemini**) to protect sensitive personal data, proprietary research, and course materials under federal (FERPA) and institutional privacy standards.
   - **Required Materials Rule**: If the instructor requires a specific AI tool (or any paid AI subscription), remind them that FSU requires listing that tool and any associated cost in the **Required Textbooks & Course Materials** section of Simple Syllabus.
5. **No Reliance on Automated AI Detectors**: Per `ai.fsu.edu` / `fda.fsu.edu` guidance, never write syllabus threats relying on commercial automated AI detectors (which are prone to false positives and cannot serve as standalone proof of misconduct at FSU). Instead, emphasize transparent process documentation (draft version history, prompt logs, disclosure statements) and formal FSU Academic Honor Policy resolution procedures.

## Step-by-Step Instructions
1. Identify which of the 3 **FSU Traffic-Light Policy Stances** the instructor wants (if not specified, default to **Yellow Light: Assisted / Conditional Use** and note how to adapt to Green or Red Light), grounding the text in FSU's official sample statements:
   - **🟢 Green Light (AI Encouraged / Allowed)**:
     > *"You are welcome to use generative artificial intelligence (AI) tools (such as university-approved tools like FSU ArtesAI, Microsoft Copilot, or Google Gemini) in this class as doing so aligns with our course learning goals. You are responsible for the information you submit based on an AI query and for assuring that it does not contain misinformation or unethical content and that it does not violate intellectual property laws. Your use of AI tools must be properly documented and cited appropriately for academic integrity."*
   - **🟡 Yellow Light (Assisted / Conditional / Assignment-Specific Use)**:
     > *"You are permitted to use generative artificial intelligence (AI) tools (such as university-approved tools like FSU ArtesAI, Microsoft Copilot, or Google Gemini) to assist you in [gathering information, brainstorming ideas, or specific tasks designated in assignment instructions], but you may not copy and paste information directly from the AI tool and present it as your own without citation. You must critically evaluate and modify any AI-generated content you use. You are responsible for the information you submit based on an AI query and for assuring that it does not contain misinformation or unethical content and that it does not violate intellectual property laws. Your use of AI tools must be properly documented and cited appropriately for academic integrity. You are expected to include a disclosure statement at the end of your assignment describing which AI tool you used and how you used it."*
   - **🔴 Red Light (AI Prohibited)**:
     > *"Generative AI tools are not permitted for use in this course. All submitted work, drafts, and assessments must be entirely your own creation. Unauthorized use of AI-generated text, code, or ideas will be treated as a violation of the FSU Academic Honor Policy (including cheating, plagiarism, and falsification)."*
2. Draft a complete, student-facing **Simple Syllabus AI Policy Statement** (180–250 words) starting from the matching official FSU template above, tailored to the course's specific assignments and learning outcomes, and incorporating the Academic Honor Policy mapping and FSU enterprise tool privacy guidance.
3. Build a **"Green Light / Yellow Light / Red Light" Assignment Matrix** (Markdown table) customized to the course's deliverables:
   - **🟢 Green Light (Allowed & Encouraged — Study & Exploration)**: Specific study, tutoring, or brainstorming uses permitted in this course.
   - **🟡 Yellow Light (Conditional — Permitted ONLY with Citation, Critical Evaluation & Disclosure Statement)**: Specific tasks allowed only when modified, verified, and accompanied by a disclosure statement.
   - **🔴 Red Light (Prohibited — FSU Academic Honor Policy Violation: Plagiarism, Cheating, or Falsification)**: Specific uses prohibited in this course.
4. Provide a copy-pasteable **Student AI Attribution & Disclosure Statement** modeled on FSU's official example (e.g., *"I used [FSU-Approved Tool Name] to [specific task, e.g., brainstorm counterarguments / debug R syntax] with the prompt '[prompt]'. All AI-assisted output was critically evaluated, verified against primary sources, and edited for accuracy and style."*), plus a reminder to check **Required Textbooks & Course Materials** if any AI tool is mandatory.
