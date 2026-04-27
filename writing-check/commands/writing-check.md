---
description: Scan a draft for AI writing tells and voice drift
allowed-tools: Read, Write, Grep, Glob
argument-hint: [file-or-text]
---

Run the writing-check skill against the provided draft.

If $ARGUMENTS is a file path, read the file first. If it's inline text, use it directly. If no arguments are provided, ask the user to paste or point to the draft they want checked.

Follow the full process defined in the writing-check skill:
1. Check for an existing voice profile (project-local or user-global). If neither exists, run the first-run setup flow before doing anything else.
2. Load the AI slop checklist and the user's voice profile.
3. Scan the draft for surface-level AI tells.
4. Run the detection-tool scan (perplexity, burstiness, texture, semantic predictability).
5. Report findings by severity, including detection-tool risk assessment.
6. Ask the user how they want to proceed.
