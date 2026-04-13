# SAPM Monte Carlo — E-Waste Export / Basel Convention Evasion

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *E-Waste Export (Basel Convention Evasion).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **6.59** |
| β_W mean | 6.71 |
| β_W std | 1.25 |
| **90% CI** | **[4.9, 8.9]** |
| 99% CI | [4.3, 10.1] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$6,922.2B/yr** |
| Π (revenue) | $1,050.0B/yr |

**β_W = 6.59** means the e-waste export industry destroys **$6.59 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 1 — Impossibility

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-ewaste.git
cd sapm-mc-ewaste
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 6.59` and `ΔW median : $6,922.2B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_planned_obsolescence | $2,995.9B | [$1,994.3B, $4,493.2B] | Lognormal |
| C2_toxic_health | $1,598.9B | [$1,022.4B, $2,508.2B] | Lognormal |
| C3_environmental | $999.5B | [$625.2B, $1,599.0B] | Lognormal |
| C4_lost_materials | $62.0B | [$44.4B, $79.4B] | Normal |
| C5_carbon | $698.7B | [$446.1B, $1,096.2B] | Lognormal |
| C6_governance | $449.5B | [$289.6B, $699.9B] | Lognormal |
| **Total ΔW** | **$6,922.2B** | **[$5,115.9B, $9,389.5B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 2.5 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0000%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — E-Waste Export (Basel Convention Evasion)*.
> GitHub: epostnieks/sapm-mc-ewaste.
> https://github.com/epostnieks/sapm-mc-ewaste
