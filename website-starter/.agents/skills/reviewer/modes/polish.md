# Reviewer Mode - Polish

## Goal

Compare an already accepted live page against an explicit external comparable and identify concrete remaining differences.

This mode is optional and bounded.

## Hard precondition

A comparable selected by the operator must exist, for example:

```text
reference URL
reference screenshot
approved external visual reference
explicit measurable target
```

`DESIGN.md`, general best practices, "modern", and the critic's personal taste are not sufficient external comparables.

If no usable comparable exists:

```text
VERDICT: BLOCKED
BLOCKERS: operator must supply a comparison reference
```

Do not invent one.

## Inputs

```text
live page
external comparable
PRODUCT.md when product intent matters
content/page.md when copy/funnel differences matter
titles/IDs of findings fixed in previous polish rounds
```

Do not ingest previous critics' full essays unless required for scoped verification.

## One critic pass

Compare side by side where tooling permits.

Return only concrete, checkable differences.

A finding survives only when:

1. the difference is observable against the supplied comparable or an approved product requirement;
2. fixing it does not require inventing a new product decision;
3. the condition can be verified after a fix.

Bad:

```text
Make it more premium.
Add richer gradients.
It could feel more dynamic.
```

Good:

```text
The reference maintains a strong size contrast between section headline and support copy, while the live page compresses them into nearly the same scale across three consecutive sections.
```

## Ownership

Route each surviving difference to:

```text
CODER
ART_DIRECTOR
STRATEGIST
OPERATOR
```

Do not fix it yourself.

## Bounded loop

The parent workflow owns the round count.

Maximum:

```text
3 rounds
```

Stop when the first condition occurs:

- a round yields no meaningful surviving differences;
- 3 rounds are complete;
- operator stops.

## Regression rule

If a polish round breaks previously accepted behavior or clearly degrades the approved result, recommend reverting that round instead of opening an unbounded repair cycle.

## Re-review

Verify only the differences that were selected for fixing and regressions caused by those fixes.
