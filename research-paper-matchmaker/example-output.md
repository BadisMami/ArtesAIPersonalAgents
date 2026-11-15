# Example Output: Research Paper Matchmaker

Below is an example of what your ArtesAI **Research Paper Matchmaker** agent will generate when given the prompt in [`example-input.md`](./example-input.md):

Generated with ArtesAI using gpt-5.6-luna on 2026/11/15.
---

## Project restatement

You are building a **vision-based fault-detection layer** for an FSU autonomous materials workflow using an xArm6, an electrochemical cell, and a potentiostat. The system will check sample identity/location, successful gripping, dipping depth, and sample stability during testing. It should use **markers and image comparison first**, with machine learning only when simpler methods are insufficient.

## Paper 1: Zhang, Ren, Hsu, Chen, et al. (2025)

**“A multimodal robotic platform for multi-element electrocatalyst discovery.”** *Nature*.

[Paper link](https://www.nature.com/articles/s41586-025-09640-5)

### What it is about

The paper describes CRESt, an autonomous platform that combines robotic experiment execution, catalyst synthesis, electrochemical testing, active learning, and automated characterization. According to the provided excerpt, the platform uses onboard cameras and vision-language models (VLMs—models that interpret images together with language) to detect experimental irregularities such as liquid-handling problems, sample-geometry deviations, and pipette misalignment.

The paper appears to address not only robot control, but also the broader problem of making long-running automated experiments reliable and scientifically useful.

### How it helps your project

- **Strong system-level precedent:** It supports the idea that camera-based monitoring should be integrated directly into an autonomous materials workflow rather than treated as a separate inspection step.

- **Useful fault categories:** The reported examples—liquid-handling errors, geometry deviations, and pipette misalignment—are conceptually close to your checks for:
  - whether the correct sample is present,
  - whether the gripper successfully picked it up,
  - whether the sample is positioned correctly in the cell, and
  - whether the experimental setup has shifted.

- **Human-in-the-loop response:** The excerpt says the system flags anomalies and suggests corrective actions for human operators. This is relevant to your design in which a `FAIL` stops the robot and emails a person. You can use the paper as support for treating fault detection as part of the control and recovery process, not merely as a post-run quality report.

- **Motivation for uncertainty handling:** The paper’s anomaly-monitoring role is compatible with your three-way output:
  - `PASS`: visual evidence agrees with the expected state,
  - `FAIL`: a known fault is detected,
  - `UNCERTAIN`: the camera evidence is ambiguous or confidence is too low.

- **Potential comparison point for future expansion:** If markers and image comparison eventually become inadequate, the paper may provide a useful example of a more advanced VLM-based monitoring layer.

### What does not directly apply

- **The paper’s main scientific objective differs from yours.** CRESt is focused on discovering electrocatalysts through automated experimentation. Your immediate objective is operational safety and reliability of an existing robotic workflow.

- **VLMs may be more complex than necessary.** Your initial checks—marker detection, template matching, background subtraction, image registration, and geometric measurement—may be easier to validate and more deterministic than a VLM. The excerpt does not establish that VLMs are necessary for the particular faults in your xArm6 setup.

- **The excerpt does not provide implementation details for your exact checks.** It does not state how the cameras were positioned, what image-processing algorithms were used, how dipping depth was measured, or how thresholds were selected. Those details are therefore **Not stated in the provided text**.

- **Hardware and workflow transfer is uncertain.** The platform’s cameras, robot configuration, cell geometry, sample holders, and control software may differ substantially from your FSU setup. Any direct hardware or software design transfer requires verification from the full paper.

## Relevance score: **Medium–High**

This is highly relevant as a **system-design and motivation paper** for monitoring autonomous electrochemical experiments, anomaly detection, and human escalation. It is less directly useful as an implementation guide for your first version because the provided excerpt emphasizes VLM-based monitoring and does not describe simple marker-based or image-comparison methods in enough detail.

## Ranking table

| Rank | Paper (Authors, Year) | Relevance Score | Best Use for Your Project |
|---|---|---|---|
| 1 | Zhang, Ren, Hsu, Chen, et al. (2025) | Medium–High | Use as a system-level reference for integrating camera checks, anomaly detection, uncertainty, and human intervention into an autonomous materials workflow. |

## What to focus on first

If you read the full paper, prioritize:

1. **The sections describing onboard vision and experimental monitoring**  
   Look for the monitored failure modes, camera placement, visual inputs, and how anomalies are communicated to operators.

2. **The robot-execution or system-architecture description**  
   Focus on how visual checks are connected to the experiment sequence and whether a failed check prevents subsequent actions.

3. **Any discussion of corrective actions, operator review, or reliability**  
   This is most relevant to your `FAIL → stop robot → email human` design.

4. **Supplementary methods, if available**  
   The main paper may describe the vision system at a high level, while implementation details—training data, thresholds, latency, and failure cases—may appear in the supplement. If those details are absent, record them as **Not stated in the provided text** rather than assuming the system will transfer directly.

## Bottom line

Use this paper to justify and structure your **fault-detection architecture**, especially the ideas of continuous visual monitoring, anomaly reporting, uncertainty, and human intervention. Do **not** treat it as evidence that you need a VLM immediately. For your first implementation, a more appropriate progression is:

1. **Markers and fixed-camera geometry** for sample identity, location, and dipping depth.
2. **Image comparison or template matching** for gripper and sample-presence checks.
3. **Explicit uncertainty thresholds** when visual evidence is poor.
4. **Machine learning or VLMs only for failure modes that remain difficult after calibration.**

Two concrete next steps:

- Create a fault matrix listing each check, camera view, measurable visual feature, PASS/FAIL threshold, and UNCERTAIN condition.
- Read the paper’s vision-monitoring and supplementary-methods sections specifically for camera configuration, anomaly categories, and operator escalation. If it does not give enough implementation detail, use `/find` to locate papers on **robotic manipulation visual verification**, **electrochemical cell automation**, and **marker-based robot fault detection**.

---

# Literature Search Strategy

## Search themes

Your project centers on five themes:

1. **Vision-based robotic fault detection**
2. **Fiducial markers** (printed visual markers used to estimate position and orientation)
3. **Grasp-success and object-presence verification**
4. **Camera-based placement and depth verification**
5. **Anomaly detection and human-in-the-loop recovery in autonomous laboratories**

A reliable set of individual papers was not verified in the search results available for this response. The results returned database landing pages rather than specific papers with usable article records. To avoid inventing citations or recommending unverified papers, the following are targeted searches to paste directly into scholarly databases.

## Copy-pasteable search queries

### Start with direct methods

1. `"grasp success detection" AND robot AND camera AND vision`

2. `"robotic manipulation" AND "grasp verification" AND visual`

3. `"fiducial marker" AND robot AND object localization AND camera`

4. `"ArUco marker" AND robotic manipulation AND pose estimation`

5. `"visual servoing" AND robot AND object placement AND camera`

6. `"robot anomaly detection" AND camera AND manipulation`

7. `"laboratory automation" AND computer vision AND fault detection`

8. `"autonomous experimentation" AND vision AND anomaly detection`

### Narrow toward your electrochemical setup

9. `("electrochemical cell" OR potentiostat) AND robotic automation AND camera`

10. `("electrochemical testing" OR electrocatalyst) AND "autonomous laboratory" AND vision`

11. `("sample positioning" OR "sample placement") AND electrochemical cell AND robot`

12. `("liquid handling" OR dipping OR immersion) AND robot AND visual inspection`

13. `("depth estimation" OR "insertion depth") AND robotic manipulation AND camera`

14. `("human-in-the-loop" OR "operator intervention") AND robot fault detection AND vision`

## Recommended databases

- **Google Scholar** for broad searches and citation chaining.
- **IEEE Xplore** for robotic manipulation, computer vision, fiducial-marker, and fault-detection methods.
- **Springer Nature Link** for robotics and computer-vision journal articles.
- **Connected Papers** for finding related work from a particularly good seed paper.
- **Preprints.org** for recent multidisciplinary work, while checking whether a preprint has subsequently appeared in a peer-reviewed venue.

For this project, search IEEE Xplore first for manipulation and fault-detection methods, then Google Scholar for autonomous-laboratory and electrochemical-automation applications.

## Inclusion checklist

Keep a paper if it satisfies at least two of these:

- Uses a camera to verify an object, robot action, placement, insertion, grasp, or experiment state.
- Reports measurable performance such as detection accuracy, false alarms, missed faults, latency, or robustness to lighting and viewpoint changes.
- Describes a setup that could plausibly transfer to a fixed-camera laboratory cell.
- Provides implementation details such as marker type, camera geometry, image-processing steps, thresholds, calibration, or failure cases.
- Includes an explicit response to uncertainty or failure, such as stopping the robot, requesting human review, or retrying an action.

## Exclusion checklist

Deprioritize papers that:

- Only perform object recognition without connecting the result to robot control or experimental verification.
- Require large datasets or deep-learning hardware when your first implementation is intended to use markers and image comparison.
- Study visual inspection of manufactured parts with no comparable robot or laboratory workflow.
- Report only simulation results when your system must operate around a real potentiostat and electrochemical cell.
- Use a camera only for navigation and do not verify sample identity, grasp success, placement, or stability.

## Best search order for your fault checks

1. **Right sample in the correct slot:**  
   Search `fiducial marker robot slot localization camera` and `template matching object presence robotic workstation`.

2. **Gripper successfully grabbed the sample:**  
   Search `robot grasp success detection vision` and `post-grasp object verification camera`.

3. **Correct dipping depth and placement:**  
   Search `robot insertion depth visual verification` and `camera-based immersion depth measurement robot`.

4. **Sample remains stable during testing:**  
   Search `visual monitoring object displacement robotic experiment` and `camera anomaly detection laboratory automation`.

5. **PASS/FAIL/UNCERTAIN logic:**  
   Search `robotic system uncertainty-aware visual inspection human intervention` and `confidence-based robot fault detection`.

## Three follow-up search terms

Start with these especially targeted combinations:

- `"grasp verification" AND "fiducial marker" AND robot`
- `"immersion depth" AND camera AND robotic experiment`
- `"autonomous laboratory" AND "fault detection" AND computer vision`

When you find the strongest papers, paste or upload them and run `/match`; the papers can then be evaluated against your xArm6, camera, electrochemical-cell, and PASS/FAIL/UNCERTAIN workflow.
