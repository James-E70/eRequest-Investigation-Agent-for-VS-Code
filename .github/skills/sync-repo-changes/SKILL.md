---
name: sync-repo-changes
description: "Use when a workflow rule, guardrail, or behavioral change has been made to any agent file and needs to be propagated to all relevant files and committed to the GitHub repo."
disable-model-invocation: true
---
A change has been made (or a change is described below). Propagate it to every file that needs it, then commit and push to https://github.com/James-E70/eRequest-Investigation-Agent-for-VS-Code.

## Files to check and update

Before committing, review each of the following locations and update any that do not yet reflect the change. Not every file will need updating for every change — use judgment about relevance, but err on the side of inclusion for guardrails and workflow rules that affect response quality.

| File | Purpose |
|---|---|
| `.github/copilot-instructions.md` | Auto-loaded workspace instructions and the canonical source for investigation, guardrail, and workflow rules used during live support runs. Use leading-dash bullets, matching the file's existing convention. |
| `.github/skills/wisetech-support-response-consolidated/SKILL.md` | Standalone twin of `copilot-instructions.md` for colleagues who attach it without cloning the repo. Every rule change must be made in BOTH files in the same change set. Use blank-line-separated paragraphs with no leading dash, matching the file's existing convention. |
| `.github/skills/*/SKILL.md` (slash-command skills) | Slash-command skills (draft-escalation-note, triage-erequest, clean-incident-txt-files, kibana-performance-investigation, sync-repo-changes). Update if the change affects how investigations are initiated or how attachments/incidents are handled. |
| `.github/skills/wisetech-macro-assistant/SKILL.md` and `.github/instructions/macro-routing.instructions.md` | Macro rules and the auto-routing rule that loads them. Update if the change affects macro handling or its trigger conditions. |
| `/memories/support-agent-preferences.md` (user memory) | Persistent cross-workspace agent preferences. Update if the change is a behavioral rule that should apply in all workspaces and conversations, not just this repo. |
| `/memories/repo/` (repo memory) | Repo-scoped memory facts. Update if the change is a repo-specific fact, tool behavior note, or environment-specific rule. |

If an edit deliberately makes content exist in one of the two instruction files but not the other, document that divergence and the reasoning in `/memories/repo/duplicate-instruction-files.md` in the same change set.

## Local memory drift check (run every time)

Local repo memory files live in the VS Code extension's local storage and are NOT pushed to GitHub. Any colleague who clones the repo will not have them. After propagating the primary change, always run a drift check:

1. List the contents of `/memories/repo/` using the memory tool.
2. For each file found, read its full content.
3. Compare against `.github/copilot-instructions.md` and `.github/skills/wisetech-support-response-consolidated/SKILL.md` — check whether any fact, rule, or product-specific bullet point in the memory file is not already present in them.
4. For any content that is missing, add it to BOTH files under the appropriate existing section or a new clearly-named subsection, following each file's formatting convention. Do not duplicate content that is already there.
5. If a local memory file contains only ephemeral or session-specific notes with no lasting value, or only personal preferences scoped to one individual, note it but do not add it to the workspace files.
6. Include any changes from this drift check in the same commit as the primary change.

The five local-only product knowledge files first synced on 3 July 2026 (commit `0606d8b`) are:
- `/memories/repo/ap-xut-tpa-vs-ipp-job-resolution.md`
- `/memories/repo/emcs-change-of-destination-queue.md`
- `/memories/repo/forwarding-panel-divider-sizing.md`
- `/memories/repo/pave-web-404-routing.md`
- `/memories/repo/upg-loginforupgrade-runner-check.md`

Any new files created under `/memories/repo/` since that date are candidates for the drift check.

## Steps

1. Read the current content of each file in the **Files to check and update** table.
2. For each file that is missing the primary change, apply the update. Keep the wording consistent across files — the same rule should not mean different things in different files.
3. Run the **Local memory drift check** above and add any new content to both instruction files.
4. Run `git status` to confirm which files have been modified.
5. Stage all modified files with `git add`.
6. Commit with a message that describes what changed and why (include the root cause or incident reference if applicable). If the drift check added content, note it in the commit body.
7. Push to `origin main`.
8. Report the commit hash and a summary of which files were updated and which were already current.

## Notes

- Do not commit response files such as `CS########_response.txt` or `CS########_response.b64` — these are working artefacts, not repo content.
- Do not commit `.gitignore`-excluded files.
- If the change is to user memory only (not a repo file), note that it is local and not pushed to GitHub.
- If a file cannot be updated because it does not exist or the path is unclear, state that explicitly rather than silently skipping it.
