# Phase 20 - Content

Covers `WORKFLOW.md` Stage 2 Content Wireframe.

## Goal

Route the operator through the Strategist-led block-by-block content finalization until `content/page.md` is approved.

## Specialist

Use the existing Strategist window if available.

Explicit invocation when a new window is required:

```text
$strategist
```

Strategist owns this stage.

The orchestrator does not write the page copy.

## Expected behavior

The Strategist asks whether the operator has additional references for content/tone.

For each important section the Strategist provides 2-3 meaningful content variants, explains the marketing/funnel/SEO logic in plain language, and lets the operator select or combine.

The result should be practically final copy, not placeholder copy.

## Canonical artifact

```text
content/page.md
```

After this stage, it remains the canonical source of approved copy.

Later Art Director or Coder may propose copy changes, but they must not silently edit live copy first. Approved copy changes go through `content/page.md`.

## Human gate

Gate:

```text
content
```

Approve only after the operator explicitly confirms:

- section order;
- meaning of sections;
- main copy;
- CTA logic;
- overall funnel flow.

## State transition

After approval:

```text
artifacts.page = ready
gates.content = approved
stage = visual_direction
```

Tell the operator to open the Art Director window:

```text
$art-director
```
