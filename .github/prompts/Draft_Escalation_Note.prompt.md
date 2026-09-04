---
name: "Draft Escalation Note"
description: "Draft an internal escalation note for the active eRequest in the current session and save it as a .txt file in the workspace folder."
argument-hint: "Optional: add escalation emphasis or any extra context to include"
agent: "agent"
---
Draft an internal escalation note for the eRequest currently being worked on in this session.

Requirements:
- Identify the active incident or eRequest from the current session context, workspace files, or attached evidence.
- If the active incident cannot be identified with confidence, stop and ask only for the incident number.
- Treat this command as an instruction to complete the full escalation-note workflow without waiting for another prompt.
- Produce an internal escalation summary that states the issue, lists the evidence already provided, and explains why that evidence shows escalation is required.
- Keep the note support-internal rather than client-facing.
- Use the stronger SPSS reasoning style: direct, concrete, and evidence-based.
- If any external URLs were fetched during the investigation and those URLs contributed to the client-facing response (i.e., they were used to confirm root cause, support workaround recommendations, or shape the escalation rationale), include those URLs in an EXTERNAL SOURCES VERIFIED DURING INVESTIGATION section of the escalation note. URLs that were checked during investigation but did not contribute to the client response content do not need to be included.
- Save the escalation note as `<IncidentNumber>_Escalation_INT.txt` in the current workspace folder.
- Report the incident number used and the file created.

If the user includes extra prompt arguments, incorporate them when they do not conflict with the escalation-note workflow.
