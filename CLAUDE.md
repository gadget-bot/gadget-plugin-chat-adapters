# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`gadget-plugin-chat-adapters` provides bot-agnostic command and event adapter interfaces so Gadget plugins can integrate with arbitrary chat bots and platforms. It operates standalone as adapter contracts and runtime routing. Consumer plugins can integrate through this adapter layer but must not require it.

This plugin is part of the [Gadget](https://github.com/gadget-bot/gadget/) ecosystem — a Go Slack bot framework built on the Slack Events API.

See `docs/specs/gadget-plugin-chat-adapters.md` for full v1 requirements.

## Build & Development Commands

```bash
make build        # Compile binary to dist/
make test         # Run tests with coverage
make lint         # Run golangci-lint (also runs fmt check)
make fmt          # Check formatting with golangci-lint (diff only)
make all          # clean → verify → lint → test → build
make tools        # Install golangci-lint
```

Run a single test:
```bash
go test -v -run TestFunctionName ./pkg/...
```

**Always prefer `make` targets over calling `go` commands directly.** Only fall back to raw `go` commands when no suitable make target exists (e.g., running a single test).

Run `go build ./...` and `go test ./...` after any code changes before committing.

## Architecture

<!-- TODO: document key packages, entry points, and data flow as the plugin grows. -->

## Testing

Tests use Go's table-driven testing pattern. Always use interfaces and dependency injection so handlers accept mock clients rather than creating their own. Never instantiate real API clients inside handlers.

## Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`

**Breaking changes:** append `!` after type/scope, or add `BREAKING CHANGE:` in the footer.

## Branching

- `main` — production releases only; NEVER commit directly to main
- Always create a feature branch and open a PR for all changes

## GitHub Repository

The origin repository is `gadget-bot/gadget-plugin-chat-adapters`. Always use this owner/repo when querying GitHub for issues, pull requests, or other repository details.

## GitHub Issues

When opening issues:
- Always apply an issue type and the best-fitting label
- Scan existing issues to identify relationships (sub-issues, duplicates, related issues)
- Ask before changing existing relationships
