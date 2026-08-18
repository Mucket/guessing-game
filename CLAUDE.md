# CLAUDE.md

Conventions and commands for Claude Code (and human contributors) working on
this repo. This is the file Claude reads first — keep it terse and truthful.

## Purpose

A Rust CLI guessing game. The **primary** goal is learning Claude Code
workflow on a growing project; the game is a vehicle.

## Build / test / run

```bash
cargo run                              # play the game
cargo test                             # run all tests
cargo fmt                              # format (auto-runs on Claude edits)
cargo fmt --check                      # verify formatting
cargo clippy --all-targets -- -D warnings   # lint (warnings fail)
```

The `/checks` slash command runs fmt-check + clippy + test in one shot.

## Layout

- `src/main.rs` — binary crate; game logic + inline `#[cfg(test)] mod tests`.
- `.githooks/` — git hooks (`pre-commit`, `pre-push`). Wired via
  `git config core.hooksPath .githooks`; already set for this clone.
- `.github/workflows/ci.yml` — CI mirror of the local gate.
- `.claude/settings.json` — project-scoped Claude Code config (permissions,
  PostToolUse auto-`cargo fmt` on `.rs` edits).
- `.claude/commands/` — slash commands.
- `PLAN.md` — live setup checklist.
- `NOTES.md` — the human's learning log; **don't edit unless asked**.

## Workflow rules

- **Never commit directly to `main`.** Branch → PR → merge. Use
  `gh pr create --fill` and `gh pr merge --squash --delete-branch`.
- The local `pre-push` hook and GitHub branch protection both block direct
  pushes to `main`. Don't bypass them with `--no-verify` — fix the underlying
  problem instead.
- Pre-commit runs fmt-check + clippy + test. Failing hook = failing commit;
  fix and re-commit rather than skipping.
- Any PR that changes behavior adds a bullet under `## [Unreleased]` in
  `CHANGELOG.md`.

## Style

- Return `Result` at boundaries; `unwrap` is acceptable in tests and in
  narrow, provably-safe internal paths only.
- No comments explaining *what* well-named code already says. Comments earn
  their place when they explain *why* (a non-obvious invariant, a workaround).
- Structure code for testability: `main()` should be thin glue; the logic
  lives in functions that take injected reader / writer / RNG so tests can
  drive them deterministically.
