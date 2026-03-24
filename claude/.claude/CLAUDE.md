# Development Guidelines for Claude

> **About this file (v3.1.0):** Language agnostic workflow directives pointing to specific skills depending on the language.
>
> **Architecture:**
> - **CLAUDE.md** (this file): Core philosophy + quick reference (~100 lines, always loaded)
> - **Skills**: Detailed patterns loaded on-demand (backend-python, expectations, front-end-testing, functional, mutation-testing, planning, react-testing, refactoring, tdd, test-design-reviewer, typescript-strict, typescript-testing)
> - **Agents**: Specialized subprocesses for verification and analysis
>
> **Previous versions:**
> - v3.0.0): Lean version optimized for context efficiency. Core principles here; detailed patterns loaded on-demand via skills.
> - v2.0.0: Modular with @docs/ imports (~3000+ lines always loaded)
> - v1.0.0: Single monolithic file (1,818 lines)

## Core Philosophy

**TEST-DRIVEN DEVELOPMENT IS NON-NEGOTIABLE.** Every single line of production code must be written in response to a failing test. No exceptions. This is not a suggestion or a preference - it is the fundamental practice that enables all other principles in this document.

I follow Test-Driven Development (TDD) with a strong emphasis on behavior-driven testing and functional programming principles. All work should be done in small, incremental changes that maintain a working state throughout development.

## Quick Reference

**Key Principles:**

- Write tests first (TDD)
- Test behavior, not implementation
- Immutable data only
- Small, pure functions
- Use typing systems when available
- Use real schemas/types in tests, never redefine them

**Preferred Tools:**

When writing or analysing code, depending on the language load the appropriate skill for that language as referred in the following list.

- **Language**: 
    - Python: 
      - Backend: When writting backend Pythond, load the `backend-python` skill.
    - TypeScript (strict mode): load the `typescript-strict` skill.
- **State Management**: Prefer immutable patterns
- **Search**: For syntax-aware or structural matching searches, default to `ast-grep --lang rust -p '<pattern>'` command (or set --lang appropriately) and avoid falling back to text-only tools like rg or grep unless I explicitly request a plain-text search.

## Testing Principles

**Core principle**: Test behavior, not implementation. 100% coverage through business behavior.

**Quick reference:**
- Write tests first (TDD non-negotiable)
- Test through public API exclusively
- Use factory functions for test data
- Tests must document expected business behavior
- No 1:1 mapping between test files and implementation files

For detailed testing patterns and examples, load the `testing` skill.
For verifying test effectiveness through mutation analysis, load the `mutation-testing` skill.

## Code Style

**Core principle**: Functional programming with immutable data. Self-documenting code.

**Quick reference:**
- No data mutation - immutable data structures only
- Pure functions wherever possible
- No nested if/else - use early returns or composition
- No comments - code should be self-documenting
- Prefer options objects over positional parameters
- Use array methods (`map`, `filter`, `reduce`) over loops

For detailed patterns and examples, load the `functional` skill.

## Development Workflow

**Core principle**: RED-GREEN-REFACTOR in small, known-good increments. TDD is the fundamental practice.

**Quick reference:**
- RED: Write failing test first (NO production code without failing test)
- GREEN: Write MINIMUM code to pass test
- REFACTOR: Assess improvement opportunities (only refactor if adds value)
- **Wait for commit approval** before every commit
- Each increment leaves codebase in working state
- Capture learnings as they occur, merge at end

For detailed TDD workflow, load the `tdd` skill.
For refactoring methodology, load the `refactoring` skill.
For significant work, load the `planning` skill for three-document model (PLAN.md, WIP.md, LEARNINGS.md).

## Working with Claude

**Core principle**: Think deeply, follow TDD strictly, capture learnings while context is fresh.

**Quick reference:**
- ALWAYS FOLLOW TDD - no production code without failing test
- Assess refactoring after every green (but only if adds value)
- Update CLAUDE.md when introducing meaningful changes
- Ask "What do I wish I'd known at the start?" after significant changes
- Document gotchas, patterns, decisions, edge cases while context is fresh

For detailed TDD workflow, load the `tdd` skill.
For refactoring methodology, load the `refactoring` skill.
For detailed guidance on expectations and documentation, load the `expectations` skill.

## Resources and References

- [Testing Library Principles](https://testing-library.com/docs/guiding-principles)
- [Kent C. Dodds Testing JavaScript](https://testingjavascript.com/)
- [Functional Programming in TypeScript](https://gcanti.github.io/fp-ts/)

## Summary

The key is to write clean, testable, functional code that evolves through small, safe increments. Every change should be driven by a test that describes the desired behavior, and the implementation should be the simplest thing that makes that test pass. When in doubt, favor simplicity and readability over cleverness.
