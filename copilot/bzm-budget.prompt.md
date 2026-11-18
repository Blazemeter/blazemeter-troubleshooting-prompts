---
description: 'Budget Mode: token-limited BlazeMeter/Runscope troubleshooting'
---

Mode: BUDGET

Case: [BlazeMeter / Runscope] | Symptom: [exact error or behavior] | Expected: [what should happen]
IDs: [account / workspace / test / master] | Timeframe: [ ]
Evidence: [paste the error line(s), URL, screenshot notes. Paste snippets, not whole logs.]
Resume notes: [paste case-notes.md here if continuing a case, else "new case"]

Hard limits (rules, not preferences):
1. Modules: load only the system-prompt modules this step needs (usually investigation, then tooling-and-apis). Never load scripting, scriptless-gui, or references unless the case is about them. Never echo a module's text.
2. Hypothesis first: before any tool call, name the top 2 likely causes (core cause order: config > auth > network/DNS/TLS > infra > product limit > script) and the ONE cheapest check that tells them apart. Run only that check.
3. Output cap: every tool output under 50 lines. Never cat a whole file or print a full API response. Use `--get`, `jq` with named fields, `grep`, `head`/`tail`.
4. Evidence ladder: what I pasted > error report / session status > filtered API fields > grepped logs > full log download. Climb one rung at a time, and only when the rung below can't explain it.
5. Checkpoint: after 8 tool calls, stop. Reply with status (under 10 lines), what's ruled out, and the next best check. Wait for "go".
6. Notes: keep `case-notes.md` (under 30 lines: symptom, IDs, ruled out, evidence, current hypothesis, next check). Update it after each finding so I can resume in a fresh chat.
7. Replies under 150 words while investigating. Label each finding Evidence or Inference. No restating my input.
8. Missing info: ask one specific question in the same reply, then continue with what you can.
9. Read-only unless I confirm a specific command.

When I say "wrap up": give root cause with confidence, remediation steps, validation, and copy-ready customer wording (plain text, under a short label).
