# Art Director Mode - Section

## Goal

Design one page section inside the already approved visual direction.

Work one section at a time.

## Required inputs

```text
PRODUCT.md
DESIGN.md
content/page.md
design/approved-direction/
```

Also use:

```text
previous approved sections
project references
```

If the section was already fully approved during Visual Direction, do not redesign it.

Proceed directly to asset/responsive handoff.

## Step 1 - block reference decision

At the start of the block:

```text
Specific reference?
CLOSE / ADAPT / INSPIRE?
```

Skip the question only if already answered for this block.

If there is no suitable direct reference:

- important/non-obvious block -> targeted research;
- obvious derivative block -> research may be skipped if approved direction already determines the solution.

## Step 2 - research when needed

Use `reference-researcher`.

Give it:

```text
section purpose
actual content shape
PRODUCT context
DESIGN context
approved visual direction
what is missing from current references
DEEP flag
```

Use its evidence, but do not copy a candidate blindly.

## Step 3 - variants

### Important / unique / non-obvious section

Create 2-3 rendered variants.

Examples of sections commonly deserving variants:

```text
Hero
Product Showcase
How it Works
Security
Comparison
complex Feature section
unusual CTA
```

This list is illustrative.

### Simple derivative section

Create one strong variant first.

Examples:

```text
simple CTA
FAQ
footer
small text section
straightforward secondary feature
```

If the operator rejects it, create alternatives.

## Variant quality

Use the actual approved copy.

Before rendering multiple variants, pass the variant distinction gate from `SKILL.md`.

Do not create fake variation through cosmetic styling.

## Present

For each variant show:

```text
rendered result
idea
reference influence with direct URL
why it fits this content
how it supports approved direction/funnel
assets needed
main tradeoff
```

## Operator approval

The operator may choose, combine, or request a focused revision.

After approval:

- produce one final section design;
- save the approved visual source;
- record reference/fidelity;
- perform asset check;
- perform responsive check.

## Asset check

If real media is required and missing, tell the operator exactly what is needed.

Examples:

```text
desktop app screenshot at X state
10-15 second product interaction video
real product photo
specific diagram/source data
```

Do not ask vaguely for "some assets".

If the exact asset can only be determined after design approval, this is the correct moment to ask.

## Responsive check

For a complex section, define how the design transforms on mobile.

Do not let Coder invent a materially different information hierarchy later.

## DESIGN.md

Update only if this approved section establishes a reusable system-level principle.

Do not add section-specific trivia to the design system.

## Exit / coder handoff

Return compactly:

```text
STATUS: READY FOR IMPLEMENTATION | BLOCKED
SECTION:
APPROVED SOURCE:
REFERENCE/FIDELITY:
ASSETS:
RESPONSIVE:
DESIGN.md UPDATE:
BLOCKERS:
```

Production implementation belongs to `$frontend-coder`.
