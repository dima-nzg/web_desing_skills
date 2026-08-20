# Section Review Handoff

Use this protocol when sending one implemented section to `visual-reviewer`.

## First review

Provide:

```text
MODE: section

SECTION:
<name>

LIVE:
<route / URL / how to run>

VIEWPORTS:
<desktop/mobile targets>

APPROVED SOURCE:
<path to approved mockup/source>

DESIGN:
DESIGN.md

CONTENT:
<relevant heading in content/page.md>

RESPONSIVE INTENT:
<path/text if non-obvious>

NEIGHBOR CONTEXT:
<previous approved/implemented sections if useful>
```

Tell the reviewer to invoke:

```text
$reviewer
mode: section
```

Do not paste unrelated strategy/design history.

## Re-review after fixes

Provide:

```text
MODE: section re-review

ORIGINAL FINDINGS:
[R01] ...
[R02] ...

FIX DIFF:
<git diff limited to fix when practical>

LIVE:
<route / URL>

VIEWPORTS:
<affected viewport>
```

Instruction:

```text
Verify the listed findings only.
Flag a new finding only if it is a direct regression caused by these fixes.
Do not restart a full section review.
```

## Reviewer output

Expect:

```text
MODE:
VERDICT:
FINDINGS:
BLOCKERS:
REVIEWED:
```

Route findings by owner.

Never ask reviewer to implement fixes.
