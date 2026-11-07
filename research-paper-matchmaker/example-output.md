# Example Output: Research Paper Matchmaker

Below is an example of what your ArtesAI agent will generate when given the prompt in [`example-input.md`](./example-input.md):

---

> **Your project, in short:** You are adding camera-based safety checks to a robotic electrochemistry station so the robot stops and alerts a person whenever a step goes wrong, using simple vision methods first.
>
> ### Paper 1: CRESt (Zhang, Ren, Hsu, Chen, et al., *Nature*, 2025)
>
> **What it is about:** MIT researchers built CRESt, a robotic lab system guided by AI that chooses which materials to try, makes them, and tests them with electrochemistry. Over three months it explored more than 900 chemistries and ran 3,500 electrochemical tests, finding an eight-element fuel cell catalyst with 9.3 times the power density per dollar of pure palladium. It uses cameras and vision-language models (AI that can describe what it sees in an image) to watch experiments and flag problems.
>
> **How it helps your project:**
> - **Proof that your idea matters:** The authors found poor reproducibility (results that change between repeat runs) was a major early obstacle. That is a strong motivation to cite for a fault-detection layer.
> - **Same kinds of faults:** CRESt's cameras caught issues like small shape deviations in samples and a pipette moving something out of place. These match your checks for sample position and grip.
> - **Similar setup:** It is also a robot running electrochemical tests, so its lessons transfer closely to your station.
> - **Human in the loop:** CRESt suggests fixes, but humans still did most of the debugging. That supports your design choice to stop the robot and email a person on FAIL.
>
> **What does not apply:**
> - **The AI material-picking part** (active learning that decides what to test next) is outside your project's scope.
> - **The vision approach is heavier than yours:** CRESt relies on vision-language models, while you plan to start with simple markers and image comparison. Treat CRESt as a possible later upgrade, not a blueprint.
> - **The catalyst chemistry results** do not affect how you build your checks.
>
> **Relevance score: High.** It is one of the closest published examples of camera-based monitoring in a robotic electrochemistry lab.
>
> ### Ranking Table
>
> | Rank | Paper | Score | Best Use for Your Project |
> | :--- | :--- | :--- | :--- |
> | 1 | CRESt (*Nature*, 2025) | High | Motivation (reproducibility) and examples of real faults that cameras caught |
>
> **Where to start:** Read the sections on reproducibility and camera monitoring first, then skim the rest.
>
> **Suggested next step:** Type `/find` and I will look for papers on simple computer-vision checks for lab robots, so you have something to compare against CRESt's heavier approach.
