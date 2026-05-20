# PROJECT KNOWLEDGE BASE

**Project:** OpenCode Configuration Workspace
**Type:** AI Tooling / Configuration
**VCS:** Jujutsu (jj) — agents MUST NOT commit, push, or manipulate VCS
**Generated:** 2026-02-25 — updated 2026-05-19 for oh-my-opencode-slim migration
**Scope:** AI agents and security guidelines

---

## OVERVIEW

This is an OpenCode configuration workspace powered by [oh-my-opencode-slim](https://github.com/alvinunreal/oh-my-opencode-slim). The plugin provides a team of specialized agents (orchestrator, oracle, librarian, explorer, designer, fixer) with automatic delegation. Model presets manage which AI models each agent uses.

| Preset | Purpose |
|--------|---------|
| `openai` | **Work** — OpenAI models (active by default) |
| `whitescars` | **Work** — Fast OpenAI models (gpt-5.5-fast / gpt-5.3-codex-spark) |
| `alphalegion` | **Personal** — Opencode Go models (deepseek-v4-pro, kimi-k2.6) |
| `gozen` | **Personal** — Opencode Go free-tier models |

**Custom agent retained:**
- **Planner agent** (`@planner`): Writable strategic planning with decision-complete output — the only custom agent kept from the original configuration

---

## STRUCTURE

```
.
├── opencode.jsonc              # Workspace settings, model, plugin, MCP servers
├── oh-my-opencode-slim.json    # Plugin config — openai preset + agent models
├── agents/
│   └── planner.md              # @planner agent (strategic planning)
└── LICENSE                     # MIT License
```

---

## FILE ROLES

| File | Purpose |
|------|---------|
| `opencode.jsonc` | Workspace settings: main model, plugin registration, planner agent, MCP servers |
| `oh-my-opencode-slim.json` | Plugin configuration: active preset (`openai`), per-agent models/skills/MCPs |
| `agents/planner.md` | System prompt for the @planner primary agent |

---

## AGENTS

### oh-my-opencode-slim (plugin-managed)

| Agent | Role |
|-------|------|
| Orchestrator | Master delegator — main coding agent, routes work to specialists |
| Explorer | Codebase reconnaissance |
| Oracle | Strategic advisor and code review |
| Librarian | External documentation and library research |
| Designer | UI/UX implementation and visual polish |
| Fixer | Fast implementation specialist for scoped tasks |
| Council | Multi-LLM consensus (manual invocation) |
| Observer | Visual analysis (disabled by default) |

### Custom (workspace-managed)

| Agent | Role |
|-------|------|
| Planner | Strategic planning — decision-complete plans, interviews user, explores codebase |

---

## CONVENTIONS

**OpenCode-specific:**
- Agent files use **YAML frontmatter** with metadata
- Configuration uses JSONC (JSON with comments) format
- `oh-my-opencode-slim.json` selects preset and configures plugin-managed agents

**Content style:**
- Prompts are **instructional** — clear imperatives over descriptions
- Use concrete examples in skill documentation

---

## WHERE TO LOOK

| Task | Location | Notes |
|------|----------|-------|
| Change main model | `opencode.jsonc` | Edit `model` field |
| Change preset | `oh-my-opencode-slim.json` | Edit `preset` (e.g. `"openai"`, `"whitescars"`, `"alphalegion"`, `"gozen"`) |
| Change agent models | `oh-my-opencode-slim.json` | Edit `presets.<preset>.<agent>.model` |
| Change planner model | `opencode.jsonc` | Edit `agent.planner.model` |
| Change planner prompt | `agents/planner.md` | YAML frontmatter + markdown body |
| Add MCP server | `opencode.jsonc` | Add to `mcp` section |
| Switch preset at runtime | TUI | Use `/preset` command |
| Change skills per agent | `oh-my-opencode-slim.json` | Edit `presets.<preset>.<agent>.skills` |

---

## COMMANDS

No build/test commands — this is a configuration repository. To use:

1. Install OpenCode CLI: `npm install -g opencode`
2. Install plugin: `bunx oh-my-opencode-slim@latest install`
3. Run from workspace: `opencode`
4. Use agents: `@agent-name` (e.g., `@planner design the auth system`)

### Preset Switching

Switch between model presets at runtime:
```
/preset openai       # Use OpenAI models throughout
/preset whitescars   # Use fast OpenAI models
/preset alphalegion  # Use Opencode Go models
/preset gozen        # Use Opencode Go free-tier models
```

---

## SKILLS

Workspace-local skills (in `skills/`):

| Skill | Assigned to | Purpose |
|-------|------------|---------|
| ast-grep | explorer, fixer | Structural code search with AST patterns |
| exa-search | librarian | Web search via Exa API |
| find-docs | librarian | Context7 documentation and API reference lookup |
| karpathy-guidelines | oracle, fixer | Behavioral guardrails to reduce LLM coding mistakes |
| security-awareness | oracle, fixer | Phishing detection, credential protection, security review |

Orchestrator gets `*` (all skills) in all presets.

## NOTES

- **No tests** — validation happens through OpenCode's agent execution
- **No CI/CD** — configuration is deployed via OpenCode plugin system
- **openai preset** (default): orchestrator/oracle use `openai/gpt-5.5`, others use `openai/gpt-5.4-mini`
- **whitescars preset**: orchestrator/oracle use `openai/gpt-5.5-fast`, designer uses `openai/gpt-5.4`, others use `openai/gpt-5.3-codex-spark`
- **alphalegion preset**: orchestrator uses `opencode-go/deepseek-v4-pro`, oracle uses `openai/gpt-5.5`, designer uses `opencode-go/kimi-k2.6`, others use `opencode-go/deepseek-v4-flash`
- **gozen preset**: orchestrator uses `opencode-go/deepseek-v4-pro`, oracle uses `openai/gpt-5.5`, designer uses `opencode-go/kimi-k2.6`, others use `opencode/deepseek-v4-flash-free` (free tier). Switch via `/preset gozen`
- **Planner** uses `openai/gpt-5.5 (high variant)` with temperature 0.1 (same across presets)
