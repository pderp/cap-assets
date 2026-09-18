# Fidelity watch (DEC-064a)

<!-- HT-8 managed watch: begin -->

## Automated verified watch (HT-8)

Manual notes above are preserved. This source-bound table is regenerated from the locked journal; one entry per recipe cell. Both references are shown. Near-zero target-token loss does not establish unchanged predictions or reader inactivity.

Audited cells: 5; breaching cells: 5; creep alerts: 3. Development and confirmatory observations remain labelled; benchmarks never veto primary comparisons.

| Cell identity / scope | Condition / dataset / realization / order | Actual records / checkpoint | Reference | Mean KL | NLL increase | ES95 loss | Max loss | Positions for half KL | Near-zero loss fraction | Creep |
|---|---|---|---|---:|---:|---:|---:|---|---:|---|
| `3415c97ccbc1f3a7487baa52593bd467575afa27aa1db449b6566b413202277c` / development | primary / mquake / development / 1 | 300 / 300 | capoff | 0.001 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |
| `3415c97ccbc1f3a7487baa52593bd467575afa27aa1db449b6566b413202277c` / development | primary / mquake / development / 1 | 300 / 300 | original | 0.002 | 0 | 0 | 0 | 2 | 1 | none |
| `e1193af5a502412123b683549c50fd067dde484abeabe98d92a54e3746316f56` / confirmatory | primary / mquake / confirmatory / 2 | 300 / 300 | capoff | 0.001 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |
| `e1193af5a502412123b683549c50fd067dde484abeabe98d92a54e3746316f56` / confirmatory | primary / mquake / confirmatory / 2 | 300 / 300 | original | 0.002 | 0 | 0 | 0 | 2 | 1 | none |
| `78d027bdaa0f1040ec475dbe6850d9ea2e5c81251d22b8a761708d2c22b160e3` / confirmatory | primary / mquake / confirmatory / 3 | 300 / 300 | capoff | 0.001 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |
| `78d027bdaa0f1040ec475dbe6850d9ea2e5c81251d22b8a761708d2c22b160e3` / confirmatory | primary / mquake / confirmatory / 3 | 300 / 300 | original | 0.004 | 0 | 0 | 0 | 2 | 1 | new_running_maximum |
| `39ba13e5249bb897c377609a9b3d614f880e2da2d8aff5cff5bd69dad670715c` / confirmatory | primary / mquake / confirmatory / 4 | 300 / 300 | capoff | 0.001 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |
| `39ba13e5249bb897c377609a9b3d614f880e2da2d8aff5cff5bd69dad670715c` / confirmatory | primary / mquake / confirmatory / 4 | 300 / 300 | original | 0.0041 | 0 | 0 | 0 | 2 | 1 | above_twice_development_reference, new_running_maximum |
| `20e1e94d777d47b65449c240ca6445b6ac828dac6ca61983980e2d29cf191aa3` / development | primary / mquake / development / 5 | 300 / 300 | original | 0.00405 | 0 | 0 | 0 | 2 | 1 | above_twice_development_reference |
| `20e1e94d777d47b65449c240ca6445b6ac828dac6ca61983980e2d29cf191aa3` / development | primary / mquake / development / 5 | 300 / 300 | capoff | 0.001 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |

### Running maxima (all audited cells, including no-breach cells)

| Condition : dataset | Reference | Maximum KL | Maximum signed NLL increase | Development reference cell |
|---|---|---:|---:|---|
| primary:mquake | capoff | 0.001 | 0.01 | `3415c97ccbc1f3a7487baa52593bd467575afa27aa1db449b6566b413202277c` |
| primary:mquake | original | 0.0041 | 0 | `3415c97ccbc1f3a7487baa52593bd467575afa27aa1db449b6566b413202277c` |

### Creep alerts — orchestrator delivery queue

- **CREEP** `78d027bdaa0f1040ec475dbe6850d9ea2e5c81251d22b8a761708d2c22b160e3` (primary:mquake): original mean_kl 0.004 > 0.002 (new_running_maximum). Orchestrator reports immediately; this is not an admission veto.
- **CREEP** `39ba13e5249bb897c377609a9b3d614f880e2da2d8aff5cff5bd69dad670715c` (primary:mquake): original mean_kl 0.0041 > 0.004 (new_running_maximum); original mean_kl 0.0041 > 0.004 (above_twice_development_reference). Orchestrator reports immediately; this is not an admission veto.
- **CREEP** `20e1e94d777d47b65449c240ca6445b6ac828dac6ca61983980e2d29cf191aa3` (primary:mquake): original mean_kl 0.00405 > 0.004 (above_twice_development_reference). Orchestrator reports immediately; this is not an admission veto.

<!-- HT-8 managed watch: end -->
