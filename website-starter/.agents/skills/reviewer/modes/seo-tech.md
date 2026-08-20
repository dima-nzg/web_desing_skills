# Reviewer Mode - SEO / Technical

## Goal

Review the final implemented page for technical correctness, final SEO implementation, accessibility, performance signals, and conversion-breaking bugs.

This is not new keyword research.

Do not use DataForSEO unless the caller explicitly requests a new external SEO investigation.

## Required inputs

```text
PRODUCT.md
content/strategy.md
content/page.md
final application code
runnable page or build/test commands
```

If critical inputs are missing, return `BLOCKED`.

## Before checks

Record:

```text
git status
```

The technical reviewer may run commands that create temporary build/cache artifacts, but must not edit application source.

If tracked source changes already exist, note them before running checks so they are not attributed to the review.

## SEO implementation

Check as applicable:

- title;
- meta description;
- canonical;
- one coherent H1 strategy;
- H1-H6 hierarchy;
- semantic HTML;
- internal links;
- Open Graph;
- image alt behavior;
- robots;
- sitemap;
- structured data when strategy/product actually requires it.

Judge against `content/strategy.md` and `content/page.md`.

Do not invent new keyword targets.

## Functional / technical

Check as available:

- build;
- lint;
- tests;
- console errors;
- broken links;
- CTA and download flows;
- forms;
- menus;
- obvious interaction failures;
- responsive/layout errors not already caught;
- accessibility failures;
- major performance regressions or obviously avoidable heavy behavior.

Use project-provided commands before inventing new tooling.

Do not install packages merely to make the review look comprehensive.

## Source-write guard

Never:

- edit application files;
- apply formatter fixes;
- patch metadata;
- fix failing tests.

Return findings to Coder.

## After checks

Record `git status` again.

Report unexpected tracked changes or generated artifacts.

Temporary review artifacts are not product findings unless they indicate a real project problem.

## Finding standard

Prefer correctness and material impact over generic best-practice commentary.

No finding for a technically optional optimization unless it materially affects this page.
