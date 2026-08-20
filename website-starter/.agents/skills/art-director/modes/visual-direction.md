# Art Director Mode - Visual Direction

## Goal

Establish one coherent visual direction for the page on real approved content before every section is designed.

Primary output:

```text
design/approved-direction/
```

Representative section designs that the operator considers final may also enter:

```text
design/approved-sections/
```

## Required inputs

```text
PRODUCT.md
DESIGN.md
content/page.md
references/
```

If any of the first three is missing, return `BLOCKED`.

## Choose representative content

Select 2-3 sections that expose the page's visual language well.

Usually:

```text
Hero
one product/content showcase
one structurally different important section
```

Do not always choose the same trio if this page has a more representative pattern.

## Reference handling per representative block

For each representative block:

1. use the operator's direct reference when supplied;
2. confirm CLOSE / ADAPT / INSPIRE if not already specified;
3. if the source references do not contain the needed block, use targeted reference research before designing it.

Do not make the operator separately approve the research list.

## Direction variants

Create 2-3 rendered **page directions**, not three isolated unrelated sections.

Each direction must show how the same visual language continues across the representative sections.

Before rendering, define one compact hypothesis per direction.

Example dimensions:

```text
product-first asymmetric
editorial / type-led
interface-led / dense proof
```

These are examples, not default archetypes.

Do not force them when references imply something else.

## Direction consistency

Within one direction, keep coherent:

```text
type hierarchy
container/grid logic
surface treatment
product/media treatment
section rhythm
accent strategy
interaction/motion character where shown
```

The three directions may differ substantially, but each individual direction must feel like one site.

## Present to operator

For each direction show:

```text
rendered preview
short pitch
specific reference URLs that materially influenced it
what would carry forward to the rest of the page
main tradeoff
```

Do not pitch generic adjectives like "modern" or "premium" without explaining the concrete design idea.

## Operator choice

The operator may:

- select one;
- combine strong parts of multiple directions;
- request a focused revision.

When combining, resolve conflicts into one coherent direction instead of literally stitching incompatible styles together.

## Approval

After selection:

1. create the approved visual source;
2. update `DESIGN.md` only with newly approved system-level principles;
3. preserve the references actually used;
4. mark any representative section that is already compositionally final as approved so Section Mode does not redesign it.

## Exit

Return:

```text
STATUS: READY | BLOCKED
APPROVED DIRECTION:
APPROVED REPRESENTATIVE SECTIONS:
DESIGN.md CHANGES:
ASSET GAPS:
NEXT:
```

Next is the Section Loop.
