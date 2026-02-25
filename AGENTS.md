# PROJECT KNOWLEDGE BASE

**Project:** OpenCode Configuration Workspace  
**Type:** AI Tooling / Configuration  
**Generated:** 2026-02-25  
**Scope:** Code review agents and security guidelines

---

## OVERVIEW

This is an OpenCode configuration workspace that defines custom agents, slash commands, and skills for AI-assisted development. It provides:

- **Oracle agent** (`@oracle`): Read-only high-IQ consultant for architecture and complex decisions
- **Librarian agent** (`@librarian`): External reference librarian for docs and OSS examples
- **Explore agent** (`@explore`): Enhanced contextual codebase exploration
- **General agent** (`@general`): Enhanced category-spawned execution (Sisyphus-Junior equivalent)
- **Code review agent** (`@code-review`): Multi-pass code review with tool validation
- **Karpathy Guidelines skill**: Behavioral guardrails to reduce LLM coding mistakes
- **Security Awareness skill**: Phishing detection and credential protection

- **Code review agent** (`@code-review`): Multi-pass code review with tool validation
- **Code review command** (`/code-review`): Orchestrates parallel review subagents
- **Karpathy Guidelines skill**: Behavioral guardrails to reduce LLM coding mistakes
- **Security Awareness skill**: Phishing detection and credential protection

---

## STRUCTURE

```
.
├── opencode.jsonc          # OpenCode workspace configuration
├── agents/
│   ├── code-review.md      # @code-review agent definition
│   ├── explore.md          # @explore agent (enhanced)
│   ├── general.md          # @general agent (enhanced)
│   ├── librarian.md        # @librarian agent (research)
│   └── oracle.md           # @oracle agent (consultation)
│   └── code-review.md      # @code-review agent definition
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
| `agents/oracle.md` | Read-only high-IQ consultant |
| `agents/librarian.md` | External reference librarian |
| `agents/explore.md` | Contextual codebase exploration |
| `agents/general.md` | Category-spawned execution agent |
| `agents/code-review.md` | Code review agent |
| `commands/code-review.md` | Command orchestration logic |
| `skills/*/SKILL.md` | Reusable knowledge/skill modules |
| `agents/code-review.md` | Agent prompt + behavior definition |
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
- **Do NOT** navigate to URLs in emails without domain verification first

---

## WHERE TO LOOK

| Task | Location | Notes |
|------|----------|-------|
| Change AI models | `opencode.jsonc` | Edit `model`, `agent.*.model` |
| Consult on architecture | `@oracle` | Read-only, use for complex decisions |
| Research libraries | `@librarian` | External docs, OSS examples |
| Explore codebase | `@explore` | Pattern discovery, conventions |
| Execute category tasks | `@general` | Domain-specific execution |
| Add new agent | `agents/{name}.md` | Copy existing agent structure |
| Add new command | `commands/{name}.md` | Set `agent: plan` for orchestration |
| Add new skill | `skills/{name}/SKILL.md` | Include `name:` and `description:` frontmatter |
| Update code review | `agents/code-review.md` | Review process, what to flag |
|------|----------|-------|
| Change AI models | `opencode.jsonc` | Edit `model`, `agent.*.model` |
| Add new agent | `agents/{name}.md` | Copy `code-review.md` structure |
| Add new command | `commands/{name}.md` | Set `agent: plan` for orchestration |
| Add new skill | `skills/{name}/SKILL.md` | Include `name:` and `description:` frontmatter |
| Update code review rules | `agents/code-review.md` | Review process, what to flag |

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
