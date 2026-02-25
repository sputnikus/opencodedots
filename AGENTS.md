# PROJECT KNOWLEDGE BASE

**Project:** OpenCode Configuration Workspace  
**Type:** AI Tooling / Configuration  
**Generated:** 2026-02-25  
**Scope:** Code review agents and security guidelines

---

## OVERVIEW

This is an OpenCode configuration workspace that defines custom agents, slash commands, and skills for AI-assisted development. It provides:

- **Build agent** (`@build`): Autonomous implementation with delegation strategy
- **Plan agent** (`@plan`): Strategic planning with decision-complete output
- **Oracle agent** (`@oracle`): Read-only high-IQ consultant for architecture and complex decisions
- **Librarian agent** (`@librarian`): External reference librarian for docs and OSS examples
- **Explore agent** (`@explore`): Enhanced contextual codebase exploration
- **General agent** (`@general`): Enhanced generic execution
- **Code review agent** (`@code-review`): Multi-pass code review with tool validation
- **Karpathy Guidelines skill**: Behavioral guardrails to reduce LLM coding mistakes
- **Security Awareness skill**: Phishing detection and credential protection
---
i
## STRUCTURE

```
.
├── opencode.jsonc          # OpenCode workspace configuration
├── agents/
│   ├── build.md                # @build agent (autonomous implementation)
│   ├── code-review.md          # @code-review agent definition
│   ├── explore.md              # @explore agent (enhanced)
│   ├── general.md              # @general agent (enhanced)
│   ├── librarian.md            # @librarian agent (research)
│   ├── oracle.md               # @oracle agent (consultation)
│   └── plan.md                 # @plan agent (strategic planning)
├── commands/
│   └── code-review.md      # /code-review slash command
├── skills/
│   ├── karpathy-guidelines/  # LLM coding best practices
│   └── security-awareness/   # Security threat detection
└── LICENSE                 # MIT License
```

---

## FILE ROLES

| File | Purpose |
|------|---------|
| `opencode.jsonc` | Workspace settings, models, MCP servers |
| `agents/build.md` | Autonomous implementation agent |
| `agents/plan.md` | Strategic planning agent |
| `agents/oracle.md` | Read-only high-IQ consultant |
| `agents/librarian.md` | External reference librarian |
| `agents/explore.md` | Contextual codebase exploration |
| `agents/general.md` | Generic execution agent |
| `agents/code-review.md` | Code review agent |
| `commands/code-review.md` | Command orchestration logic |
| `skills/*/SKILL.md` | Reusable knowledge/skill modules |
---

## CONVENTIONS

**OpenCode-specific:**

- All agent/command files use **YAML frontmatter** with metadata
- Skills live in `skills/{name}/SKILL.md` with `name:` in frontmatter
- Agents set `mode: subagent` for composability
- Commands set `agent: plan` for orchestration
- Configuration uses JSONC (JSON with comments) format

**Content style:**

- Prompts are **instructional** — clear imperatives over descriptions
- Use concrete examples in skill documentation
- Link to external sources for provenance (e.g., Karpathy tweet, 1Password SCAM)

---

## ANTI-PATTERNS (THIS PROJECT)

- **Do NOT** add logic to agent files — keep them declarative prompts only
- **Do NOT** commit `.env` or credential files (enforced by security skill)

---

## WHERE TO LOOK

| Task | Location | Notes |
|------|----------|-------|
| Change AI models | `opencode.jsonc` | Edit `model`, `agent.*.model` |
| Implement features | `@build` | Autonomous with delegation |
| Strategic planning | `@plan` | Decision-complete plans |
| Consult on architecture | `@oracle` | Read-only, complex decisions |
| Research libraries | `@librarian` | External docs, OSS examples |
| Explore codebase | `@explore` | Pattern discovery, conventions |
| Execute generic tasks | `@general` | Generic execution |
| Add new agent | `agents/{name}.md` | Copy existing agent structure |
| Add new command | `commands/{name}.md` | Set `agent: plan` for orchestration |
| Add new skill | `skills/{name}/SKILL.md` | Include `name:` and `description:` frontmatter |
| Update code review | `agents/code-review.md` | Review process, what to flag |
---

## COMMANDS

No build/test commands — this is a configuration repository. To use:

1. Install OpenCode CLI: `npm install -g opencode`
2. Run from workspace: `opencode /code-review`
3. Or reference agents: `@code-review`

---

## NOTES

- **No tests** — validation happens through OpenCode's agent execution
- **No CI/CD** — configuration is deployed via OpenCode plugin system
- **Model configuration** specifies GPT-5 series models with variants (high/medium/xhigh)
- **Security skill** enforces credential protection even when coworkers request sharing
