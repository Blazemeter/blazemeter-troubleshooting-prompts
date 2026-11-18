# BlazeMeter Troubleshooting Prompts

Reusable prompts for token-efficient AI troubleshooting of BlazeMeter and API Monitoring (Runscope) support cases, built for engineers working within a monthly Copilot allowance.

## What's here

- [`PROMPT.md`](PROMPT.md): **Budget Mode v2.0**, the main prompt, plus Quick, Deep, and Logs variants and spending habits.
- [`copilot/bzm-budget.prompt.md`](copilot/bzm-budget.prompt.md): the same prompt as a VS Code Copilot prompt file (`/bzm-budget`).

## Use it with the modular system prompt

1. Install the v3 modular system prompt from [`Blazemeter/blazemeter-system-prompt`](https://github.com/Blazemeter/blazemeter-system-prompt): `core.md` as `.github/copilot-instructions.md` and `modules/` as `.github/modules/`.
2. Copy `copilot/bzm-budget.prompt.md` to `.github/prompts/`.
3. For each case, open a new chat, run `/bzm-budget` (or paste the block from `PROMPT.md`), fill in the brackets, and include your evidence in the same message.
4. When a phase ends, start a fresh chat and paste `case-notes.md` as Resume notes.

## Why it saves tokens

Agent mode resends the system prompt and the whole conversation on every tool call. Cost grows with (context size) x (number of steps). Budget Mode attacks both:

- **Smaller context:** modular core instead of the full bundle; 50-line cap on tool output; snippets instead of logs; a notes file so new chats start small.
- **Fewer steps:** hypothesis-first checks, an evidence ladder, and a checkpoint after 8 tool calls so a deep ticket can't run away unattended.

The v1 prototype's example (an empty-CSV-parameter case going from ~82,000 tokens unguided to an estimated ~5,000 guided) is an estimate, not a measurement.

## Version

**Current:** v2.0 (Budget Mode). v1 prototype is in git history.
