---
name: design-context
description: Analyze operator-supplied website references, existing product UI, and brand materials to create the initial project DESIGN.md for Stage 1B. Use only when explicitly invoked in the dedicated Design Context window. Do not invent page layouts, search for unrelated inspiration, write marketing copy, implement production UI, or act as Art Director.
---

# Website Design Context

## Purpose

You own Stage 1B: convert the project's existing visual evidence into an honest initial design system.

Primary artifact:

```text
DESIGN.md
```

If Impeccable is installed, also keep its generated sidecar aligned:

```text
.impeccable/design.json
```

This is **design context extraction**, not Art Direction.

You describe the visual language the project already intends to follow.

You do not invent the page's future block compositions.

## Required inputs

Read:

```text
PRODUCT.md
references/
```

Also inspect when available:

```text
existing product UI
brand assets
logos
screenshots
live reference URLs
existing CSS/tokens/components
```

If `PRODUCT.md` is missing, return `BLOCKED` and route back to Stage 0.

## Reference contract

Before analysis, establish what each reference is for.

When the operator already specified this, do not ask again.

Possible reference roles:

```text
PRIMARY
SECONDARY
PRODUCT_UI
BRAND_ONLY
CONTENT_ONLY
```

For visual references, determine which properties are intended to carry over, for example:

```text
typography
colors
density
spacing
geometry
navigation/components
product presentation
icon language
imagery
motion
responsive behavior
```

If multiple references conflict materially and the operator has not stated which one wins, propose the smallest useful choice and ask only about that conflict.

Do not average incompatible references into a generic middle.

## No random inspiration research

Do not use Mobbin, Landbook, Godly, SaaSFrame, Impeccable examples, or general inspiration search to fill missing design decisions in Stage 1B.

Those belong to Art Director targeted reference research later.

Web/browser access here is for:

- opening operator-supplied references;
- inspecting their implementation when accessible;
- verifying fonts/assets/style behavior;
- viewing responsive states or motion when the live reference supports it.

## Analyze the visual DNA

Extract only what the evidence supports.

### Overview / visual character

Identify:

- overall visual character;
- information density;
- whitespace rhythm;
- contrast strategy;
- container behavior;
- page/surface feel;
- product-presentation language;
- any clearly repeated layout principles.

Do not create future section layouts.

### Colors

Determine when evidence allows:

- page/background colors;
- surface colors;
- primary/secondary text;
- accent/action colors;
- borders/dividers;
- semantic/status colors if genuinely present.

Prefer exact CSS/token values when accessible.

If color is estimated from a screenshot, label it approximate/provisional.

### Typography

Determine:

- font families;
- weights;
- display/body/label roles;
- scale relationships;
- line-height/tracking character;
- casing conventions.

Do not claim an exact font if it cannot be verified.

### Elevation / geometry

Determine:

- flat vs layered treatment;
- borders;
- shadows;
- radius behavior;
- cards/panels only when they are actually part of the reference language.

### Components

Capture reusable visual behavior that is already evidenced:

- buttons;
- navigation;
- tabs;
- inputs;
- badges;
- tables;
- product UI frames;
- icons;
- section containers;
- other recurring primitives.

Do not extract a component system from a one-off decorative element.

### Media / product visuals

Capture:

- screenshots vs illustrations vs photography;
- framing/cropping;
- device/window chrome;
- diagram style;
- icon style;
- animation/motion character when observable.

### Responsive behavior

If a live reference is available, inspect enough viewport behavior to identify system-level responsive principles.

Do not invent responsive rules from a desktop screenshot.

## Uncertainty protocol

Never hide uncertainty inside `DESIGN.md`.

Classify unresolved decisions:

```text
CONFIRMED
PROVISIONAL
MISSING INPUT
```

A decision is `CONFIRMED` only when supported by:

- source code/tokens;
- a live reference;
- a clear operator instruction;
- repeated consistent visual evidence.

A screenshot estimate or weak inference is `PROVISIONAL`.

## Mandatory operator notice

Before finalizing `DESIGN.md`, explicitly tell the operator:

```text
Confirmed:
Provisional:
Missing / needed from you:
Why it matters:
```

Do not merely annotate provisional items in the file.

If the missing item is non-blocking, recommend a temporary provisional choice and continue only after making that status clear.

If the missing item would materially define the visual system, ask the operator instead of inventing it.

Examples:

- exact proprietary font unavailable;
- primary reference conflicts with brand logo colors;
- motion cannot be inferred from static screenshots;
- mobile behavior is unknown;
- operator has not said which of two contradictory references wins.

## Impeccable integration

Impeccable is an optional formatting/context tool, not the decision-maker.

### Step 1 - analyze first

Complete the reference analysis and uncertainty notice **before** running Impeccable document.

Prepare the answers Impeccable seed mode will need, especially:

```text
creative north star / visual character
color strategy
type direction
motion direction
references
anti-references / explicit things to avoid
```

Do not let seed questions replace your reference analysis.

### Step 2 - seed DESIGN.md

If Impeccable is installed and `/impeccable document --seed` is available:

1. invoke/run that command after the analysis;
2. answer it using the confirmed analysis and operator decisions;
3. create the root `DESIGN.md`;
4. preserve `.impeccable/design.json`.

If the command cannot be invoked from the current harness, tell the operator exactly once to run:

```text
/impeccable document --seed
```

Then resume after it completes.

### Step 3 - verify output

Read the generated `DESIGN.md`.

Verify it reflects the evidence and operator decisions.

Do not accept a seed output merely because Impeccable generated it.

If a material correction is needed and `.impeccable/design.json` exists, prefer rerunning the Impeccable document flow with corrected inputs so `DESIGN.md` and the sidecar remain synchronized.

Use `/impeccable doctor` only when there is an actual context/sidecar/hook consistency problem.

Do not run `/impeccable extract` in Stage 1B.

### No Impeccable

If Impeccable is not installed, create `DESIGN.md` yourself using:

```text
assets/design-template.md
```

Keep the same six top-level sections so the file remains compatible with the documented Impeccable/Google Stitch structure.

## DESIGN.md truthfulness

This is a greenfield seed until real UI exists.

Do not pretend that unimplemented tokens/components are already production facts.

When appropriate, include:

```html
<!-- SEED -->
```

and clearly distinguish provisional values inside the relevant section.

Do not add extra top-level sections outside the compatible six-section structure.

Fold system-level layout/responsive/motion principles into:

- `01 Overview`;
- or the relevant component entries.

## Completion check

Before reporting Stage 1B ready:

- `DESIGN.md` exists;
- it uses the required six top-level sections;
- reference priority is clear;
- exact vs approximate values are distinguishable;
- important gaps were separately reported to the operator;
- no random external inspiration was used to fill missing decisions;
- no future page block compositions were invented;
- if Impeccable is enabled, sidecar/context consistency is acceptable.

Return a concise summary:

```text
STATUS: READY | BLOCKED
CONFIRMED:
PROVISIONAL:
NEEDS OPERATOR:
ARTIFACTS:
```

Do not ask for a separate Stage 1B approval when the workflow expects the joint Strategy + Design Context review.
