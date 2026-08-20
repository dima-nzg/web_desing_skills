# Reviewer Mode - Section

## Goal

Review one implemented section after the operator already approved its design.

This is an implementation review, not a new design exploration.

## Required inputs

At minimum:

```text
approved section mockup or approved visual source
DESIGN.md
relevant section from content/page.md
live rendered section
target route / viewport context
```

Useful when available:

```text
neighboring approved sections
responsive intent
original implementation findings for scoped re-review
```

If the approved visual source or live render is unavailable, return `BLOCKED`.

## What to inspect

### Fidelity

Compare live implementation to approved design:

- composition;
- proportions;
- alignment;
- spacing;
- typography;
- background/surface treatment;
- asset treatment;
- intended emphasis.

Do not penalize harmless pixel-level differences.

### Responsive behavior

Check the viewports that matter for the section.

At minimum, inspect desktop and mobile when browser tooling permits.

Look for:

- overflow;
- clipped content;
- broken stacking;
- collapsed hierarchy;
- unusable touch targets;
- asset cropping that changes meaning;
- interaction states that fail.

### Implementation-introduced slop

Flag simplification only when implementation degraded an approved decision.

Examples:

- approved asymmetric layout became generic equal cards;
- custom product visual became a generic icon block;
- distinctive hierarchy was flattened;
- approved visual asset was replaced by a placeholder.

Do not use "AI-slop" as a generic aesthetic insult.

### Cross-section consistency

If previous approved sections are available, check only obvious system drift:

- duplicated composition that weakens page rhythm;
- inconsistent shared primitive;
- contradictory spacing/type treatment.

Do not redesign the page from one section review.

## Approved-mockup problem

If the implementation faithfully matches the mockup but the mockup itself now causes a real problem:

```text
OWNER: ART_DIRECTOR
```

Describe the problem and escalate.

Do not tell Coder to diverge from the approved design.

## Re-review

On a fix pass, review only the supplied finding IDs plus regressions introduced by the fix.
