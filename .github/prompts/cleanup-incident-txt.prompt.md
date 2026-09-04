---
name: "Clean Incident TXT Files"
description: "Delete incident-related text files from the current workspace, including CS*.txt and CS*.b64.txt artifacts."
argument-hint: "Optional: add exclusions or a different filename pattern"
agent: "agent"
---
Delete incident-related text artifacts from the current workspace.

Requirements:
- Target files whose names start with `CS` and end with `.txt` or `.b64`.
- Include normal response or escalation text files, Base64 artifacts such as `.b64.txt`, and raw Base64 files such as `.b64`.
- Briefly identify the matching files before deleting them.
- Delete only the matching files.
- Verify the matching files are gone.
- Summarize what was removed and mention any incident-related files left behind because they did not match the pattern.

If the user includes extra prompt arguments, apply them when they do not conflict with the deletion goal.
