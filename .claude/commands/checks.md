---
description: Run cargo fmt --check, clippy -D warnings, and cargo test; report what passed and what failed
---

Run the three local checks in order and report the results concisely:

1. `cargo fmt --check` — formatting.
2. `cargo clippy --all-targets -- -D warnings` — lint (warnings fail).
3. `cargo test --quiet` — tests.

If everything passes, say so in one line. If anything fails, show only the
relevant failure output (not the whole build log) and stop after the first
failing step — no need to run the later ones once fmt fails.
