# BlazeMeter Troubleshooting Prompts

Reusable prompts for token-efficient AI troubleshooting of BlazeMeter and API Monitoring (Runscope) support cases, built for engineers working within a monthly Copilot allowance.

## What's here

- [`PROMPT.md`](PROMPT.md): **Budget Mode v2.0**, the main prompt, plus Quick, Deep, and Logs variants and spending habits.
- [`copilot/bzm-budget.prompt.md`](copilot/bzm-budget.prompt.md): the same prompt as a VS Code Copilot prompt file (`/bzm-budget`).
- [`zed/skills/bzm-budget/SKILL.md`](zed/skills/bzm-budget/SKILL.md): the same prompt as a Zed skill (`/bzm-budget` in Zed's Agent Panel).
- [`zed/bzm-profiles.json`](zed/bzm-profiles.json): two Zed agent profiles, **BZM Budget** and **BZM Investigate**, that trim the agent's tool list.

## Use it with the modular system prompt

1. Install the v3 modular system prompt from [`Blazemeter/blazemeter-system-prompt`](https://github.com/Blazemeter/blazemeter-system-prompt): `core.md` as `.github/copilot-instructions.md` and `modules/` as `.github/modules/`.
2. Copy `copilot/bzm-budget.prompt.md` to `.github/prompts/`.
3. For each case, open a new chat, run `/bzm-budget` (or paste the block from `PROMPT.md`), fill in the brackets, and include your evidence in the same message.
4. When a phase ends, start a fresh chat and paste `case-notes.md` as Resume notes.

## Use it in Zed (Zed Agent, any model incl. GitHub Copilot)

Zed has two pieces that map onto Budget Mode: **skills** (on-demand instructions you call with `/name`) and **agent profiles** (which tools the agent may use).

**1. System prompt.** Install the modular system prompt the same way as for VS Code (`core.md` → `.github/copilot-instructions.md`, `modules/` → `.github/modules/`). Zed's agent reads `.github/copilot-instructions.md` as project instructions. Zed uses only the *first* instruction file it finds (`.rules`, `.cursorrules`, `.windsurfrules`, `.clinerules`, `.github/copilot-instructions.md`, `AGENT.md`, `AGENTS.md`, …), so make sure the repo has none of the earlier ones.

**2. The `/bzm-budget` skill.** Global (every project):
```bash
mkdir -p ~/.agents/skills
cp -R zed/skills/bzm-budget ~/.agents/skills/
```
Or per project: copy it into `<repo>/.agents/skills/` (project skills load only in trusted worktrees). It's marked `disable-model-invocation`, so it runs only when you type `/bzm-budget`, never on its own.

**3. The profiles.** In Zed run `zed: open settings file`, and merge the `"profiles"` block from `zed/bzm-profiles.json` into your existing `"agent"` section (don't paste a second `"agent"` key). Save; no restart needed.

- **BZM Budget**: read, grep, find, list, terminal, skills, and edit/write (for `case-notes.md`). No web fetch, web search, subagents, file moves/deletes, or MCP servers. Every tool and MCP server you leave enabled sends its schema on every request, so the short list itself saves tokens.
- **BZM Investigate**: the same plus `fetch`, for when you need to check BlazeMeter docs.
- Need one MCP server (e.g. a BlazeMeter MCP)? Open the profile selector → **Configure** and turn on just that server for the profile.
- Optional: set a cheaper `default_model` on BZM Budget in the same modal so grunt work never burns premium requests.

**Per case:** open a new thread in the Agent Panel → pick **BZM Budget** in the profile selector → pick your model (e.g. GitHub Copilot) → type `/bzm-budget`, then the case, IDs, and evidence → send. Reply `go` at each checkpoint, `wrap up` at the end. Zed auto-compacts long threads at 90% of the context window; a fresh thread with `case-notes.md` pasted is still cheaper.

**Profiles don't apply to External Agents** (e.g. Copilot CLI or Claude Code run through Zed's ACP). For those, paste the block from `PROMPT.md` instead.

## Why it saves tokens

Agent mode resends the system prompt and the whole conversation on every tool call. Cost grows with (context size) x (number of steps). Budget Mode attacks both:

- **Smaller context:** modular core instead of the full bundle; 50-line cap on tool output; snippets instead of logs; a notes file so new chats start small.
- **Fewer steps:** hypothesis-first checks, an evidence ladder, and a checkpoint after 8 tool calls so a deep ticket can't run away unattended.

The v1 prototype's example (an empty-CSV-parameter case going from ~82,000 tokens unguided to an estimated ~5,000 guided) is an estimate, not a measurement.

## Version

**Current:** v2.1 (Budget Mode + Zed skill and profiles). v1 prototype is in git history.
