# PLAN

Live tracking of the workflow-setup plan for the guessing-game project.
Source of truth: `/Users/colinmcrae/.claude/plans/in-this-project-i-rosy-eich.md`.

Legend:
- `- [ ]` — todo
- `- [x]` — done
- `- [~]` — skipped/deferred (with a reason)
- **(Claude)** — Claude Code executes
- **(You)** — you execute (interactive / shared state)
- **(Both)** — Claude drafts, you review, Claude commits

---

## 1. Prerequisites

- [x] **(You)** Install Rust via `rustup` — `rustc 1.97.1`
- [x] **(You)** Install `gh` — `gh 2.97.0`
- [x] **(You)** Authenticate: `gh auth login` — logged in as `Mucket`

## 2. Scaffold the Rust project

- [x] **(Claude)** `cargo new guessing-game --bin` and move contents to repo root
- [x] **(Claude)** `cargo run` prints "Hello, world!"
- [x] **(Claude)** Add `rand = "0.8"` to `Cargo.toml`
- [x] **(Claude)** Create `rust-toolchain.toml` (stable, with rustfmt + clippy)

## 3. Initialize git — locally, then GitHub

- [ ] **(Claude)** `git init -b main`
- [ ] **(Claude)** Write `.gitignore` (`/target`, `**/*.rs.bk`, `.DS_Store`, `.claude/settings.local.json`)
- [ ] **(Claude)** Create `LICENSE` (MIT)
- [ ] **(Claude)** First commit: `Initial scaffold`
- [ ] **(You)** `gh repo create guessing-game --private --source=. --push`

## 4. Enforce "no direct push to main" — two layers

- [ ] **(You)** Apply GitHub branch protection via `gh api` (enforce_admins=true)
- [ ] **(Claude)** Write `.githooks/pre-push` that blocks `refs/heads/main`
- [ ] **(Claude)** `git config core.hooksPath .githooks` + `chmod +x`

## 5. Local pre-commit gate

- [ ] **(Claude)** Write `.githooks/pre-commit` (fmt --check, clippy -D warnings, test --quiet)
- [ ] **(Claude)** `chmod +x .githooks/pre-commit`

## 5b. GitHub Actions CI

- [ ] **(Claude)** Write `.github/workflows/ci.yml` (fmt, clippy, test on PR + push to main)
- [ ] **(You)** After CI runs green on the first PR, re-apply branch protection to require the `check` status check

## 6. Claude Code configuration

- [ ] **(Claude)** Write `.claude/settings.json` (permissions + PostToolUse `cargo fmt` on `*.rs`)
- [ ] **(Claude)** Write `.claude/commands/checks.md` (the `/checks` slash command)

## 6b. README.md

- [ ] **(Both)** Draft `README.md` (~15–25 lines; what/quick-start/how-to-play/dev pointer/license)

## 6c. CHANGELOG.md

- [ ] **(Claude)** Initialize `CHANGELOG.md` (Keep-a-Changelog format, `[Unreleased]` section)

## 6d. NOTES.md — learning log

- [ ] **(You)** Own the content; Claude only edits when explicitly asked
- [ ] **(Claude)** Scaffold the empty structure

## 7. CLAUDE.md

- [ ] **(Both)** Draft v1 CLAUDE.md (~30 lines; purpose, build/test/run, layout, workflow, style)

## 8. The game

- [ ] **(Claude)** `enum Comparison { Higher, Lower, Correct }`
- [ ] **(Claude)** `fn compare(guess: u8, secret: u8) -> Comparison`
- [ ] **(Claude)** `fn play<R: BufRead, W: Write, F: FnMut() -> u8>(...)`
- [ ] **(Claude)** `main()` wires stdin/stdout/`rand::thread_rng()` into `play`

## 9. Unit tests

- [ ] **(Claude)** `compare_returns_correct_on_equal`
- [ ] **(Claude)** `compare_returns_higher_when_guess_below_secret`
- [ ] **(Claude)** `compare_returns_lower_when_guess_above_secret`
- [ ] **(Claude)** `play_terminates_on_correct_guess`
- [ ] **(Claude)** `play_reports_higher_then_correct`

## 10. First-feature PR walk-through

- [ ] **(Claude)** `git switch -c feat/comparison-logic`
- [ ] **(Claude)** Implement `compare` + tests
- [ ] **(Claude)** `git commit` (pre-commit hook runs)
- [ ] **(You)** `git push -u origin feat/comparison-logic`
- [ ] **(You)** `gh pr create --fill`
- [ ] **(You)** `gh pr merge --squash --delete-branch`
- [ ] **(Claude)** `git switch main && git pull`

## Verification (final)

- [ ] `cargo run` plays the game end-to-end
- [ ] `cargo test` — all pass
- [ ] `cargo fmt --check` — clean
- [ ] `cargo clippy --all-targets -- -D warnings` — clean
- [ ] Pre-commit hook rejects a fmt-violating commit
- [ ] Local pre-push hook rejects direct push to `main`
- [ ] Branch protection rejects `--no-verify`-bypassed push
- [ ] PR flow: create → merge → pull produces the merged commit
- [ ] Editing a `.rs` file via Claude Code triggers auto-`cargo fmt` (PostToolUse hook)
- [ ] CLAUDE.md is legible cold in under a minute
