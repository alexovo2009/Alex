# AGENTS.md

This document provides coding-agent guidelines intended for automated agents operating within this repository. It covers build, lint, test workflows, code style conventions, and policy for dealing with Cursor and Copilot rules if present.

## Table of contents
- [Overview](#overview)
- [Scope & Audience](#scope--audience)
- [General Principles](#general-principles)
- [Build, Lint, Test](#build-lint-test)
- [Running a Single Test](#running-a-single-test)
- [Code Style Guidelines](#code-style-guidelines)
- [Imports & Formatting](#imports--formatting)
- [Types, Naming & Errors](#types-naming--errors)
- [Documentation & Comments](#documentation--comments)
- [Structure & Modularity](#structure--modularity)
- [Testing Policy](#testing-policy)
- [Security & Observability](#security--observability)
- [CI, Hooks & Validation](#ci-hooks--validation)
- [Cursor Rules](#cursor-rules)
- [Copilot Rules](#copilot-rules)
- [Appendix](#appendix)

## Overview
- This AGENTS.md describes how code is built, linted, and tested in this repository.
- It also codifies preferred code style, naming, error handling, and test strategies so agents can operate with minimal ambiguity.
- It is intended for humans and automation alike; when necessary, modify or extend to align with project evolution.

## Scope & Audience
- Audience: automated agents (CI/CD tasks, code synthesis bots, formatters, linters) and maintainers.
- Applies to all languages present in the workspace; follow language-specific tooling where defined by scripts.
- Prefer idempotent operations; minimize side effects outside the repo workspace.

## General Principles
- Be explicit about intent; prefer failing fast with clear messages.
- Respect repository conventions and existing tooling; extend rather than replace when possible.
- Do not modify unrelated files; isolate changes to the scope of the current task.
- Use the repository's existing test coverage as a guardrail; avoid introducing flaky tests.
- When in doubt, defer to human maintainers for policy decisions on ambiguous items.

## Build, Lint, Test
- Use the repository's standard scripts when available. If not, prefer language-typical commands described below.
- Always run in a deterministic, non-interactive manner. Capture and report exit codes and stdout/stderr.
- Prefer running tests with a single-target scope when debugging; use filtering options to limit to a subset.

### Build
- Node/JavaScript/TypeScript (when a build step exists):
  - `npm run build` or `yarn build` (respect project script order in `package.json`).
- Python: no built binary; ensure dependencies installed and run: `python -m build` if project ships wheels, otherwise skip.
- Go: `go build ./...` to compile all modules.
- Rust: `cargo build`.
- Java: `mvn -q -DskipTests package` or `gradle build` depending on project.
- C#: `dotnet build`.
- If multiple languages exist, run per-language build commands in sequence, capturing per-language logs.

### Lint
- Node/TS: `npm run lint` (or `yarn lint`). Enforce Prettier/ESLint rules configured in repo.
- Python: `ruff check --exit-non-zero --no-cache .` and/or `flake8` where applicable; prefer `ruff` where configured.
- Go: `golangci-lint run` or `go vet ./...`.
- Rust: rely on `cargo fmt -- --check` and `cargo clippy` when configured.
- Java: `mvn -DskipTests verify` or `gradle lint` where defined.
- C#: `dotnet format` and static analyzers as configured in project.
- Ensure linters are run on changed files only where practical, or the whole project if needed for consistency.

### Test
- Node/TS: `npm test` or `yarn test`. Prefer `npm test -- --watchAll=false` to ensure deterministic runs.
- Python: `pytest -q` with `-k` for filtering by name when needed; ensure coverage if configured.
- Go: `go test ./...` including coverage if configured; for specific tests use `-run`.
- Rust: `cargo test` with `-- --nocapture` for verbose output if needed.
- Java: `mvn -Dtest=*TestName* test` for targeted tests or `mvn test` for full suite.
- C#: `dotnet test` with `--filter FullyQualifiedName~TestName` to run a single test.

> Note: If a repo uses language-specific test runners, prefer invoking their standard CLI to preserve environment and flags.

## Running a Single Test
- Goal: deterministically execute only a named test case or class to expedite debugging.
- Node/JS (Jest):
  - `npm test -- -t "test name"` (matches full test name). For vitest: `vite test --testNamePattern="name"`.
- Python (pytest):
  - `pytest -k "name"` or `pytest -q test_module.py::TestClass::test_name`.
- Go: `go test ./... -run ^TestName$` (regex on test function name).
- Rust: `cargo test TestName`.
- Java: `mvn -Dtest=TestName test`.
- C#: `dotnet test --filter FullyQualifiedName~TestName`.

## Code Style Guidelines
- The repo values consistency and readability; implement these as baseline rules.
- When in doubt, align to the most widely adopted standard among the repo's languages.

### Imports & Formatting
- Keep imports grouped: standard library first, then third-party, then local modules.
- Separate groups with blank lines; avoid unused imports.
- Use explicit type imports where supported; prefer named imports to default imports if they reduce ambiguity.
- Format code with project tooling (see Build/Lint). Ensure formatting passes on CI.
- Prefer tree-shaking-friendly imports in modular setups.

### Formatting Best Practices by Language
- Node/TS: use Prettier for style, ESLint for rules; add `prettier --check` in lint script; auto-fix where safe.
- Python: use Black for formatting; isort for import order; mypy for type checks.
- Go: `gofmt`/`goimports` for formatting; `golangci-lint` integrates lint rules.
- Rust: `rustfmt` for formatting; `clippy` for linting.
- Java: rely on the project's formatter (Google Java Format) or IDE tooling; run `mvn fmt:format` if configured.
- C#: `dotnet format` for formatting; analyzers enforce rules.

### Types, Naming & Errors
- Use explicit types where possible; avoid `any` or dynamic typing in typed languages.
- Naming conventions:
  - camelCase for variables and functions.
  - PascalCase for types, classes, interfaces.
  - UPPER_SNAKE for constants where appropriate.
- Return types should be explicit; avoid `void` surprises in public APIs unless clearly documented.
- Error handling:
  - Propagate meaningful errors with context; wrap errors where supported (e.g., `%w` in Go, `cause` in Java, `from` in Rust).
  - Do not swallow errors silently; log or surface as user-facing messages when appropriate.
- API surfaces should be documented; avoid leaking internals through public interfaces.

### Documentation & Comments
- Write doc comments for exported functions, classes, interfaces.
- Use inline comments sparingly; prefer self-documenting code with descriptive names.
- For tests and public helpers, document intent and edge cases.

### Testing & Coverage
- Tests should be deterministic and hermetic.
- Name tests clearly: include the function or feature under test and a short scenario.
- Prefer small, focused tests; limit test dependencies and external I/O.
- Collect and report coverage where configured; fail CI if coverage drops.

### Security & Observability
- Do not log secrets or credentials; use secrets management or environment variables.
- Validate inputs and sanitize outputs; guard against injection risks.
- Instrument with structured logs; include request IDs or correlation IDs when available.
- Use feature flags and config to guard experimental paths in tests.

### Performance & Reliability
- Favor non-blocking operations and asynchronous I/O where appropriate.
- Use caching and memoization carefully; validate cache invalidation strategies.
- Write performance-oriented tests where applicable and document expectations.

### Code Review & Quality
- PRs should be small, focused, and reviewable within a sane timeframe.
- Include rationale in commit messages; keep message scope narrow and actionable.
- Respect contributor guidelines and test for accessibility and localization basics where relevant.

## CI, Hooks & Validation
- Pre-commit hooks should run locally and on CI; formatting checks should fail fast if not passing.
- Ensure tests pass in a clean environment; depend on lockfiles to ensure reproducibility.
- CI should report: build success, lint status, test results, and coverage.
- If a change touches multiple languages, tests may need to run in multiple environments.

## Cursor Rules
- Not currently present in repository (no `.cursor/rules/` or `.cursorrules` found).
- Default expectations (when added):
  - Agents should not alter semantics while applying cursor-driven edits.
  - Preserve line endings and indentation to minimize diffs.
  - Validate edits by running the corresponding build/test steps.

## Copilot Rules
- Not currently present (no `.github/copilot-instructions.md` found).
- If added, Copilot rules should be visible to agents; prefer following explicit guidance and avoiding large auto-generated edits that break style.

## Appendix
- Quick start for new contributors:
  - Run `npm run build` / `npm run lint` / `npm test` as available.
  - If you need to test a single unit, use the framework-specific single-test commands described above.
  - Read existing AGENTS.md for language-specific quirks and repository conventions.
- For questions or edge cases, reach out to the repo maintainers or file an issue.
