# search-shootout — react

**Date:** 2026-05-20 16:55
**Corpus:** `/Users/blackfloofie/codedb-bench/react`
**Indexed files:** 6,619
**Corpus bytes:** 26.5 MB
**Iterations:** 500 warm × 3 sessions (median-of-medians)

## Build phase

| Backend | Cold index time | On-disk size |
|---|---|---|
| fts5_trigram | 1.69s | 93.5 MB |
| fts5_unicode61 | 0.42s | 36.3 MB |
| codedb | 0.05s | 67.4 MB |
| lean-ctx | 8.43s | — |

## Query latency (warm, ms)

> codedb: MCP stdio (one server, many calls).
> fts5_*: persistent SQLite connection.
> lean-ctx: per-call CLI spawn (includes ~700ms binary startup).
> Hit counts are NOT directly comparable across backends — use them as recall sanity (zero vs non-zero).

| query | kind | fts5_tri min | fts5_tri p50 | fts5_tri p95 | fts5_tri p99 | fts5_tri hits | fts5_uni min | fts5_uni p50 | fts5_uni p95 | fts5_uni p99 | fts5_uni hits | codedb min | codedb p50 | codedb p95 | codedb p99 | codedb hits | leanctx min | leanctx p50 | leanctx p95 | leanctx p99 | leanctx hits |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `useState` | common-identifier | 0.78 | 0.82 | 1.20 | 2.16 | 674 | 0.02 | 0.02 | 0.02 | 0.02 | 674 | 1.64 | 4.20 | 245.29 | 362.95 | 50 | 43.40 | 47.87 | 64.54 | 65.82 | 20 |
| `useEffect` | common-identifier | 0.40 | 0.43 | 0.43 | 0.46 | 434 | 0.01 | 0.01 | 0.01 | 0.01 | 426 | 0.92 | 2.40 | 234.79 | 294.76 | 50 | 44.11 | 46.71 | 62.51 | 63.94 | 20 |
| `forwardRef` | camelcase-identifier | 0.17 | 0.19 | 0.19 | 0.20 | 129 | 0.01 | 0.01 | 0.01 | 0.01 | 127 | 0.27 | 1.10 | 258.77 | 367.94 | 50 | 46.01 | 50.61 | 66.85 | 68.51 | 20 |
| `createElement` | camelcase-identifier | 1.01 | 1.04 | 1.08 | 1.13 | 403 | 0.01 | 0.01 | 0.01 | 0.02 | 401 | 0.83 | 2.15 | 255.83 | 362.82 | 50 | 71.84 | 74.88 | 91.24 | 93.55 | 20 |
| `Fiber` | substring-identifier | 0.12 | 0.14 | 0.14 | 0.15 | 303 | 0.01 | 0.01 | 0.01 | 0.01 | 180 | 0.33 | 1.17 | 262.30 | 398.55 | 50 | 112.17 | 118.87 | 142.55 | 164.73 | 20 |
| `Lane` | substring-identifier | 0.05 | 0.06 | 0.06 | 0.07 | 72 | 0.01 | 0.01 | 0.01 | 0.01 | 40 | 0.20 | 0.81 | 263.19 | 335.52 | 50 | 126.60 | 131.52 | 155.83 | 176.86 | 20 |
| `Suspense` | substring-identifier | 0.40 | 0.41 | 0.43 | 0.46 | 314 | 0.01 | 0.01 | 0.01 | 0.01 | 259 | 0.45 | 1.30 | 250.29 | 371.65 | 50 | 46.83 | 49.85 | 66.74 | 70.31 | 20 |
| `flushPassiveEffects` | rare-camelcase | 0.21 | 0.22 | 0.23 | 0.24 | 8 | 0.01 | 0.01 | 0.01 | 0.01 | 7 | 0.09 | 0.48 | 259.55 | 348.79 | 9 | 166.02 | 176.53 | 262.34 | 342.25 | 20 |
| `enableTransitionTracing` | rare-flag | 0.71 | 0.74 | 0.80 | 0.85 | 25 | 0.01 | 0.01 | 0.01 | 0.01 | 25 | 0.21 | 1.05 | 266.76 | 359.64 | 28 | 159.62 | 164.83 | 182.58 | 192.27 | 20 |
| `scheduleCallback` | camelcase-identifier | 0.43 | 0.44 | 0.46 | 0.50 | 22 | 0.01 | 0.01 | 0.01 | 0.01 | 22 | 0.17 | 0.95 | 251.94 | 334.18 | 39 | 113.43 | 118.06 | 135.19 | 142.73 | 20 |
| `concurrent` | lowercase-word | 0.40 | 0.42 | 0.44 | 0.47 | 127 | 0.01 | 0.01 | 0.01 | 0.01 | 75 | 0.26 | 1.11 | 264.91 | 349.87 | 50 | 110.99 | 115.06 | 132.22 | 141.77 | 20 |
| `function` | lang-keyword | 1.69 | 1.78 | 1.82 | 1.85 | 5286 | 0.08 | 0.08 | 0.09 | 0.10 | 5245 | 15.00 | 15.67 | 254.49 | 336.27 | 50 | 44.28 | 47.07 | 62.95 | 65.44 | 20 |
| `set` | short-trigram-exact | 0.04 | 0.04 | 0.04 | 0.05 | 2038 | 0.02 | 0.02 | 0.02 | 0.02 | 851 | 3.32 | 6.43 | 249.41 | 370.86 | 50 | 43.19 | 47.00 | 63.77 | 65.49 | 20 |
| `ReactDOMRoot` | rare-camelcase | 0.14 | 0.15 | 0.15 | 0.16 | 8 | 0.01 | 0.01 | 0.01 | 0.01 | 6 | 0.11 | 0.56 | 255.69 | 351.61 | 12 | 187.75 | 194.15 | 217.31 | 232.72 | 12 |
| `xyzzy_react_does_not_exist` | negative | 0.19 | 0.21 | 0.22 | 0.23 | 0 | 0.03 | 0.03 | 0.04 | 0.04 | 0 | 0.04 | 0.28 | 252.61 | 346.77 | 0 | 181.21 | 186.96 | 209.90 | 226.89 | 0 |

## Normalized files-list comparison

Each backend asked the same question: return the SET of files containing the query.
`agree` is the pairwise Jaccard similarity (1.00 = all backends agree on the set).

| query | codedb files | fts5_tri files | fts5_uni files | leanctx files | agree-jaccard |
|---|---|---|---|---|---|
| `useState` | 716 | 674 | 674 | 8 | 0.479 |
| `useEffect` | 436 | 434 | 426 | 4 | 0.483 |
| `forwardRef` | 129 | 129 | 127 | 5 | 0.494 |
| `createElement` | 403 | 403 | 401 | 6 | 0.496 |
| `Fiber` | 275 | 303 | 180 | 5 | 0.356 |
| `Lane` | 69 | 72 | 40 | 4 | 0.344 |
| `Suspense` | 310 | 314 | 259 | 2 | 0.442 |
| `flushPassiveEffects` | 8 | 8 | 7 | 7 | 0.458 |
| `enableTransitionTracing` | 25 | 25 | 25 | 5 | 0.500 |
| `scheduleCallback` | 22 | 22 | 22 | 2 | 0.500 |
| `concurrent` | 118 | 127 | 75 | 4 | 0.344 |
| `function` | 5328 | 5286 | 5245 | 2 | 0.492 |
| `set` | 1614 | 2038 | 851 | 2 | 0.281 |
| `ReactDOMRoot` | 8 | 8 | 6 | 9 | 0.417 |
| `xyzzy_react_does_not_exist` | 0 | 0 | 0 | 0 | 1.000 |

