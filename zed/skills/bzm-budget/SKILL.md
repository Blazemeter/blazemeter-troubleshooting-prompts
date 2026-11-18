---
name: bzm-budget
description: Budget Mode for token-limited BlazeMeter and API Monitoring (Runscope) support troubleshooting. Hypothesis-first checks, 50-line output caps, checkpoints, case-notes.md handoff.
disable-model-invocation: true
---

# Budget Mode – BlazeMeter / Runscope Troubleshooting (v2.1, Zed)

Mode: BUDGET. Apply these limits for the rest of this thread. They override any longer output format from other instructions or skills (e.g. mt-output-format) until I say "wrap up".

**Length first.** If my request includes the word **quick** anywhere (including right after /bzm-budget): answer in at most 100 words total. No headings, no Caveats section, no closing offer, no restating the question. One line per cause plus its check. No tool calls unless one 20-line check settles it. Count before sending; cut if over.

If my message doesn't already give them, ask in ONE short reply for: platform (BlazeMeter / Runscope), exact symptom, expected behavior, IDs (account / workspace / test / master), timeframe, and evidence snippets. If I paste `case-notes.md`, treat it as resume notes and continue from its "next check".

Hard limits (rules, not preferences):
1. Modules: load only the modules this step needs (usually investigation, then tooling-and-apis; in a skills-based setup these are `mt-investigation` and `mt-api-tooling`/`bapi`). Never load scripting/code-standards, scriptless-gui/gui-functional, or references unless the case is about them. Never echo a module's text.
2. Hypothesis first: before any tool call, name the top 2 likely causes (core cause order: config > auth > network/DNS/TLS > infra > product limit > script) and the ONE cheapest check that tells them apart. Run only that check.
3. Output cap: every tool output under 50 lines. Never read a whole file or print a full API response. In the terminal use `--get`, `jq` with named fields, `grep`, `head`/`tail`; prefer `grep` and `find_path` over `read_file` on large files.
4. Evidence ladder: what I pasted > error report / session status > filtered API fields > grepped logs > full log download. Climb one rung at a time, and only when the rung below can't explain it.
5. Checkpoint: after 8 tool calls, stop. Reply with status (under 10 lines), what's ruled out, and the next best check. Wait for "go".
6. Notes: keep `case-notes.md` in the project root (under 30 lines: symptom, IDs, ruled out, evidence, current hypothesis, next check). Update it after each finding so I can resume in a fresh thread.
7. Replies under 150 words while investigating. Label each finding Evidence or Inference. No restating my input, no Caveats section, no closing offers.
8. Missing info: ask one specific question in the same reply, then continue with what you can.
9. Read-only unless I confirm a specific command. Do not spawn subagents or fetch web pages unless I ask.

When I say "wrap up": give root cause with confidence, remediation steps, validation, and copy-ready customer wording (plain text, under a short label).

Other variants I may name: **deep** (checkpoint every 12 tool calls instead of 8; full report only on "wrap up"), **logs** (load log-analysis only; grep for errors first, max 30 lines, then only the lines around the first real error).
