# Engineering Decisions

This document captures several public design decisions from the private project.

## 1. Authoritative journal first

The system keeps a durable append-oriented event history as the authoritative record.

A local database/dashboard is useful for analysis, but it is treated as a projection that can be rebuilt.

**Reason:** convenience storage should not silently redefine history.

## 2. Separate research logic from execution logic

Strategy hypotheses are kept conceptually separate from execution assumptions.

**Reason:** a research result should not depend on an optimistic hidden fill model.

## 3. Record uncertainty explicitly

Ambiguous and censored outcomes have their own states.

**Reason:** unknown is not the same as zero, loss, or win.

## 4. Freeze rules before evaluation

Experiment rules are fixed before the corresponding evaluation window is interpreted.

**Reason:** reduce hindsight-driven parameter changes.

## 5. Prefer observable evidence

The design avoids conclusions that require unavailable future information or unverifiable execution assumptions.

**Reason:** make the research path auditable.

## 6. Rebuildable projections

Dashboards and local query databases can be reconstructed from authoritative events.

**Reason:** reporting infrastructure should be recoverable without inventing new trading outcomes.

## 7. Small components and focused tests

The private codebase separates concerns such as ingestion, validation, risk, storage, strategy research, and reporting.

**Reason:** a single large trading loop becomes difficult to reason about and easy to break.

## 8. Promotion is a decision gate

Research output is not automatically promoted to a higher-risk stage.

**Reason:** engineering readiness, data quality, execution quality, and statistical evidence are different dimensions.

## 9. Private/public boundary

This showcase intentionally describes architecture and decisions without publishing:

- strategy implementation
- research parameters
- exchange integration
- credentials
- logs
- account data

**Reason:** demonstrate engineering judgement without exposing sensitive operational or research details.
