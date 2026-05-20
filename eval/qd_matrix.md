# QD Matrix — code-search-shootout

Tasks: 16  ·  Backends: 5  ·  Filled cells: 67

## Quality (out of 5) — mean per cell

| task | codedb | codedb_LEAN | fts5_trigram | leanctx | codegraph |
|---|---|---|---|---|---|
| `T0_getNextLanes` | 5.00±0.00 (n=2) | — | 5.00 | 4.00 | 5.00 |
| `T1_setState_trace` | 4.67±0.58 (n=3) | 5.00 | 5.00 | 5.00 | 3.00 |
| `T2_snapshot_flag_sites` | 4.00±0.71 (n=5) | 3.00 | 5.00 | 3.00 | 5.00 |
| `T3_compare_two_functions` | 5.00±0.00 (n=2) | 5.00 | 5.00 | 5.00 | 5.00 |
| `R0_find_iter` | 5.00 | — | 5.00 | 5.00 | 5.00 |
| `R1_pattern_compile_trace` | 4.50±0.71 (n=2) | — | 4.00 | 4.00 | 4.00 |
| `R2_matchkind_all_sites` | 4.00±0.00 (n=2) | — | 3.00 | 3.00 | 4.00 |
| `R3_pikevm_vs_backtrack` | 5.00 | — | 3.00 | 5.00 | 4.00 |
| `F0_url_for` | 5.00 | — | 5.00 | 5.00 | 5.00 |
| `F1_route_decorator_trace` | 5.00 | — | 4.00 | 3.00 | 5.00 |
| `F2_before_request_sites` | 4.00 | — | 5.00 | 2.00 | 3.00 |
| `F3_app_vs_blueprint` | 5.00 | — | 5.00 | 4.00 | 4.00 |
| `G0_context_json` | 5.00 | — | 5.00 | 5.00 | 5.00 |
| `G1_engine_run_trace` | 4.00 | — | 2.00 | 2.00 | 5.00 |
| `G2_default_middleware_sites` | 5.00 | — | 2.00 | 4.00 | 4.00 |
| `G3_bind_vs_shouldbind` | 5.00 | — | 5.00 | 5.00 | 5.00 |

### Per-backend averages (across all tasks where measured)

| backend | avg quality | avg tokens | avg wall (s) | avg calls | tokens / quality-point |
|---|---|---|---|---|---|
| **codedb** | 4.70 | 16,717 | 16.6 | 6.5 | 3,558 |
| **codedb_LEAN** | 4.33 | 24,474 | 108.0 | 14.7 | 5,648 |
| **fts5_trigram** | 4.25 | 17,511 | 28.6 | 7.9 | 4,120 |
| **leanctx** | 4.00 | 18,370 | 43.3 | 9.9 | 4,593 |
| **codegraph** | 4.44 | 6,929 | 48.9 | 12.1 | 1,562 |

## Efficiency (tokens) — mean per cell

| task | codedb | codedb_LEAN | fts5_trigram | leanctx | codegraph |
|---|---|---|---|---|---|
| `T0_getNextLanes` | 21,198±1,980 (n=2) | — | 14,523 | 21,212 | 2,100 |
| `T1_setState_trace` | 18,253±2,689 (n=3) | 35,504 | 17,876 | 18,370 | 9,500 |
| `T2_snapshot_flag_sites` | 15,967±2,661 (n=5) | 20,123 | 15,853 | 23,661 | 28,000 |
| `T3_compare_two_functions` | 15,151±1,283 (n=2) | 17,795 | 15,307 | 15,361 | 11,000 |
| `R0_find_iter` | 13,642 | — | 14,299 | 17,729 | 450 |
| `R1_pattern_compile_trace` | 25,734±2,232 (n=2) | — | 22,645 | 32,596 | 9,000 |
| `R2_matchkind_all_sites` | 15,251±3,371 (n=2) | — | 21,030 | 18,040 | 28,000 |
| `R3_pikevm_vs_backtrack` | 19,467 | — | 15,844 | 24,645 | 4,200 |
| `F0_url_for` | 14,846 | — | 13,077 | 13,958 | 850 |
| `F1_route_decorator_trace` | 15,070 | — | 18,488 | 13,877 | 7,800 |
| `F2_before_request_sites` | 15,175 | — | 17,971 | 14,285 | 3,000 |
| `F3_app_vs_blueprint` | 14,450 | — | 15,921 | 15,162 | 2,100 |
| `G0_context_json` | 17,688 | — | 25,638 | 15,625 | 420 |
| `G1_engine_run_trace` | 17,140 | — | 17,731 | 16,560 | 1,650 |
| `G2_default_middleware_sites` | 13,410 | — | 17,936 | 18,029 | 400 |
| `G3_bind_vs_shouldbind` | 15,029 | — | 16,043 | 14,813 | 2,400 |

## Wall time (seconds) — mean per cell

| task | codedb | codedb_LEAN | fts5_trigram | leanctx | codegraph |
|---|---|---|---|---|---|
| `T0_getNextLanes` | 31.5±17.7 (n=2) | — | 25.0 | 123.0 | 15.0 |
| `T1_setState_trace` | 59.7±42.9 (n=3) | 226.0 | 95.0 | 91.0 | 45.0 |
| `T2_snapshot_flag_sites` | 24.4±24.3 (n=5) | 46.0 | 49.0 | 121.0 | 180.0 |
| `T3_compare_two_functions` | 21.5±9.2 (n=2) | 52.0 | 29.0 | 61.0 | 75.0 |
| `R0_find_iter` | 21.0 | — | 12.0 | 12.0 | 5.0 |
| `R1_pattern_compile_trace` | 29.5±27.6 (n=2) | — | 32.0 | 68.0 | 55.0 |
| `R2_matchkind_all_sites` | 2.0±1.4 (n=2) | — | 28.0 | 28.0 | 210.0 |
| `R3_pikevm_vs_backtrack` | 12.0 | — | 25.0 | 38.0 | 28.0 |
| `F0_url_for` | 22.0 | — | 12.0 | 18.0 | 12.0 |
| `F1_route_decorator_trace` | 18.0 | — | 38.0 | 18.0 | 35.0 |
| `F2_before_request_sites` | 4.0 | — | 18.0 | 18.0 | 45.0 |
| `F3_app_vs_blueprint` | 4.0 | — | 18.0 | 12.0 | 12.0 |
| `G0_context_json` | 6.0 | — | 12.0 | 6.0 | 8.0 |
| `G1_engine_run_trace` | 4.0 | — | 18.0 | 22.0 | 35.0 |
| `G2_default_middleware_sites` | 1.0 | — | 28.0 | 45.0 | 5.0 |
| `G3_bind_vs_shouldbind` | 5.0 | — | 18.0 | 12.0 | 18.0 |

## Pareto frontier

A backend is **Pareto-dominant** if no other backend beats it on all three axes (quality higher, tokens lower, wall lower).

| backend | quality | tokens | wall (s) | status |
|---|---|---|---|---|
| codedb | 4.70 | 16,717 | 16.6 | **PARETO-OPTIMAL** |
| codegraph | 4.44 | 6,929 | 48.9 | **PARETO-OPTIMAL** |
| codedb_LEAN | 4.33 | 24,474 | 108.0 | dominated by: codedb, codegraph |
| fts5_trigram | 4.25 | 17,511 | 28.6 | dominated by: codedb |
| leanctx | 4.00 | 18,370 | 43.3 | dominated by: codedb, fts5_trigram |

## MAP-Elites grid

Rows = behavioral niche (`query_type`). Cols = backend.
Each cell shows aggregated (quality / tokens / wall) over tasks in that niche.
**Bold** = best in row on quality; *italic* = best in row on tokens.

| niche | codedb | codedb_LEAN | fts5_trigram | leanctx | codegraph |
|---|---|---|---|---|---|
| `uncategorized` (4 tasks) | **5.00** / 17,199 / 26.5s | 5.00 / 20,123 / 52.0s | 5.00 / 15,580 / 39.0s | 4.50 / 19,791 / 106.0s | 5.00 / *10,250* / 60.0s |
| `symbol-lookup` (3 tasks) | **5.00** / 14,846 / 21.0s | — | 5.00 / 14,299 / 12.0s | 5.00 / 15,625 / 12.0s | 5.00 / *450* / 8.0s |
| `trace` (3 tasks) | 4.50 / 17,140 / 18.0s | — | 4.00 / 18,488 / 32.0s | 3.00 / 16,560 / 22.0s | **5.00** / *7,800* / 35.0s |
| `pattern-find` (3 tasks) | **4.00** / 15,175 / 2.0s | — | 3.00 / 17,971 / 28.0s | 3.00 / 18,029 / 28.0s | 4.00 / *3,000* / 45.0s |
| `comparison` (3 tasks) | **5.00** / 15,029 / 5.0s | — | 5.00 / 15,921 / 18.0s | 5.00 / 15,162 / 12.0s | 4.00 / *2,400* / 18.0s |

### Niche wins per backend

| backend | niches won on quality | niches won on tokens |
|---|---|---|
| codedb | 4 | 0 |
| codedb_LEAN | 0 | 0 |
| fts5_trigram | 0 | 0 |
| leanctx | 0 | 0 |
| codegraph | 1 | 5 |
