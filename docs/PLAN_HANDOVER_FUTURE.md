# Plan-Build Handover Implementation Guide

## Current Status (March 2026)

The automatic plan-to-build handover via `plan_exit` tool is **DISABLED** due to critical bugs in OpenCode's experimental plan mode.

### Known Issues

1. **Model Mismatch Bug** (Issue #9296)
   - Build phase uses plan agent's model instead of its own configured model
   - Results in tool call errors and invalid function patterns
   
2. **Forced Switching Behavior**
   - Experimental mode is "too eager" to jump to implementation
   - Even simple read-only tasks trigger unwanted handover
   
3. **Tool Disabled**
   - `plan_enter` tool temporarily disabled in OpenCode v1.2.12 (Feb 2026)
   - Changelog: "Temporarily disable plan enter tool to prevent unintended mode switches"

### Current Workaround

**Manual handover** - Plan agent presents completed plan, user manually switches to @orchestrator or @build agent.

See `agents/plan.md` "Step 4: Handoff" section for current implementation.

---

## Future Implementation (Once OpenCode Fixes Bugs)

When OpenCode resolves the handover issues, follow these steps to re-enable automatic handover:

### Step 1: Update Plan Agent Handoff Section

Replace the current manual handoff in `agents/plan.md`:

```markdown
### Step 4: Handoff

When plan is complete, use the `plan_exit` tool to signal completion and request handoff:

```
The plan is complete.

Summary: [1-2 sentences]
Key decisions: [bullet list]
Validation: [what specialists confirmed]

Ready to begin implementation?
```

Use `plan_exit` tool with:
- `agent`: "orchestrator" (recommended) or "build"
- `message`: Summary of plan completion

This will automatically switch to the implementation agent.
```

### Step 2: Update Planning Delegation Loop

Update the diagram in `agents/plan.md`:

```
Interview → Ground → Delegate Analysis → Synthesize → Delegate Validation → Refine → Handoff
            ↑________________|_____________________|________________|
```

(Change "Plan Complete" back to "Handoff")

### Step 3: Environment Configuration

Enable experimental plan mode:

```bash
export OPENCODE_EXPERIMENTAL_PLAN_MODE=1
opencode
```

Or add to your shell profile for permanent enablement.

### Step 4: Agent Configuration (opencode.jsonc)

Ensure agents are configured:

```jsonc
{
  "agent": {
    "plan": {
      "model": "openai/gpt-5.4",
      "variant": "xhigh",
      "temperature": 0.1
    },
    "orchestrator": {
      "model": "openai/gpt-5.4",
      "variant": "medium",
      "temperature": 0.1
    },
    "build": {
      "model": "openai/gpt-5.3-codex",
      "variant": "high",
      "temperature": 0.1
    }
  }
}
```

### Step 5: Verification Steps

After re-enabling, verify:

1. **Model correctness**: Ensure build/orchestrator uses its configured model, not plan's
2. **Tool availability**: Check that all expected tools are available after handover
3. **State preservation**: Verify plan context is properly passed to implementation agent
4. **User control**: Confirm user can still opt-out of automatic handover if desired

### Step 6: Update Documentation

Update this file to reflect the feature is enabled:
- Remove "DISABLED" warning
- Move workaround instructions to "Troubleshooting" section
- Update README.md and AGENTS.md to mention automatic handover

---

## Migration Checklist

Once OpenCode announces the fix:

- [ ] Update `agents/plan.md` Step 4 to use `plan_exit` tool
- [ ] Update delegation loop diagram
- [ ] Test handover with different model configurations
- [ ] Test handover opt-out (user says "No")
- [ ] Verify tool registry is correct after handover
- [ ] Update README.md plan section
- [ ] Update AGENTS.md with handover details
- [ ] Update this document to reflect enabled status
- [ ] Remove or archive this workaround document

---

## Related OpenCode Issues

- [#9055](https://github.com/anomalyco/opencode/issues/9055) - Switching from plan mode to build agent (Closed)
- [#9296](https://github.com/anomalyco/opencode/issues/9296) - Build uses plan agent's model (Open)
- [#17040](https://github.com/anomalyco/opencode/pull/17040) - Plugin-driven agent handoff (Closed - compliance issues)

## References

- [OpenCode Modes Documentation](https://opencode.ai/docs/modes/)
- [Experimental Plan Mode Changelog](https://github.com/anomalyco/opencode/blob/dev/CHANGELOG.md)

---

**Last Updated**: 2026-03-28
**Status**: Awaiting OpenCode fixes
**Workaround**: Manual agent switching (see plan.md)
