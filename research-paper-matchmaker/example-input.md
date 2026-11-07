# Example Input: Research Paper Matchmaker

**Before you paste:** Download and attach the CRESt paper to the chat:
Zhang, Ren, Hsu, Chen, et al., "A multimodal robotic platform for multi-element electrocatalyst discovery," *Nature* (2025). https://www.nature.com/articles/s41586-025-09640-5

Then copy and paste the text below into your ArtesAI agent chat:

```text
/match

My project: I work in Dr. Abdelhafiz's autonomous materials lab at FSU. We have a robotic arm (xArm6) that picks up catalyst samples, dips them into an electrochemical cell, and runs tests with a potentiostat. I am building a fault-detection layer that uses cameras to check each step before the robot moves on: is the right sample in the slot, did the gripper actually grab it, is it dipped to the right depth, and is it still in place during the test. Each check returns PASS, FAIL, or UNCERTAIN, and a FAIL stops the robot and emails a person. I want to use simple computer vision first (markers and image comparison) and only add machine learning if needed.

I attached the CRESt paper. Is it useful for my project, and which parts should I focus on?
```
