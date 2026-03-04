---
description: Review changes with parallel specialized subagents using multiple AI models for diverse perspectives
agent: plan
---

Review uncommitted changes by default. If no uncommitted changes, review the last commit. If the user provides a PR/MR number or link, fetch it with CLI tools first.

Guidance: $ARGUMENTS

## Multi-Model Code Review Architecture

This command orchestrates a 2-tier review system:
- **Tier 1**: Three specialized reviewers using Google Gemini models (diverse perspectives)
- **Tier 2**: One validator using OpenAI codex-5.3 (consistency and final verification)

### Tier 1: Specialized Area Reviewers (Parallel)

Launch THREE (3) specialized subagents in parallel, each with a different model and focus:

1. **@code-review-correctness** (Google Gemini 3 Flash)
   - Focus: Logic errors, type safety, edge cases, missing guards
   - Strength: Fast, cost-effective correctness validation
   - Model: `google/gemini-3-flash-preview`

2. **@code-review-security** (Google Gemini 3.1 Pro)
   - Focus: Authentication, injection risks, data exposure, cryptography
   - Strength: Deep reasoning for security analysis
   - Model: `google/gemini-3.1-pro-preview`

3. **@code-review-complexity** (Google Gemini 3 Flash)
   - Focus: Over-engineering, maintainability, abstraction quality, readability
   - Strength: Fast pattern matching for design concerns
   - Model: `google/gemini-3-flash-preview`

If the user guidance specifies areas, map them to these reviewers:
- "correctness", "bugs", "logic" → correctness reviewer
- "security", "auth", "injection" → security reviewer
- "complexity", "maintainability", "design" → complexity reviewer

### Tier 2: Validation Reviewer (Sequential)

After all three area reviewers complete:

1. **Deduplicate findings** — Keep the version with better evidence, use the higher severity when they disagree, and drop anything without a `file:line` reference

2. **Run lint/test** — Execute the project's lint and test commands to catch anything the reviewers missed

3. **Launch validator** — ONE (1) final @code-review subagent using `openai/gpt-5.3-codex`
   
   Pass it:
   - The compiled findings from all three reviewers
   - The user guidance
   - This instruction: "For each finding, read the code at the referenced file:line. Classify as **Confirmed** (provably real), **Disputed** (not supported by the code), or **Acknowledged** (real but not worth fixing). Return only Confirmed findings."

### Output

Present only **Confirmed** findings to the user, ranked by severity. Include:
- Which reviewer(s) originally flagged it
- The file:line reference
- Severity and category
- Evidence and suggested fix

If nothing survived validation, say so explicitly.
