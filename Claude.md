# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a documentation repository containing reference materials and best practices for creating and managing CLAUDE.md files for use with Claude Code (Anthropic's agentic coding CLI tool).

## Repository Structure

```
/
├── README.md                      # Project overview and usage guide
├── CLAUDE.md                      # Repository-specific CLAUDE.md (this file)
├── Claude.global.md               # Universal rules for all languages
├── Claude.frontend.md             # TypeScript/JavaScript/React/Node.js
├── Claude.python.md               # Python with UV package manager
├── Claude.ruby.md                 # Ruby (Rails, Sinatra, etc.)
├── Claude.rust.md                 # Rust (Cargo, async, etc.)
└── refers/                        # Reference documentation
    ├── write-a-good-claude-md.md  # Guide on writing effective CLAUDE.md
    └── claude-code-best-practices.md  # Best practices for agentic coding
```

## Key Concepts

### CLAUDE.md Purpose
CLAUDE.md files are used to onboard Claude Code into codebases by documenting:
- **WHAT**: Tech stack, project structure, codebase organization
- **WHY**: Project purpose and functionality of different parts
- **HOW**: Development workflow, build/test commands, verification methods

### Progressive Disclosure Pattern
For complex projects, use separate markdown files for task-specific instructions rather than cluttering the root CLAUDE.md. Example structure:
```
agent_docs/
  ├── building_the_project.md
  ├── running_tests.md
  ├── code_conventions.md
  └── service_architecture.md
```

Then reference these files in CLAUDE.md with brief descriptions, instructing Claude to read relevant files as needed.

### Key Principles
1. **Less is more**: Keep CLAUDE.md concise (<300 lines recommended)
2. **Universal applicability**: Only include instructions that apply to most tasks
3. **Avoid code style guidelines**: Use linters and formatters instead
4. **Pointer over copy**: Reference files with `file:line` rather than duplicating content

## Working with This Repository

When working with files in this repository:
- **Use templates** - The `Claude.*.md` files are ready-to-use templates for different languages
- **Reference materials** are in the `refers/` directory (theoretical background)
- **README.md** contains usage instructions and links to blog posts
- All CLAUDE.md files follow progressive disclosure and "less is more" principles

## When Adding or Modifying Templates

1. **Keep it concise** - Aim for <300 lines per file
2. **Universal applicability** - Only include rules that apply to most tasks in that language
3. **Progressive disclosure** - Reference external docs rather than duplicating content
4. **No style guidelines** - Use linters/formatters instead (ruff, eslint, rubocop, etc.)
5. **Pointer over copy** - Use `file:line` references to point to authoritative context
6. **Focus on HOW** - Commands, workflows, and verification methods
