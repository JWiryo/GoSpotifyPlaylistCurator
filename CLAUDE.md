# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

Behavioral guidelines to reduce common LLM coding mistakes. These bias toward caution over speed — for trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

## Project: Current state

This is a freshly scaffolded GoLand project. `main.go` still contains the default IDE-generated boilerplate (a "Hello gopher" stub with `//TIP` comments), and there are no dependencies in `go.mod` yet. None of the intended Spotify playlist-curation functionality exists — treat the module name `go-spotify-playlist-curator` and this filename as the only signal of intent.

When building out features, the first real work will be replacing the boilerplate in `main.go` and adding dependencies (e.g. a Spotify Web API client and an OAuth flow) to `go.mod`.

## Project: Commands

- Run: `go run .`
- Build: `go build -o bin/curator .`
- Test all: `go test ./...`
- Test a single package verbosely: `go test -v ./path/to/pkg`
- Run one test: `go test -run TestName ./path/to/pkg`
- Format / vet before committing: `go fmt ./... && go vet ./...`

## Project: Notes

- Go version is pinned to `1.26` in `go.mod` — modern Go syntax (range-over-func, generics, `min`/`max`/`clear` builtins, etc.) is available.
- This is not yet a git repository; `git init` before making commits.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.
