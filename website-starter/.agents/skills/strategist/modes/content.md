# Strategist Mode - Content

## Goal

Turn approved strategy into practically final website content, block by block, before Art Direction.

Primary artifact:

```text
content/page.md
```

This is interactive by design.

The operator should make meaningful content choices now so the project does not repeatedly reopen copy during design and implementation.

## Required inputs

```text
PRODUCT.md
content/strategy.md
```

Also read when available/useful:

```text
DESIGN.md
references/
```

`DESIGN.md` is context for realistic content density and tone fit, not permission to do design work.

If `content/strategy.md` is not approved/ready, return `BLOCKED`.

## Before the first section

Ask once:

```text
Do we have additional references for copy, tone, content structure, or competitor sections to follow?
```

The operator may supply:

- sites whose writing style is useful;
- competitor sections worth adapting;
- tone examples;
- specific ideas to preserve.

Do not repeat this question for every section.

## Work sequentially

Process one section at a time in the approved page order.

For each important section, present 2-3 **meaningfully different** content approaches.

They should differ in message strategy or emphasis, not merely synonyms.

Each variant includes:

```text
Idea
Heading
Subheading if needed
Body / supporting copy
CTA if needed
Proof/supporting content if needed
Visual/content asset requirement
Pitch:
  marketing logic
  funnel role
  SEO/search-intent role
  key tradeoff
```

Explain the pitch in plain language.

## Operator choice

The operator may:

- choose one variant;
- combine elements;
- request a focused correction.

After approval, immediately persist the chosen section into `content/page.md`.

Do not wait until the end of the whole page to save all decisions.

Then continue to the next section.

## Simple sections

For a simple derivative section such as a compact CTA or straightforward FAQ intro, 2 strong variants may be enough.

Do not force a third weak variant merely to satisfy a number.

## Copy quality

The content must simultaneously:

- explain the product clearly;
- move the visitor confidently toward the primary action;
- be persuasive without empty hype;
- naturally cover relevant SEO topics and intent;
- use real facts and proof;
- match the approved tone/reference direction;
- have realistic final-design length.

Avoid:

- keyword stuffing;
- generic "revolutionary / seamless / next-generation" filler;
- fake proof;
- vague claims that cannot be defended;
- SEO paragraphs that damage the funnel.

## SEO behavior

Use the approved strategy.

Do not restart broad keyword research section by section.

Targeted research is allowed only when:

- a factual claim needs verification;
- a section exposes a real intent/content gap;
- the operator introduces a new competing direction.

If new research materially changes the approved strategy, surface the conflict before rewriting the page architecture.

## Funnel continuity

Before each new section, consider what the previous approved section already established.

Do not repeat the same promise in different words.

Each section should advance at least one of:

```text
understanding
desire
proof
objection removal
conversion
SEO coverage that also serves the reader
```

## Asset requirements

For each approved section, record the intended content/visual requirement at a useful level:

```text
product screenshot
video
animation
photo
diagram
real data/proof
none
```

Do not invent the actual asset.

Exact production asset requirements may be refined later by Art Director.

## Artifact format

Maintain:

```text
# Page Content

## Page flow
<approved order>

## 01. <Section name>
Purpose:
Funnel role:
SEO/topic role:
Heading:
Subheading:
Body:
CTA:
Proof/support:
Visual/content requirement:
Notes:

## 02. ...
```

Do not keep rejected variants in the canonical final file unless the operator explicitly wants them preserved.

## Near-final rule

After Stage 2:

- headings;
- main claims;
- CTA logic;
- section order;
- core body copy

are treated as practically final.

Later wording changes should be small.

If Art Director/Coder later wants a substantive copy change, update `content/page.md` first through the operator/Strategist, then implementation.

## Completion

When all sections are approved:

1. read `content/page.md` end to end;
2. remove repetition;
3. verify funnel continuity;
4. verify SEO coverage remains natural;
5. verify no unsupported claims remain;
6. make only non-substantive consistency edits;
7. ask the operator for Gate 1 content approval through the workflow.

Do not proceed into Art Direction yourself.
