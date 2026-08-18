# Changelog

All notable changes to this project are documented here.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Added
- Initial scaffold: Rust binary crate, `rand` dependency, pinned toolchain.
- MIT license.
- Tracked setup plan in `PLAN.md`.
- Git hooks: `.githooks/pre-commit` (fmt + clippy + test) and
  `.githooks/pre-push` (block direct pushes to `main`).
- GitHub Actions CI workflow (`.github/workflows/ci.yml`).
- Claude Code project settings and `/checks` slash command.
- Documentation: `README.md`, `CLAUDE.md`, `NOTES.md`.
