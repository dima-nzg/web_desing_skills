# Reviewer Mode - Whole Page

## Goal

Review the completed page as one system after every section has already passed operator approval.

Use a fresh reviewer context when practical.

Do not repeat section-level nitpicks.

## Required inputs

```text
live full page
DESIGN.md
content/page.md
approved visual direction
approved sections or representative approved mockups
```

If the live page cannot be inspected, return `BLOCKED`.

## What to inspect

Only page-level issues:

### Rhythm

- section pacing;
- density vs whitespace;
- abrupt transitions;
- multiple consecutive sections with the same composition;
- sections that visually dominate or disappear without intent.

### Hierarchy

- where attention goes from Hero to final CTA;
- whether product proof and conversion points remain visible;
- whether page-level emphasis matches the intended funnel.

### System consistency

- shared typography behavior;
- backgrounds;
- product visual language;
- container/section spacing;
- repeated primitives.

### Desktop/mobile coherence

Check that the mobile page preserves the same information hierarchy and intent, not merely that it technically fits.

### Funnel continuity

Use `content/page.md`.

Flag only where implementation/page composition materially weakens the already approved content flow.

Do not reopen copy strategy merely because another wording is possible.

## Exclusions

Do not:

- re-review each section from scratch;
- propose new sections;
- replace the approved visual direction;
- invent a new reference standard.

A whole page can be `CLEAN`.
