# BlazeMeter Troubleshooting Prompts

Reusable AI troubleshooting prompts optimized for token efficiency when investigating BlazeMeter and Runscope support cases.

## Purpose

These prompts help support engineers work with AI assistants (Claude, ChatGPT, Copilot, etc.) more efficiently by:
- Reducing token consumption through targeted investigation
- Establishing clear troubleshooting priorities
- Separating evidence from inference
- Providing both internal analysis and customer-ready responses

## Usage

Copy the appropriate prompt from [PROMPT.md](PROMPT.md) and paste it at the start of your AI troubleshooting session, then fill in the bracketed sections with your case details.

### Available Prompts

1. **Full Version** - Comprehensive troubleshooting session with all guidelines
2. **Quick Version** - For simple, straightforward issues
3. **Deep Investigation Version** - For complex multi-step root cause analysis
4. **Log Analysis Version** - When you already have logs downloaded

## Token Savings

Following these prompts can reduce token consumption by 90%+ compared to unguided investigation:
- Example: Empty CSV parameter investigation went from 82,000 tokens (unguided) to estimated ~5,000 tokens (guided)

## Key Principles

- Start with error reports before downloading logs
- Use surgical API calls (`--get 'result.field'`) instead of full responses
- Ask targeted questions before pulling data
- Provide both technical findings and customer-ready explanations
- Separate BlazeMeter and Runscope platforms (never assume feature parity)

## Feedback & Improvements

This is a living document. Contributions and refinements welcome based on real-world troubleshooting experiences.

## Version

**Current Release:** prototype
