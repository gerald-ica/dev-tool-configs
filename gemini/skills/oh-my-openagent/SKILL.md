---
name: oh-my-openagent
description: Multi-agent orchestration framework for AI-driven software development. Coordinates specialized discipline agents (Sisyphus, Hephaestus, Prometheus, Oracle, Librarian, Explore) for task decomposition, parallel execution, and self-improvement loops. Use when orchestrating multiple AI agents, building multi-model workflows, or handling complex development tasks with parallel agents.
version: "1.0.0"
license: See LICENSE in repository
metadata:
  homepage: "https://github.com/code-yeongyu/oh-my-openagent"
  openclaw:
    emoji: "🤖"
    homepage: "https://github.com/code-yeongyu/oh-my-openagent"
    requires:
      bins:
        - node
      anyBins:
        - npm
        - pnpm
        - bun
---

# oh-my-openagent

Multi-model, multi-agent orchestration framework for software development. Coordinates specialized AI agents working in parallel to solve complex tasks. Published as `oh-my-opencode`.

## What It Does

Decomposes development tasks into sub-tasks assigned to specialized "Discipline Agents" that execute in parallel across multiple LLMs, with self-verification loops.

## Discipline Agents

| Agent | Role |
|-------|------|
| **Sisyphus** | Repetitive/iterative tasks |
| **Hephaestus** | Code crafting and implementation |
| **Prometheus** | Knowledge discovery and learning |
| **Oracle** | Prediction and analysis |
| **Librarian** | Documentation and knowledge management |
| **Explore** | Codebase exploration and navigation |

## Setup

```bash
# Install globally
npm install -g oh-my-opencode
# or
pnpm add -g oh-my-opencode
```

**Supports:** Claude, Kimi, GLM-5, GPT-5.4, Gemini, and other LLMs.

## Key Features

- **Multi-model orchestration**: Route tasks to different LLMs with fallback strategies
- **Parallel agent execution**: Multiple discipline agents work simultaneously
- **Hash-Anchored Edit Tool (Hashline)**: Content hash validation for safe concurrent code edits
- **AST-Grep integration**: Precise code navigation and refactoring via Abstract Syntax Trees
- **LSP support**: Language Server Protocol integration for IDE-quality features
- **Ralph Loop**: Self-referential execution for task verification and iteration
- **MCP integration**: Web search (Exa), docs lookup (Context7), GitHub code search (Grep.app)
- **Tmux integration**: Full terminal-based agent workflows

## Usage

```bash
# Interactive CLI
oh-my-opencode "Refactor the authentication module to improve security"

# System decomposes task across agents:
# - Explore: Analyze current implementation
# - Oracle: Identify risks
# - Hephaestus: Implement improvements
# - Librarian: Update documentation
# - Ralph Loop: Verify changes
```

## Configuration (JSONC)

```jsonc
{
  "models": {
    "primary": "claude-opus",
    "fallback": "gpt-4"
  },
  "agents": {
    "parallelism": 4,
    "timeout": 300
  },
  "mcp": {
    "enabled": true,
    "services": ["web-search", "documentation"]
  }
}
```

## When to Use This Skill

- Orchestrating multiple AI agents for complex development tasks
- Building multi-model workflows with fallback strategies
- Handling large refactoring projects with parallel agent execution
- Implementing safe concurrent code modifications
- Setting up self-verifying agent loops (Ralph Loop pattern)
- Integrating AST-based code analysis into agent workflows
