# Budget Mode – BlazeMeter / Runscope Troubleshooting (v2.0)

Token-limited troubleshooting for support cases. Designed to sit on top of the modular system prompt in [`Blazemeter/blazemeter-system-prompt`](https://github.com/Blazemeter/blazemeter-system-prompt) v3 (`core.md` always on, modules loaded on demand). It also works on its own.

Copy everything below the cut line into the first message of a NEW chat, fill in the brackets, and send it with your evidence in the same message.

## ✂️ CUT BELOW THIS LINE

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

---

## Variants (each is a one-message start; same core rules apply)

**Quick** (one question, no tools expected):
```
Mode: BUDGET, quick. Platform: [ ]. Question: [ ]. Answer in under 100 words from the core rules; no tool calls unless one 20-line check settles it.
```

**Deep** (multi-step root cause; still budgeted):
```
Mode: BUDGET, deep. Platform: [ ]. Symptom: [ ]. IDs: [ ]. Evidence: [ ]. Same hard limits, checkpoint every 12 tool calls instead of 8. Full report only on "wrap up".
```

**Logs in hand:**
```
Mode: BUDGET, logs. Logs at: [path]. Load the log-analysis module only. Grep for errors first (max 30 lines), then open only the lines around the first real error. Give root cause with file:line and the fix.
```

## How to spend less (habits, not prompt text)

- **One phase, one chat.** Context is resent on every turn, so turn 40 of one long chat costs far more than turn 4 of a new one. When a phase ends (triage done, cause found), start a new chat and paste `case-notes.md` as "Resume notes".
- **Pick the cheaper model for grunt work.** Grepping logs and pulling fields don't need the premium model; switch up only for the reasoning step. Premium models carry a higher multiplier against your monthly allowance.
- **Paste the error, not the log.** The single most expensive thing in a session is a big log or JSON landing in context, because it is then resent on every turn after.
- **Steer early.** If the agent starts pulling too much, reply: `Budget: hypothesis first, 50-line cap, one check.`
- **Install the modular core, not the bundle.** In Copilot, `core.md` as `.github/copilot-instructions.md` plus `.github/modules/` costs about a quarter of the full bundle per turn, before any module loads.

## Copilot prompt file

`copilot/bzm-budget.prompt.md` is the same prompt as a VS Code Copilot prompt file. Copy it to `.github/prompts/` in your repo and run it with `/bzm-budget` in Copilot Chat.
