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
│   ├── explore.md              # @explore agent (enhanced)
│   ├── general.md              # @general agent (enhanced)
│   ├── librarian.md            # @librarian agent (external research)
│   ├── oracle.md               # @oracle agent (consultation)
│   └── plan.md                 # @plan agent (strategic planning)
└── skills/
    ├── ast-grep/               # Structural code search with AST patterns
    ├── coderabbit-code-review/ # CodeRabbit CLI code review
    ├── exa-search/             # Web search via Exa API
    ├── find-docs/              # Context7 documentation lookup
    ├── karpathy-guidelines/    # LLM coding best practices
    └── security-awareness/     # Security threat detection
```

## Configuration

### Models

Configured models follow OpenAI Codex best practices:

| Agent | Model | Variant | Purpose |
|-------|-------|---------|---------|
| `build` | `openai/gpt-5.3-codex` | high | Complex implementation tasks |
| `plan` | `openai/gpt-5.4` | xhigh | Strategic planning |
| `oracle` | `openai/gpt-5.4` | high | Architecture consultation |
| `general` | `openai/gpt-5.3-codex` | medium | General-purpose work |
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

- **`ast-grep`**: Structural code search using Abstract Syntax Tree patterns
  - Find code patterns that text search cannot handle
  - Locate specific language constructs (e.g., "async functions without error handling")
  - Match code based on structure rather than just text
  - Requires ast-grep CLI: `npm install -g @ast-grep/cli`

- **`coderabbit-code-review`**: AI-powered code review using CodeRabbit CLI
  - Finds bugs, security issues, and quality risks
  - Groups findings by severity (Critical, Warning, Info)
  - Supports staged, committed, or all changes
  - Requires CodeRabbit CLI: `npm install -g coderabbit`

- **`exa-search`**: Web search via Exa API for research and current information
  - Semantic web search with filters
  - Fetch contents from URLs
  - Find similar links
  - Grounded Q&A with streaming support
  - Requires Exa CLI and `EXA_API_KEY`

- **`find-docs`**: Documentation lookup via Context7 for up-to-date library docs
  - Query current documentation for any library
  - Get code examples and usage patterns
  - Version-specific documentation support
  - Covers setup, migration guides, and API docs
  - Requires Context7 CLI: `npm install -g ctx7`

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
- [x] Additional MCP servers (context7, grep-app, exa)
- [x] Code review via CodeRabbit CLI
- [x] Documentation lookup via Context7 (`find-docs` skill)
- [x] Web search via Exa (`exa-search` skill)
- [x] AST-based code search (`ast-grep` skill)
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
