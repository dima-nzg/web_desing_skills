# Phase 30 - Visual Direction

Covers `WORKFLOW.md` Stage 3.

## Goal

Have Art Director establish one approved visual direction using real page content before full section production.

## Specialist

Use:

```text
$art-director
```

Prefer one Art Director window that remains open through all later section design work.

## Required inputs

Verify these exist before routing:

```text
PRODUCT.md
DESIGN.md
content/page.md
references/
```

## Operator control

For any representative block that has a direct reference, Art Director asks:

```text
CLOSE
ADAPT
INSPIRE
```

If the needed block does not exist in the provided references, Art Director uses targeted reference research before designing from scratch.

## Expected result

Art Director creates 2-3 genuinely different rendered visual directions using representative sections.

The operator selects one direction or combines parts.

Approved representative sections do not need to be redesigned again in the Section Loop.

## Canonical artifacts

Expected:

```text
design/approved-direction/
```

and, for representative sections already approved as final compositions:

```text
design/approved-sections/
```

Art Director may update `DESIGN.md` with newly approved system-level visual principles.

## Human gate

Gate:

```text
visual_direction
```

Approve only after explicit operator choice.

## State transition

After approval:

```text
artifacts.visual_direction = ready
gates.visual_direction = approved
section_loop.status = active
stage = section_loop
```

Tell the operator to keep the Art Director window and open/prepare the Frontend Coder window:

```text
$frontend-coder
```

The orchestrator does not need to be revisited after every section.
