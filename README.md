# OpenCode Configuration Workspace

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Personal OpenCode configuration for AI-assisted development on my work machine.

## Overview

This repository contains my customized OpenCode setup featuring:

- **Custom agents** for specialized tasks (code review, planning)
- **Skills** for consistent AI behavior (Karpathy guidelines, security awareness)
- **MCP servers** for extended capabilities (database access)
- **Model configuration** optimized for different agent roles

## Structure

```
.
├── AGENTS.md                       # Project knowledge base
├── LICENSE                         # MIT License
├── README.md                       # This file
├── opencode.jsonc                  # OpenCode workspace configuration
├── agents/
│   └── code-review.md              # @code-review agent definition
├── commands/
│   └── code-review.md              # /code-review command
└── skills/
    ├── karpathy-guidelines/        # LLM coding best practices
    │   └── SKILL.md
    └── security-awareness/         # Security threat detection
        └── SKILL.md
```

## Quick Start

1. **Install OpenCode CLI**:
   ```bash
   npm install -g opencode
   ```

2. **Clone this repository**:
   ```bash
   git clone <repo-url> ~/.config/opencode-work
   cd ~/.config/opencode-work
   ```

3. **Use the configuration**:
   ```bash
   opencode /code-review    # Run code review command
   opencode @code-review    # Invoke code-review agent
   ```

## Configuration

### Models

Configured models follow OpenAI Codex best practices:

| Agent | Model | Variant | Purpose |
|-------|-------|---------|---------|
| `build` | `openai/gpt-5.3-codex` | high | Complex implementation tasks |
| `plan` | `openai/gpt-5.2` | xhigh | Strategic planning |
| `general` | `openai/gpt-5.3-codex` | medium | General-purpose work |
| `explore` | `openai/gpt-5.3-codex-spark` | — | Fast discovery |
| `code-review` | `openai/gpt-5.3-codex` | — | Code review |
| `title`/`summary` | `opencode/gpt-5-nano` | — | Fast text tasks |

### Agents

- **`@code-review`**: Multi-pass code review with tool validation
  - 3 parallel review subagents (correctness, security, complexity)
  - Tool-assisted validation (linters, type checkers)
  - Risk-based analysis (HIGH/MEDIUM/LOW)

### Skills

- **`karpathy-guidelines`**: Behavioral guidelines to reduce LLM coding mistakes
  - Think before coding
  - Simplicity first
  - Surgical changes
  - Goal-driven execution

- **`security-awareness`**: Security threat detection and credential protection
  - Phishing detection
  - Domain verification
  - Credential handling
  - Social engineering defense

### MCP Servers

- **`dbeaver`**: Local DBeaver MCP server for database access (read-only)

## Usage

### Commands

```bash
# Run code review on uncommitted changes
opencode /code-review

# Invoke code-review agent directly
opencode @code-review
```

### Agents

Agents are specialized AI workers configured for specific tasks:

- **Plan agents** (`@plan`): Strategic planning and requirements analysis
- **Build agents** (`@build`): Implementation and coding tasks
- **Explore agents** (`@explore`): Codebase discovery and pattern finding
- **Review agents** (`@code-review`): Code review and quality assurance

## Philosophy

This configuration follows these principles:

1. **Minimal but complete**: Start small, add only what's needed
2. **Delegation-first**: Encourage agents to use specialized subagents
3. **Verification**: Validate with tools, not just analysis
4. **Security**: Built-in awareness of common threats
5. **Simplicity**: Follow Karpathy guidelines - minimum code that solves the problem

## Future Enhancements

Planned additions for the work machine setup:

- [ ] Additional subagents (oracle, librarian, explore)
- [ ] Custom build/plan prompts with delegation encouragement
- [ ] Workflow commands (/plan, /research, /consult)
- [ ] Additional MCP servers (filesystem, context7)
- [ ] Project-specific skills

## References

This configuration draws inspiration from:

- [OpenAI Codex](https://github.com/openai/codex) - Prompt structure and agent patterns
- [oh-my-opencode](https://github.com/code-yeongyu/oh-my-opencode) - Multi-agent orchestration concepts
- [Superpowers](https://github.com/obra/superpowers) - Skill-based workflow enforcement
- [Antigravity](https://antigravity.dev) - Agent-first IDE patterns

## License

MIT License - see [LICENSE](LICENSE) file for details.

---

**Note**: This is a personal configuration. Adapt to your needs.
