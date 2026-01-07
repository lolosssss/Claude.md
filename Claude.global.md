# Global Claude Code Instructions

This file contains universal rules for Claude Code that apply across all programming languages and projects.

## Core Principles

- **Less is more**: Keep changes minimal and focused. Don't refactor or add features beyond what's requested.
- **Read before writing**: Always read existing files before modifying them to understand context and patterns.
- **Verify before completing**: Run tests, type checks, or build commands to ensure changes work correctly.
- **Be explicit**: Ask for clarification when requirements are ambiguous instead of making assumptions.

## File Operations

- **Use specialized tools**: Use Read (not cat), Edit (not sed), and Write tools for file operations
- **Edit existing files**: Prefer editing existing files over creating new ones unless explicitly necessary
- **Preserve formatting**: Maintain existing indentation, line endings, and code structure when editing
- **No redundant files**: Never create documentation files unless explicitly requested

## Code Quality

- **Avoid over-engineering**: Build the simplest solution that meets requirements
- **No premature abstractions**: Don't create utilities or helpers for one-time operations
- **Trust existing code**: Don't add validation for scenarios that can't happen
- **Use linters**: Rely on dedicated linting/formatting tools rather than manual style enforcement

## Workflow

- **Plan first, code second**: For complex tasks, create a plan before implementing
- **Ask questions**: Use AskUserQuestion tool when you need clarification or preferences
- **Track progress**: Use TodoWrite for tasks with 3+ steps or multi-step work
- **Run tests in parallel**: Execute independent commands in parallel when possible

## Security

- **Prevent vulnerabilities**: Avoid XSS, SQL injection, command injection, and OWASP Top 10 issues
- **Validate inputs**: Check user inputs and external API responses at system boundaries
- **Fix issues immediately**: If you write insecure code, correct it right away

## Git Workflow

- **Commit only when asked**: Never create commits unless explicitly requested
- **Write meaningful messages**: Focus on "why" rather than "what" when committing
- **Never force push**: Warn user if requested to force push to main/master
- **Skip hooks carefully**: Only use --no-verify if user explicitly requests it

## When NOT to use tools

- **Don't use Task tool**: For direct file reads or specific file searches (use Read/Glob instead)
- **Don't use Bash**: For file operations like cat, grep, find, sed, awk, echo (use specialized tools)
- **Don't use Bash for searches**: Use Grep (not grep/rg) for searching code
- **Don't create todos**: For single straightforward tasks (<3 steps)

## Progressive Disclosure

For project-specific or language-specific instructions, refer to separate documentation files rather than cluttering this global configuration. Language-specific patterns, testing frameworks, and build tools should be documented in project-level CLAUDE.md files.
