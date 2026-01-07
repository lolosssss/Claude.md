# Claude.md Templates

A collection of well-crafted CLAUDE.md files for Claude Code (Anthropic's agentic coding CLI tool). These files follow best practices from the community and are designed to help you onboard Claude to your codebase effectively.

## What is CLAUDE.md?

`CLAUDE.md` is a special file that Claude Code automatically pulls into context when starting a conversation. It's the highest-leverage configuration point for getting good results from Claude Code. The file serves to:

- **Onboard Claude to your codebase** by explaining the WHAT (tech stack), WHY (purpose), and HOW (workflows)
- **Provide universal rules** that apply across most tasks
- **Reference additional resources** for detailed information (progressive disclosure)

## Why This Repository Exists

Based on research and best practices from:

- **[Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)** by Kyle - Deep dive into CLAUDE.md theory and context engineering principles
- **[Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)** by Anthropic - Comprehensive guide to effective agentic coding workflows

This repository provides ready-to-use templates that follow these principles:

- **Less is more** - Keep CLAUDE.md concise and universally applicable
- **Progressive disclosure** - Reference detailed docs instead of duplicating content
- **Quality over quantity** - Focus on instructions that improve performance

## Available Templates

### Global Rules
- **[`Claude.global.md`](./Claude.global.md)** - Universal rules that apply across all programming languages and projects
  - Core principles (minimal changes, verify before completing)
  - File operations and code quality guidelines
  - Security and git workflow patterns
  - When to use (and not use) specific tools

### Language-Specific Templates

#### Frontend
- **[`Claude.frontend.md`](./Claude.frontend.md)** - TypeScript, JavaScript, Node.js, and React
  - Package manager detection (npm, yarn, pnpm, bun)
  - TypeScript configuration and patterns
  - React component structure and hooks
  - Testing (Jest, Vitest) and linting (ESLint, Prettier, Biome)
  - Framework-specific guidance (Next.js, Vite)

#### Python
- **[`Claude.python.md`](./Claude.python.md)** - Python development with UV
  - UV for fast package management and virtual environments
  - Type checking with mypy
  - Modern tooling (ruff, black, pytest)
  - Framework support (Django, Flask, FastAPI)
  - Data science workflow considerations

#### Ruby
- **[`Claude.ruby.md`](./Claude.ruby.md)** - Ruby development
  - Version managers (rbenv, rvm, asdf)
  - Bundler workflows
  - Testing with RSpec and Minitest
  - Linting with RuboCop
  - Rails and Sinatra patterns

#### Rust
- **[`Claude.rust.md`](./Claude.rust.md)** - Rust development
  - Cargo commands for building, testing, and dependency management
  - Clippy (linter) and rustfmt
  - Ownership, borrowing, and error handling patterns
  - Common crates (tokio, serde, thiserror, anyhow)
  - Performance and profiling tips

## How to Use These Templates

### 1. Choose Your Base Templates

Start with `Claude.global.md` as your foundation, then add language-specific templates as needed.

### 2. Copy to Your Project

```bash
# Global rules for all projects
cp Claude.global.md ~/.claude/CLAUDE.md

# Language-specific rules
cp Claude.frontend.md /path/to/project/.claude/CLAUDE.md
cp Claude.python.md /path/to/project/.claude/CLAUDE.md
```

### 3. Customize for Your Project

Edit the copied files to include:
- Your project-specific commands
- Build/test workflows
- Architecture documentation references
- Team conventions

### 4. Progressive Disclosure for Complex Projects

For larger projects, create additional documentation files:

```bash
project/
├── .claude/
│   ├── CLAUDE.md              # Main entry point (concise!)
│   └── docs/
│       ├── architecture.md    # System design docs
│       ├── testing.md         # Test strategies
│       └── deployment.md      # Deploy workflows
```

Then reference these in your main CLAUDE.md:
```markdown
## Additional Documentation

Before starting complex tasks, review:
- `.claude/docs/architecture.md` - System architecture and design patterns
- `.claude/docs/testing.md` - Testing strategies and guidelines
- `.claude/docs/deployment.md` - Deployment and CI/CD workflows
```

## Key Principles

### 1. Less is More

Keep CLAUDE.md files concise. Research shows that:
- Frontier LLMs can follow ~150-200 instructions consistently
- Instruction-following quality decreases as instruction count increases
- Shorter files (<300 lines) perform better

### 2. Universal Applicability

Only include instructions that apply to most tasks. For example:
- ✅ "Always run typecheck before committing"
- ❌ "How to structure database migrations" (only relevant sometimes)

### 3. Progressive Disclosure

Use pointers to additional information rather than duplicating content:
- ✅ "See `docs/architecture.md:50-100` for service communication patterns"
- ❌ [Copying entire architecture section into CLAUDE.md]

### 4. No Style Guidelines

Don't use Claude Code as a linter. Use dedicated tools instead:
- TypeScript/JavaScript: ESLint, Prettier, Biome
- Python: ruff, black
- Ruby: RuboCop, Standard
- Rust: rustfmt, clippy

## Claude Code Placement

CLAUDE.md files can be placed in several locations:

- **Project root** (`/path/to/project/CLAUDE.md`) - Most common, shared with team
- **Parent directories** - Automatically pulled in when working in subdirectories
- **Home directory** (`~/.claude/CLAUDE.md`) - Applies to all sessions
- **Child directories** - Pulled in on-demand when working in those directories

## Best Practices from the Community

### Effective Workflows

1. **Explore, Plan, Code, Commit** - Research and plan before implementing
2. **Write Tests, Commit; Code, Iterate, Commit** - TDD with Claude Code
3. **Multi-Claude Workflows** - Use multiple Claude instances for code review

### Optimization Tips

- **Be specific** in your instructions for better results
- **Provide images** for UI/UX work (mocks, screenshots)
- **Use tab-completion** to reference files quickly
- **Course correct early** - interrupt and redirect as needed
- **Use `/clear`** frequently to reset context between tasks

### Git and GitHub Integration

Claude Code can handle 90%+ of git interactions:
- Writing commit messages
- Handling complex operations (rebase, cherry-pick)
- Creating pull requests
- Fixing failing builds

For full details, see [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices).

## Contributing

Have improvements or additional language templates? Contributions welcome!

Guidelines:
- Follow the "less is more" principle
- Keep files concise and universally applicable
- Use progressive disclosure for detailed information
- Reference external docs rather than duplicating content

## Resources

- **[Claude Code Documentation](https://claude.ai/code)** - Official docs
- **[Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)** - Theory and principles
- **[Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)** - Workflow patterns and tips

## License

These templates are provided as-is for use with Claude Code. Feel free to modify and distribute for your projects.
