# OpenCode Configuration

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Personal and work OpenCode configuration powered by [oh-my-opencode-slim](https://github.com/alvinunreal/oh-my-opencode-slim).

## Presets

| Preset | Purpose | Switch command |
|--------|---------|---------------|
| `openai` | **Work** — OpenAI models (gpt-5.5 / gpt-5.4-mini) | `/preset openai` (default) |
| `gozen` | **Personal** — mixed providers (deepseek, kimi, openai) | `/preset gozen` |

## Overview

This repository contains my OpenCode setup featuring:

- **[oh-my-opencode-slim](https://github.com/alvinunreal/oh-my-opencode-slim)** plugin for agent orchestration
- **Custom planner agent** (`@planner`) for writable strategic planning
- **Workspace skills** for structural code search, security awareness, and more
- **MCP servers** for database access (dbeaver), Linear, and Notion
- **Two model presets** — `openai` (work) and `gozen` (personal)

## Structure

```
.
├── AGENTS.md                       # Project knowledge base
├── LICENSE                         # MIT License
├── README.md                       # This file
├── oh-my-opencode-slim.json        # Plugin config — presets + skill assignments
├── opencode.jsonc                  # OpenCode workspace configuration
├── agents/
│   └── planner.md                  # @planner agent (writable strategic planning)
└── skills/
    ├── ast-grep/                   # Structural code search with AST patterns
    ├── exa-search/                 # Web search via Exa API
    ├── find-docs/                  # Context7 documentation lookup
    ├── karpathy-guidelines/        # LLM coding best practices
    └── security-awareness/         # Security threat detection
```

## Agents

### Plugin-managed (oh-my-opencode-slim)

| Agent | Role | openai model | gozen model |
|-------|------|-------------|------------|
| Orchestrator | Master delegator — main coding agent | `openai/gpt-5.5` | `opencode-go/deepseek-v4-pro` |
| Oracle | Strategic advisor, code review, debugging | `openai/gpt-5.5 (high)` | `openai/gpt-5.5 (high)` |
| Librarian | External docs, library research | `openai/gpt-5.4-mini` | `opencode-go/deepseek-v4-flash` |
| Explorer | Codebase reconnaissance | `openai/gpt-5.4-mini` | `opencode-go/deepseek-v4-flash` |
| Designer | UI/UX implementation | `openai/gpt-5.4-mini` | `opencode-go/kimi-k2.6` |
| Fixer | Fast scoped implementation | `openai/gpt-5.4-mini` | `opencode-go/deepseek-v4-flash` |
| Council | Multi-LLM consensus | preset-dependent | preset-dependent |

### Custom (workspace-managed)

| Agent | Role | Model | Notes |
|-------|------|-------|-------|
| Planner | Strategic planning — interviews user, explores codebase, produces decision-complete plans | `openai/gpt-5.5 (high)` | Primary agent. `edit: ask`, `bash: deny` |

## Skills

Workspace-local skills assigned to appropriate agents:

| Skill | Assigned to | Purpose |
|-------|------------|---------|
| ast-grep | explorer, fixer | Structural code search with AST patterns |
| exa-search | librarian | Web search via Exa API |
| find-docs | librarian | Context7 documentation and API reference lookup |
| karpathy-guidelines | oracle, fixer | Behavioral guardrails to reduce LLM coding mistakes |
| security-awareness | oracle, fixer | Phishing detection, credential protection, security review |

## MCP Servers

- **`dbeaver`**: Database access via DBeaver MCP server (read-only)
- **`linear`**: Linear issue tracking integration
- **`notion`**: Notion workspace integration

## Quick Start

```bash
# Install OpenCode and the plugin
npm install -g opencode
bunx oh-my-opencode-slim@latest install

# For skills used by gozen agents
npx skills add https://github.com/Leonxlnx/taste-skill
npx skills add backnotprop/bro-skills -g

# Run with this config
cd opencode_conf
opencode

# Switch presets at runtime
/preset openai     # Work — OpenAI models
/preset gozen      # Personal — mixed providers
```

## Configuration

- **`opencode.jsonc`**: Workspace settings — main model, plugin registration, planner agent, MCP servers
- **`oh-my-opencode-slim.json`**: Plugin configuration — active preset (`openai`), both presets defined with per-agent models/skills/MCPs, council config, todo continuation settings
- **`agents/planner.md`**: System prompt for the @planner agent

## Philosophy

1. **Delegation-first**: Agents delegate to specialists for optimal quality/speed/cost
2. **Verification**: Validate with tools, not just analysis
3. **Security**: Built-in awareness of common threats
4. **Separation of concerns**: Planning (planner) vs execution (orchestrator)

## Updates

To update the plugin to the latest version:

```bash
bunx oh-my-opencode-slim@latest install
```

## License

MIT License - see [LICENSE](LICENSE) file for details.

---

**Note**: `openai` is the work preset (active by default). `gozen` is my personal preset using alternative model providers. Use `/preset` to switch at runtime.
