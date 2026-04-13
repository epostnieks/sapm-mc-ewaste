# Monte Carlo Assumptions — E-Waste Export / Basel Convention Evasion

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $1,050.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 6.59 | Confirmed by N=100,000 draws |
| ΔW median (result) | $6,922.2B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_planned_obsolescence` | lognormal | $2,000B | $3,000B | $4,500B | Deadweight loss from designed-in obsolescence |
| `C2_toxic_health` | lognormal | $1,000B | $1,600B | $2,500B | Lead, mercury, cadmium exposure in informal recycling |
| `C3_environmental` | lognormal | $600B | $1,000B | $1,600B | Soil/water contamination, ecosystem damage |
| `C4_lost_materials` | normal | $45B | $62B | $80B | Unrecovered gold, copper, rare earths |
| `C5_carbon` | lognormal | $400B | $700B | $1,100B | Carbon cost of replacement manufacturing |
| `C6_governance` | lognormal | $250B | $450B | $700B | Basel Convention evasion, export displacement |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 2.5 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 2.5) = 0.0000%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 6.49 | 20% DC adj = 5.19 | 40% DC adj = 3.89

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $6,922B = 6.5% of world GDP ($106T) ✓
- **β_W range**: 6.59 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
