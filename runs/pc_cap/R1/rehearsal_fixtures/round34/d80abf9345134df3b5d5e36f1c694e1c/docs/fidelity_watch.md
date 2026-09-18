# Fidelity watch (DEC-064a)

<!-- HT-8 managed watch: begin -->

## Automated verified watch (HT-8)

Manual notes above are preserved. This source-bound table is regenerated from the locked journal; one entry per recipe cell. Both references are shown. Near-zero target-token loss does not establish unchanged predictions or reader inactivity.

Audited cells: 4; breaching cells: 3; creep alerts: 1. Development and confirmatory observations remain labelled; benchmarks never veto primary comparisons.

| Cell identity / scope | Condition / dataset / realization / order | Actual records / checkpoint | Reference | Mean KL | NLL increase | ES95 loss | Max loss | Positions for half KL | Near-zero loss fraction | Creep |
|---|---|---|---|---:|---:|---:|---:|---|---:|---|
| `2573ca3b554d9eb16328a79570fac761e508c84b97b7ae3ac32ae1f18326ea09` / development | primary / mquake / development / 2 | 300 / 300 | capoff | 0.002 | 0 | 0 | 0 | 2 | 1 | above_twice_development_reference, new_running_maximum |
| `2573ca3b554d9eb16328a79570fac761e508c84b97b7ae3ac32ae1f18326ea09` / development | primary / mquake / development / 2 | 300 / 300 | original | 0 | 0 | 0 | 0 | 2 | 1 | none |
| `2fff2c4352439f6fb63a1c39484931ef488949b2fdaf927bcb2881ddb2a3a0bf` / development | other / mquake / development / 3 | 300 / 300 | capoff | 0.001 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |
| `2fff2c4352439f6fb63a1c39484931ef488949b2fdaf927bcb2881ddb2a3a0bf` / development | other / mquake / development / 3 | 300 / 300 | original | 0.1 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |
| `8d1cb7ebbd88d29c2b7e8ce4d3e18f503017b1393d6b15a9093ff059675e0d7c` / confirmatory | primary / zsre / confirmatory / 4 | 300 / 300 | original | 0.1 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |
| `8d1cb7ebbd88d29c2b7e8ce4d3e18f503017b1393d6b15a9093ff059675e0d7c` / confirmatory | primary / zsre / confirmatory / 4 | 300 / 300 | capoff | 0.001 | 0.01 | 0.01 | 0.01 | 2 | 1 | none |

### Running maxima (all audited cells, including no-breach cells)

| Condition : dataset | Reference | Maximum KL | Maximum signed NLL increase | Development reference cell |
|---|---|---:|---:|---|
| other:mquake | capoff | 0.001 | 0.01 | `2fff2c4352439f6fb63a1c39484931ef488949b2fdaf927bcb2881ddb2a3a0bf` |
| other:mquake | original | 0.1 | 0.01 | `2fff2c4352439f6fb63a1c39484931ef488949b2fdaf927bcb2881ddb2a3a0bf` |
| primary:mquake | capoff | 0.002 | 0 | `3415c97ccbc1f3a7487baa52593bd467575afa27aa1db449b6566b413202277c` |
| primary:mquake | original | 0 | 0 | `3415c97ccbc1f3a7487baa52593bd467575afa27aa1db449b6566b413202277c` |
| primary:zsre | original | 0.1 | 0.01 | `unavailable` |
| primary:zsre | capoff | 0.001 | 0.01 | `unavailable` |

### Creep alerts — orchestrator delivery queue

- **CREEP** `2573ca3b554d9eb16328a79570fac761e508c84b97b7ae3ac32ae1f18326ea09` (primary:mquake): capoff mean_kl 0.002 > 0 (new_running_maximum); capoff mean_kl 0.002 > 0 (above_twice_development_reference). Orchestrator reports immediately; this is not an admission veto.

<!-- HT-8 managed watch: end -->
