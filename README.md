# harness-engineering

> Boostrap and enforce runtime system for AI agents

A Claude Code plugin that helps you set up new projects or add enforcement tooling to existing projects. It provides scaffolding, linting, formatting, testing infrastructure, and quality gates to keep your codebase maintainable.

## Features

- **Project Scaffolding**: Quick setup for Node/TypeScript, Python, C/C++, and Bun projects
- **Quality Enforcement**: Pre-commit hooks for linting, formatting, and secret scanning
- **Pre-push Hooks**: Test runner with SHA-based caching to skip unchanged code
- **CLAUDE.md Generation**: Auto-generates project documentation for AI agents
- **Quality Gates**: 300-line file limit, 50-line function limit, complexity checks

## Installation

1. Clone this repository to `~/.claude/plugins/harness-engineering`:
```bash
git clone https://github.com/nampq/harness-engineering.git ~/.claude/plugins/harness-engineering
```

2. Restart Claude Code

## Usage

Trigger the skill by saying:
- "Set up my project"
- "Add quality enforcement"
- "Harness this project"

The skill will guide you through:
1. **Environment Detection** - Identifies your stack
2. **Socratic Questions** - Understands what you're building
3. **Scaffolding** - Creates project structure
4. **Enforcement Installation** - Sets up hooks and tools
5. **CLAUDE.md Generation** - Creates AI-friendly documentation

## License

MIT &copy; 2026 Nam Pham
