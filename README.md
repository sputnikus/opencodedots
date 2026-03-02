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
│   ├── build.md                # @build agent (autonomous implementation)
│   ├── code-review.md          # @code-review agent definition
│   ├── explore.md              # @explore agent (enhanced)
│   ├── general.md              # @general agent (enhanced)
│   ├── librarian.md            # @librarian agent (external research)
│   ├── oracle.md               # @oracle agent (consultation)
│   └── plan.md                 # @plan agent (strategic planning)
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
| `oracle` | `openai/gpt-5.2` | high | Architecture consultation |
| `general` | `openai/gpt-5.3-codex` | medium | General-purpose work |
| `code-review` | `openai/gpt-5.3-codex` | — | Code review |
| `explore` | `openai/gpt-5.1-codex-mini` | — | Fast discovery |
| `librarian` | `openai/gpt-5.1-codex-mini` | — | External research |

### Agents

- **`@build`**: Autonomous implementation agent (primary)
  - Write, modify, and fix code with surgical precision
  - Delegates to @explore, @oracle, @librarian for parallel work
  - Verifies with linters, type checkers, tests

- **`@plan`**: Strategic planning agent (primary)
  - Analyzes complex tasks and coordinates work
  - Produces decision-complete execution plans
  - Interviews user, explores context before planning

- **`@code-review`**: Evidence-based code review with tool validation
  - Finds provable bugs, security issues, and design concerns
  - Validates with tools (linters, type checkers), not just inspection
  - Risk-based analysis (HIGH: auth/crypto/external; MEDIUM: business logic; LOW: UI)

- **`@oracle`**: Read-only high-IQ consultant
  - Architecture and complex decision consultation
  - Debugging after 2+ failed attempts, catches blind spots
  - Security/performance analysis with confidence levels
  - Multi-system tradeoff evaluation

- **`@librarian`**: External reference librarian
  - Official documentation lookup (Context7, API docs)
  - Production-quality OSS implementation examples
  - Library best practices and security guidance
  - Distinguishes documented facts from opinions

- **`@explore`** (built-in, enhanced): Contextual codebase exploration
  - Pattern discovery and conventions
  - Module relationship mapping
  - Pre-implementation research

- **`@general`** (built-in, enhanced): Fast execution agent for well-specified quick tasks
  - Quick task execution with minimal overhead
  - Following existing codebase patterns exactly
  - Surgical, minimal changes only
  - Evidence-based completion with verification

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
- [x] Custom build/plan prompts with delegation encouragement
- [ ] Additional MCP servers (context7, grep-app, exa)
- [ ] Alternative `@code-review` powered by Gemini model
- [ ] Workflow commands (/plan, /research, /consult)
- [ ] Build configuration package (template agents/commands/skills)

## References

This configuration draws inspiration from:

- [oh-my-opencode](https://github.com/code-yeongyu/oh-my-opencode) - Multi-agent orchestration concepts
- [OpenAI Codex](https://github.com/openai/codex) - Prompt structure and agent patterns
- [Superpowers](https://github.com/obra/superpowers) - Skill-based workflow enforcement
- [oh-my-pi](https://github.com/can1357/oh-my-pi) - System prompt design

## License

MIT License - see [LICENSE](LICENSE) file for details.

---

**Note**: This is a personal configuration. Adapt to your needs. For more fun
you might want to check my [OmO config](https://gist.github.com/sputnikus/287216dd23facabc32b72b487b77b182)
