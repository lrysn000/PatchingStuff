## The Task

In this assignment you will be provided six .zip files. Each **zip file** containing:

- A frozen snapshot of a real open-source project
- An `ISSUE.md` file describing a bug that was once reported against that project

Your job is to **fix the bug** and **produce a patch file** capturing your changes.

Part of the task is figuring out how to work with the project — reading its documentation, understanding its build system, and learning its conventions — without being told how. This is deliberate: in a real engineering role, you will not always be handed a setup guide. Working out how to get oriented, build the code, and run the tests is itself a skill, and one where AI assistance is available to you.

A good fix will address the behaviour described in `ISSUE.md`, follow the project's existing conventions rather than imposing your own style, and include or update tests in the manner the project expects. Whether and how well you achieve this is something you will reflect on in your report.

There is no starter code and no template. Approaching this the way a real contributor would — reading the code, understanding the conventions, forming a hypothesis, testing it — is part of the task.

--------

## Producing Your Patch

The zip file contains a plain folder snapshot with no git history. Before making any changes, initialise a repository and commit the original state so you have a clean baseline to diff against:

Then make your changes. When you are ready to generate the patch:  

-----

git diff > my-fix.patch

The patch file is the equivalent of a pull request diff. Include a brief header comment (lines beginning with `#`) at the top of the file describing what the fix does and how you verified it.

-------------

## The Report

Write a **single PDF of approximately 3000 words** covering the four parts below. This is a reflective document, not a structured Q&A. Write in continuous prose.

**Screenshot requirement:** Take screenshots throughout your entire AI interaction session — prompts, responses, corrections, dead ends, and all. From this full record, select **5 screenshots** that best illustrate the moments you discuss in your report, and collect them as a labelled appendix (Figure 1, Figure 2, … Figure 5). Each figure must have a caption. Each must be referenced by figure number at the relevant point in your narrative — a figure that appears only in the appendix without being discussed in the body earns no credit.

---

### Part 1 — Understanding the Codebase (~700 words)

Reflect on how you built a working understanding of an unfamiliar project. This covers everything before you began writing the fixes — how you oriented yourself, how you used AI as a tool for that orientation, and what you learned about the limits of that approach. Make sure to reflect on both issues you fixed.

Reference at least **2 figures** from your appendix within this part.

---

### Part 2 — Resolving the Issue (~1100 words)

Reflect on the process of moving from understanding the bug to producing a correct, convention-compliant fixes. Consider your interactions with AI throughout this process — what you asked, how those interactions evolved, where they succeeded, and where they did not. Consider also the moments where you stepped in yourself, and what drove those decisions. Make sure to reflect on both issues you fixed.

Reference at least **2 figures** from your appendix within this part.

---

### Part 3 — Quality and Craft (~500 words)

A fix that passes tests is not necessarily ready to be merged. Reflect on the quality of what you produced and what it would take for it to genuinely belong in the project. Make sure to reflect on both issues you fixed.

Reference at least **1 figure** from your appendix within this part.

---

### Part 4 — Broader Reflection (~700 words)

Step back from the technical work and reflect on AI as a tool for software engineering more broadly. Ground your response in what you actually experienced in this assignment — surface-level or generic commentary does not score here.

Consider: what it means to use AI as a coaching and learning tool rather than just an answer machine, where that framing holds and where it breaks down; the ethical implications of AI-assisted contributions to shared codebases and communities; where you would and would not reach for AI assistance in future engineering work, and why; and what this experience changed — or did not change — about how you think about the role of AI in the discipline.

---