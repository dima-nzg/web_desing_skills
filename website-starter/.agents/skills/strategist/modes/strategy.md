# Strategist Mode - Strategy

## Goal

Produce a reliable strategic, SEO, funnel, and page-structure foundation in one autonomous research pass.

Primary artifact:

```text
content/strategy.md
```

This stage runs in parallel with Design Context.

## Required inputs

At minimum:

```text
PRODUCT.md
```

Also inspect when available:

```text
references/
existing site/product
known competitors supplied by operator
```

If `PRODUCT.md` is missing, return `BLOCKED` and route back to Stage 0.

## SEO mode

Read the project setting supplied by Orchestrator:

```text
FREE
SEO VERIFIED
```

### FREE

Use:

- Web Search;
- browser;
- competitor pages;
- live SERP evidence where available;
- model synthesis.

Never output invented search volume, CPC, difficulty, or competition numbers.

Qualitative demand/intention conclusions must be labeled qualitative.

### SEO VERIFIED

Use everything from FREE plus the configured DataForSEO capability.

Only metrics returned by the real tool are considered verified.

Expected capability categories:

```text
keyword expansion / ideas
historical keyword metrics
SERP data for target location/language
```

If DataForSEO is unavailable or fails materially:

1. do not fabricate metrics;
2. report the tooling gap;
3. ask the operator whether to continue in FREE or fix VERIFIED tooling.

Do not silently downgrade.

## Research plan

The Strategist owns the plan and synthesis.

Delegate read-heavy evidence gathering to `seo-researcher` when useful.

A normal pass covers:

### 1. Product and competitor scan

- understand the product and conversion goal;
- inspect operator-supplied references/competitors;
- find relevant direct competitors;
- identify actual search competitors for the intended queries;
- note positioning, claims, proof, CTA, structure, and terminology.

Do not assume the operator's visual reference is also the strongest SEO competitor.

### 2. Keyword/topic discovery

Build enough evidence to identify:

- primary topic/keyword cluster for the main page;
- supporting topics;
- transactional/download-oriented queries when relevant;
- user questions/objections;
- topics better suited to separate SEO pages.

Do not optimize for list size.

Hundreds of weak keywords are less useful than a coherent validated cluster.

### 3. SERP validation

For the important clusters, verify:

- what page type ranks;
- actual search intent;
- recurring content themes;
- real search competitors;
- mismatches between attractive keywords and the product's offer.

Search volume never overrides incompatible intent.

### 4. Funnel

Define the information sequence needed to move the visitor from arrival to the primary action:

- what they must understand first;
- what keeps attention;
- what proof is needed;
- what objections must be removed;
- where CTA belongs;
- what should make the final action feel justified.

### 5. Page skeleton

Recommend the section order based on this project.

For each section define:

```text
purpose
core message
content scope
CTA if needed
proof if needed
visual/content asset requirement
SEO/topic responsibility where relevant
```

The skeleton is a strategic recommendation, not final copy.

## DEEP setting

If `deep = true`:

- broaden competitor/SERP evidence where ambiguity remains;
- test plausible competing keyword directions;
- inspect more edge cases in the funnel;
- surface high-impact strategic contradictions.

Do not make every research branch exhaustive.

Depth is spent where the decision is uncertain or materially affects the site.

## Artifact format

Write `content/strategy.md` with these sections:

```text
# Strategy

## 1. Product / audience / conversion
## 2. Competitor findings
## 3. SEO intent and keyword/topic clusters
## 4. SERP conclusions
## 5. Funnel
## 6. Recommended page structure
## 7. Section briefs
## 8. Separate SEO page opportunities
## 9. Evidence gaps / assumptions
## 10. Research mode and key sources
```

### Keyword section

Prefer compact clusters over raw dumps.

For SEO VERIFIED, include verified metrics only where they help decisions.

Clearly distinguish:

```text
verified metric
qualitative observation
inference
```

### Sources

Include direct URLs for the most important external sources used to justify decisions.

Do not turn the artifact into a bibliography.

## Completion

Before declaring Stage 1A ready:

- research mode is explicit;
- primary search intent is clear;
- main keyword/topic cluster is defensible;
- important SERP mismatches are surfaced;
- funnel is coherent;
- every proposed section has a purpose;
- unsupported assumptions are listed.

Return a concise summary for the operator.

Do not ask for Stage 1A approval separately if the workflow expects the joint Strategy + Design Context review.
