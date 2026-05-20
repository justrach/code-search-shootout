# code-search-shootout

Reproducible benchmark comparing four code-search backends on a real-world
JS/TS corpus (facebook/react). Measures cold-build time, on-disk size, warm
query latency, and agentic task completion (how many tokens + tool calls
an LLM agent burns finishing a real exploration task on each backend).

The headline (full writeup in [RESULTS.md](RESULTS.md)):

- **codedb** beats lean-ctx by **10-1400x per query**, MCP-vs-MCP.
- At the **pure engine level codedb is 5-200x faster** than SQLite FTS5 trigram on word-index lookups.
- All three backends solve the same agent tasks; codedb and fts5 do it with ~20% fewer tokens and ~70% less wall time than lean-ctx.
- Adding `--paths-only` compression to codedb's CLI and asking agents to use it made codedb **32% more tokens, 70% slower** — a self-experiment that proves the "compression-first design hurts agents" thesis on a controlled tool.
- Removing in-line cloud-sync telemetry tightened codedb p99 by **~1,200x average** across 15 queries.

## Backends

| Backend | What it is | Install |
|---|---|---|
| `codedb` | Custom Zig trigram + word index + outline + dep graph, MCP-native | `curl -fsSL https://codedb.codegraff.com/install.sh \| bash` |
| `fts5_trigram` | SQLite FTS5 with `trigram` tokenizer (3.34+) | bundled with sqlite3 |
| `fts5_unicode61` | SQLite FTS5 with default word-boundary tokenizer + BM25 | bundled with sqlite3 |
| `lean-ctx` | yvgude/lean-ctx — Rust BM25 + compression daemon | `cargo install lean-ctx` |

## Reproducing

```bash
# 1. Get the corpus (outside /tmp — codedb refuses to index temp roots)
mkdir -p ~/codedb-bench
git clone --depth 1 https://github.com/facebook/react ~/codedb-bench/react

# 2. Install the backends you want to compare
#   codedb:   curl -fsSL https://codedb.codegraff.com/install.sh | bash
#   lean-ctx: cargo install lean-ctx
#   fts5:     comes with sqlite3 (3.34+)

# 3. Run (3 sessions x 500 iter, median-of-medians, files-list normalize)
python3 shootout.py --corpus ~/codedb-bench/react \
                    --iters 500 --sessions 3 \
                    --normalize-files-list \
                    --clean-codedb \
                    --out results/react-$(date +%Y-%m-%d).md
```

Flags:

- `--iters N` — warm iterations per query (default 500)
- `--sessions N` — multi-session median-of-medians (default 1; use 3 for tight numbers)
- `--normalize-files-list` — pairwise files-set Jaccard across backends
- `--skip-codedb`, `--skip-fts5`, `--skip-leanctx` — limit backends
- `--leanctx-cli` — use `lean-ctx grep` CLI per call (cold spawn) instead of MCP-resident (default is MCP)
- `--clean-codedb` — wipe matching codedb snapshot before indexing

## What it measures

**Build phase:** wall-clock to build the index from scratch + on-disk size.

**Query phase:** for each query in `queries.json`, warm the backend with one call, then time `--iters` calls per session, over `--sessions` sessions. Reports min/p50/p95/p99 latency (median-of-medians across sessions) plus result counts.

**Normalized files-list:** every backend asked the same question — return the SET of files containing the query. Reports pairwise Jaccard similarity. Validates that all backends find substantially the same answers.

> Hit counts in the latency table are NOT directly comparable across backends (codedb caps at 50 display, FTS5 returns files, lean-ctx caps at 20). Use those as recall sanity; the **normalized files-list** is the apples-to-apples recall metric.

## Calibration

- **codedb** runs as an MCP server over stdio (`codedb <root> mcp`). Persistent process; warm queries are pure RPC.
- **FTS5** uses a persistent SQLite connection from Python.
- **lean-ctx** is invoked through its MCP stdio (`lean-ctx`) by default — same fairness as codedb.
- Pass `--leanctx-cli` to use the per-call `lean-ctx grep` CLI instead (which pays ~700 ms Rust binary startup per call); this is the "what a shell pipeline feels" mode.

## Query set

`queries.json` covers a spectrum of code-search workloads on a React corpus:

- common-identifier — high-frequency, lots of result merging (`useState`)
- camelcase-identifier — full identifier (`forwardRef`, `createElement`)
- substring-identifier — substring of bigger names (`Fiber`, `Lane`, `Suspense`)
- rare-camelcase — low-frequency named symbol (`flushPassiveEffects`)
- short-trigram-exact — 3-char query (`set`)
- lang-keyword — high-frequency stress test (`function`)
- negative — should return 0 on all backends (`xyzzy_react_does_not_exist`)

## Agentic eval (separate methodology)

`shootout.py` measures tool-level latency. To measure **agent-level efficiency** (the thing that actually matters when you're paying tokens), we ran Sonnet 4.6 sub-agents on real React-internals exploration tasks, each restricted to one backend's CLI only. Full methodology + results in [RESULTS.md sections 4, 9, 10](RESULTS.md).

## Contributing

PRs welcome — especially:

- New corpora (a `corpora/` directory of curated targets would be great)
- New backends (anything with an MCP server or a CLI can be added to `shootout.py`)
- New agentic tasks
- Results from your own machines (drop a markdown file in `results/`)

## License

MIT.

## Related

- [codedb](https://github.com/justrach/codedb) — the Zig code-intelligence server this benchmark was originally built to evaluate. The bench surfaced two fixes that shipped to codedb: a negative-query Tier 5 short-circuit (113 ms → 0.29 ms) and a telemetry tail-latency fix (in-line cloud sync was causing ~10% of MCP calls to spike to 200-400 ms; moved to a background thread; ~1,200x average p99 improvement).
