# Phase 50 - Final

Covers `WORKFLOW.md` Stages 5-8.

## Goal

Run fresh whole-page review, optional bounded polish, final SEO/technical review, operator final review, explicit release authorization, and lightweight retrospective.

The orchestrator coordinates these checks but does not perform them inline.

## 1. Fresh Final Page Review

Use a **fresh** custom agent:

```text
visual-reviewer
```

Do not reuse the persistent Section Reviewer as the primary final judge.

The reviewer evaluates only whole-page issues:

- rhythm between sections;
- repeated composition;
- visual density;
- cross-section hierarchy;
- funnel continuity;
- desktop/mobile coherence.

Reviewer returns concrete findings only and does not edit application code.

Art Director/Coder own fixes.

A follow-up review is scoped to the findings and fix diff.

## 2. Optional POLISH

Run only when:

```text
settings.polish = true
```

Hard precondition: there is an external comparable selected by the operator, such as:

- reference URL;
- reference screenshot;
- approved visual reference;
- another explicit external standard.

Without a comparable, do not let the critic invent one. Report that POLISH cannot run meaningfully and continue to final checks unless the operator supplies a reference.

Each polish round uses a fresh visual critic when practical.

Round:

```text
live page vs reference
-> concrete checkable differences
-> filter meaningful findings
-> Art Director/Coder fixes
-> scoped verification
```

Stop on the first condition:

1. no meaningful new differences survive the filter;
2. 3 rounds completed;
3. operator stops.

If a polish round regresses already-approved behavior or clearly degrades the accepted result, revert that round instead of starting an open-ended repair loop.

## 3. SEO / Technical Pass

Use:

```text
technical-reviewer
```

It checks final implementation against:

```text
PRODUCT.md
content/strategy.md
content/page.md
```

Typical scope:

- metadata/canonical;
- headings/semantic HTML;
- internal links;
- Open Graph;
- alt/images;
- robots/sitemap;
- structured data when needed;
- accessibility;
- performance;
- console/layout/interaction errors;
- CTA/download/forms behavior.

Reviewer does not edit application source.

Coder fixes findings.

Follow-up verification is scoped.

## 4. Final AI gate

After required findings are resolved:

```text
gates.final_ai_review = approved
```

Do not mark approved merely because reviewers returned.

## 5. Final Human Review

Tell the operator to walk the live site as a user on desktop and mobile.

The operator is the final product/design gate.

Only after explicit operator approval may the project be considered ready.

## 6. Deploy / release

Never deploy automatically.

If the operator explicitly requests release/deploy, follow project-specific release instructions and safety/authorization rules.

"Site is ready" does not mean "deploy is authorized."

## 7. Retrospective

Keep it short.

Capture only reusable lessons:

- repeated failures worth updating AGENTS/skills;
- workflow improvements;
- strong reusable visual references/patterns.

If repeated production patterns genuinely exist, Impeccable `extract` may be considered here.

Do not turn retrospective into a large report.

## State transition

When final human review is approved and release work is either completed or intentionally not requested:

```text
stage = done
```

Record any remaining non-blocking notes in `blockers` only if they truly remain unresolved; otherwise clear them.
