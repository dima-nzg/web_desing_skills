# Phase 10 - Strategy + Design Context

Covers `WORKFLOW.md` Stage 1A + Stage 1B and their joint operator review.

## Goal

Wait for the two parallel specialist tracks to produce:

```text
content/strategy.md
DESIGN.md
```

Do not perform either track inside the orchestrator.

## Strategist track

Preferred window:

```text
existing Strategist window
```

Expected artifact:

```text
content/strategy.md
```

Pass current project setting:

```text
seo_mode
deep
```

## Design Context track

Preferred window:

```text
Design Context window
```

Expected artifact:

```text
DESIGN.md
```

If Impeccable is enabled, the Design Context specialist owns the `document --seed` step after reference analysis.

Any provisional design decisions or missing source material must be surfaced to the operator before joint approval.

## Readiness check

Do not approve based on file existence alone.

Confirm:

- both artifacts exist;
- each specialist reports its stage complete;
- Design Context has surfaced material uncertainties;
- the operator has reviewed both artifacts together.

The operator may request changes in either specialist window.

## Human gate

Gate:

```text
strategy_design_review
```

Mark it `approved` only after explicit operator approval of the combined Strategy + Design Context direction.

## State transition

After approval:

```text
artifacts.strategy = ready
artifacts.design = ready
gates.strategy_design_review = approved
stage = content
```

Tell the operator to return to the **same Strategist window** if available and continue with Stage 2.

Do not require Design Context window to stay open after approval.
