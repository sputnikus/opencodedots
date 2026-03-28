# PROJECT KNOWLEDGE BASE

**Project:** OpenCode Configuration Workspace  
**Type:** AI Tooling / Configuration
**VCS:** Jujutsu (jj) — agents MUST NOT commit, push, or manipulate VCS  
**Generated:** 2026-02-25  
**Scope:** AI agents and security guidelines

---

## OVERVIEW

This is an OpenCode configuration workspace that defines custom agents and skills for AI-assisted development. It provides:

- **Orchestrator agent** (`@orchestrator`): Pure manager/coordinator using OpenCode Ensemble plugin - never writes code, only delegates to parallel workers
- **Build agent** (`@build`): Autonomous implementation with delegation strategy
- **Plan agent** (`@plan`): Strategic planning with decision-complete output
- **Oracle agent** (`@oracle`): Read-only high-IQ consultant for architecture and complex decisions
- **Librarian agent** (`@librarian`): External reference librarian for docs and OSS examples
- **Explore agent** (`@explore`): Enhanced contextual codebase exploration
- **General agent** (`@general`): Enhanced generic execution
- **OpenCode Ensemble plugin**: Multi-agent team coordination with messaging, shared tasks, and parallel execution
- **CodeRabbit code-review skill**: AI-powered code review via CodeRabbit CLI
- **Karpathy Guidelines skill**: Behavioral guardrails to reduce LLM coding mistakes
- **Security Awareness skill**: Phishing detection and credential protection
- **AST-grep skill**: Structural code search with AST patterns
- **Exa Search skill**: Web search via Exa API
- **Find Docs skill**: Context7 documentation lookup

---

## STRUCTURE

```
.
├── opencode.jsonc          # OpenCode workspace configuration
├── agents/
│   ├── build.md                # @build agent (autonomous implementation)
│   ├── explore.md              # @explore agent (enhanced)
│   ├── general.md              # @general agent (enhanced)
│   ├── librarian.md            # @librarian agent (research)
│   ├── oracle.md               # @oracle agent (consultation)
│   ├── orchestrator.md         # @orchestrator agent (multi-agent teams)
│   └── plan.md                 # @plan agent (strategic planning)
├── skills/
│   ├── ast-grep/               # Structural code search with AST patterns
│   ├── coderabbit-code-review/ # CodeRabbit CLI code review
│   ├── exa-search/             # Web search via Exa API
│   ├── find-docs/              # Context7 documentation lookup
│   ├── karpathy-guidelines/    # LLM coding best practices
│   └── security-awareness/     # Security threat detection
└── LICENSE                 # MIT License
```
---

## FILE ROLES

| File | Purpose |
|------|---------|
| `opencode.jsonc` | Workspace settings, models, MCP servers, plugins |
| `agents/build.md` | Autonomous implementation agent |
| `agents/plan.md` | Strategic planning agent |
| `agents/oracle.md` | Read-only high-IQ consultant |
| `agents/librarian.md` | External reference librarian |
| `agents/explore.md` | Contextual codebase exploration |
| `agents/general.md` | Generic execution agent |
| `agents/orchestrator.md` | Multi-agent team orchestration with ensemble plugin |
| `skills/*/SKILL.md` | Reusable knowledge/skill modules |

---

## CONVENTIONS

**OpenCode-specific:**

- All agent files use **YAML frontmatter** with metadata
- Skills live in `skills/{name}/SKILL.md` with `name:` in frontmatter
- Agents set `mode: subagent` for composability
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
| Multi-agent team execution | `@orchestrator` | Uses OpenCode Ensemble plugin for parallel teams |
| Implement features | `@build` | Autonomous with delegation |
| Strategic planning | `@plan` | Decision-complete plans (manual handover, see docs) |
| Consult on architecture | `@oracle` | Read-only, complex decisions |
| Research libraries | `@librarian` | External docs, OSS examples |
| Explore codebase | `@explore` | Pattern discovery, conventions |
| Execute generic tasks | `@general` | Generic execution |
| Add new agent | `agents/{name}.md` | Copy existing agent structure |
| Add new command | `commands/{name}.md` | Set `agent: plan` for orchestration |
| Add new skill | `skills/{name}/SKILL.md` | Include `name:` and `description:` frontmatter |
| Code review | `skills/coderabbit-code-review/SKILL.md` | CodeRabbit CLI integration |
| Multi-agent plugin config | `opencode.jsonc` | `plugin: ["@hueyexe/opencode-ensemble"]` |
| Plan handover (future) | `docs/PLAN_HANDOVER_FUTURE.md` | Automatic handover once OpenCode fixes bugs |

---

## COMMANDS

No build/test commands — this is a configuration repository. To use:

1. Install OpenCode CLI: `npm install -g opencode`
2. Run from workspace: `opencode /command-name`
3. Or reference agents: `@agent-name`

### Code Review

Code review is provided via the `coderabbit-code-review` skill using CodeRabbit CLI:

1. Install CodeRabbit CLI: `npm install -g coderabbit` (or via Homebrew)
2. Authenticate: `coderabbit auth login`
3. Use the skill in OpenCode — it will automatically run `coderabbit review`

See `skills/coderabbit-code-review/SKILL.md` for details.

---

## NOTES

- **No tests** — validation happens through OpenCode's agent execution
- **No CI/CD** — configuration is deployed via OpenCode plugin system
- **Model configuration** specifies GPT-5 series models with variants (high/medium/xhigh)
- **Security skill** enforces credential protection even when coworkers request sharing
