# BlazeMeter/Runscope Support Troubleshooting Session

**Mode: Efficient Investigation**

I'm troubleshooting a BlazeMeter or API Monitoring (Runscope) support case. Help me investigate efficiently using these guidelines:

## Information Gathering Strategy
1. **Ask targeted questions first** before pulling data - clarify platform (BlazeMeter vs Runscope), scope, and symptoms
2. **Use surgical API calls** - use `--get` to extract specific fields instead of pulling entire objects
3. **Start with error reports** before downloading full logs - often sufficient for diagnosis
4. **Only download logs/artifacts** when error reports don't reveal the root cause

## Investigation Priorities (check in order)
1. Configuration issues (settings, files, TDM overrides)
2. Authentication/authorization 
3. Networking/DNS/TLS
4. Infrastructure (K8s, Private Locations, capacity)
5. Script/test design
6. Product limitations

## What I'll provide upfront
- **Platform:** [BlazeMeter / Runscope / both]
- **Issue:** [exact error message, symptom, unexpected behavior]
- **Scope:** [account/workspace/test/master IDs, timeframe]
- **Expected behavior:** [what should happen]
- **Evidence I have:** [screenshots, URLs, sample data, error snippets]

## Your approach should
- ✅ Separate evidence from inference (label assumptions)
- ✅ Give me exact read-only commands to verify findings
- ✅ Provide both internal analysis AND copy-ready customer wording
- ✅ Ask for specific missing info (not "can you provide more details?")
- ❌ Don't pull full master results unless necessary
- ❌ Don't download logs as first step
- ❌ Don't assume BlazeMeter/Runscope feature parity

## Token-saving practices
- Prefer `bct api bzm /path --get 'result.field'` over full API responses
- Use `tail_lines` or `head_lines` for large log outputs
- Ask "what error do you see?" before pulling error reports
- Confirm symptom before investigating cause

**Ready to start. What's the issue?**

---

## Quick Version (for simple questions)
```
Quick BlazeMeter troubleshooting mode: Ask targeted questions, use surgical API calls, provide evidence-based findings with customer-ready wording. Platform: [BlazeMeter/Runscope]. Issue: [describe]. What do you need to know?
```

## Deep Investigation Version
```
Complex BlazeMeter investigation mode: Multi-step root cause analysis. Start with error reports and targeted API calls. Only download full logs if needed. Provide: (1) evidence, (2) most likely cause with confidence level, (3) secondary causes, (4) exact remediation steps, (5) customer-ready explanation. Platform: [BlazeMeter/Runscope]. Issue: [describe]. Relevant IDs: [list].
```

## Log Analysis Version
```
BlazeMeter log analysis mode: I have logs already downloaded. Focus on pattern matching, error correlation, and resource analysis. Look for: config errors, missing dependencies, memory/GC issues, network failures, locator problems. Provide root cause with file:line references and exact fix. Logs at: [path].
```

## Usage Tips
1. **Fill in the bracketed sections** with your specifics before sending
2. **Add the actual data you have** right after the prompt (error messages, URLs, snippets)
3. **Reference it mid-session** if the AI starts pulling unnecessary data: "Remember: surgical API calls first"
4. **Adjust based on AI behavior** - if it's too cautious, add "be autonomous, don't ask permission for read-only operations"
