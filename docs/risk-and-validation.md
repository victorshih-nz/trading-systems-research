# Risk and Validation

This project uses a fail-closed approach.

## Fail-closed principle

If the system cannot establish enough confidence in the current state, the safe behaviour is to stop trusting the action or observation.

Conceptual examples:

| Situation | Public design response |
| --- | --- |
| market data becomes stale | reject current evaluation |
| stream continuity is uncertain | quarantine affected evidence |
| local state cannot be reconciled | stop progressing the action |
| more than one state appears authoritative | fail closed |
| execution evidence is ambiguous | do not count as authoritative fill |
| run is interrupted | preserve unknown outcome |
| risk boundary is breached | block new action |

## Why this matters

A research platform can create misleading results if it silently converts uncertainty into certainty.

Examples:

- assuming a fill because price touched a level
- treating missing observations as zero return
- continuing after a feed gap without marking affected outcomes
- reconstructing an interrupted trade as a win or loss without evidence

The project instead tries to preserve uncertainty explicitly.

## Risk boundaries

The private implementation contains hard limits around areas such as:

- exposure
- position count
- planned loss
- cumulative loss states
- leverage/margin configuration
- data freshness
- system readiness

Exact values are intentionally private.

## Validation layers

The project uses several validation layers:

### Unit tests

Small deterministic tests verify business rules, state transitions, parsing, reporting, and edge cases.

### Deterministic simulation

Synthetic fixtures test whether controls behave correctly.

These simulations validate logic; they do **not** prove market profitability.

### Historical research

Historical data is used to evaluate hypotheses under frozen rules.

### Shadow / paper observation

New data is observed without assuming immediate live deployment.

### Promotion review

Only evidence that passes the required checks is considered for the next stage.

## Core distinction

A system can be:

- technically correct
- operationally reliable
- statistically interesting

and still **not** be ready for live capital.

That separation is intentional.
