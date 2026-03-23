---
description: 'Guidelines to use rtk, to reduce tokens when using CLI tools'
applyTo: '**'
---

# Copilot Instructions for rtk

**rtk (Rust Token Killer)** is a CLI proxy that filters and compresses command outputs before they reach an LLM context, saving 60–90% of tokens. It wraps common tools (`git`, `cargo`, `grep`, `pnpm`, `go`, etc.) and outputs condensed summaries instead of raw output.

## Using rtk in this session

**Always prefix commands with `rtk` when running shell commands** — this is the entire point of the project and reduces token consumption for every operation you perform.

```bash
# Instead of:              Use:
git status                 rtk git status
git log -10                rtk git log -10
cargo test                 rtk cargo test
cargo clippy --all-targets rtk cargo clippy --all-targets
grep -r "pattern" src/     rtk grep -r "pattern" src/
```

**rtk meta-commands** (always use these directly, no prefix needed):
```bash
rtk gain              # Show token savings analytics for this session
rtk gain --history    # Full command history with per-command savings
rtk discover          # Scan session history for missed rtk opportunities
rtk proxy <cmd>       # Run a command raw (no filtering) but still track it
```

**Verify rtk is installed before starting:**
```bash
rtk --version   # Should print: rtk X.Y.Z
rtk gain        # Should show a dashboard (not "command not found")
```

> ⚠️ **Name collision**: `rtk gain` failing means you have `reachingforthejack/rtk` (Rust Type Kit) installed instead of this project. Run `which rtk` and check the binary source.

