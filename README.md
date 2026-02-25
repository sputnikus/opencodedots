# OpenCode Configuration

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
│   ├── code-review.md              # @code-review agent definition
│   ├── explore.md                  # @explore agent (enhanced)
│   ├── general.md                  # @general agent (enhanced)
│   ├── librarian.md              # @librarian agent (external research)
│   └── oracle.md                   # @oracle agent (consultation)
│   └── code-review.md              # @code-review agent definition
├── commands/
│   └── code-review.md              # /code-review command
└── skills/
    ├── karpathy-guidelines/        # LLM coding best practices
    │   └── SKILL.md
    └── security-awareness/         # Security threat detection
        └── SKILL.md
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

- **`@oracle`**: Read-only high-IQ consultant
  - Architecture and complex decision consultation
  - Debugging after 2+ failed attempts
  - Security/performance analysis
  - Multi-system tradeoff evaluation

- **`@librarian`**: External reference librarian
  - Official documentation lookup (Context7)
  - OSS implementation examples
  - Library best practices and patterns
  - Security guidance for unfamiliar libraries

- **`@explore`** (built-in, enhanced): Contextual codebase exploration
  - Pattern discovery and conventions
  - Module relationship mapping
  - Pre-implementation research

- **`@general`** (built-in, enhanced): Category-spawned execution
  - Domain-specific task execution
  - Parallel task delegation
  - Sisyphus-Junior equivalent

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

## Philosophy

This configuration follows these principles:

1. **Minimal but complete**: Start small, add only what's needed
2. **Delegation-first**: Encourage agents to use specialized subagents
3. **Verification**: Validate with tools, not just analysis
4. **Security**: Built-in awareness of common threats

## Future Enhancements

Planned additions for the work machine setup:

- [x] Additional subagents (oracle, librarian, explore, general)
- [ ] Custom build/plan prompts with delegation encouragement
- [ ] Workflow commands (/plan, /research, /consult)
- [ ] Additional MCP servers (filesystem, context7)

## References

This configuration draws inspiration from:

- [oh-my-opencode](https://github.com/code-yeongyu/oh-my-opencode) - Multi-agent orchestration concepts
- [OpenAI Codex](https://github.com/openai/codex) - Prompt structure and agent patterns
- [Superpowers](https://github.com/obra/superpowers) - Skill-based workflow enforcement

## License

MIT License - see [LICENSE](LICENSE) file for details.

---

**Note**: This is a personal configuration. Adapt to your needs.
