# guessing-game

A tiny Rust CLI guessing game — built as a sandbox for learning Claude Code
workflow on a growing project. The game picks a random number in `0..=99`,
you guess, it tells you `higher`, `lower`, or `correct`, and it loops until
you get it.

## Quick start

Requires Rust (install via [rustup.rs](https://rustup.rs)). Then:

```bash
cargo run
```

## How to play

Type a whole number between 0 and 99, press Enter. Repeat until the game
prints `correct`.

## Development

- Conventions and commands: see [CLAUDE.md](./CLAUDE.md).
- Live setup checklist: see [PLAN.md](./PLAN.md).
- Session-by-session learnings: see [NOTES.md](./NOTES.md).
- Change history: see [CHANGELOG.md](./CHANGELOG.md).

## License

MIT — see [LICENSE](./LICENSE).
