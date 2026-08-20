# Phase 40 - Section Loop

Covers `WORKFLOW.md` Stage 4.

## Goal

Let Art Director + Frontend Coder repeat the approved section cycle until the whole page is built and approved block by block.

The orchestrator tracks only:

```text
section_loop.status = active | done
```

Do not mirror every section status into `.website/state.md`.

## Runtime windows

Keep alive:

```text
Art Director
Frontend Coder
```

## Per-section loop

Operational sequence:

```text
reference / targeted research
-> 2-3 mockups for important/non-obvious sections
-> operator choice
-> asset + responsive check
-> production implementation
-> independent section review
-> targeted refinement
-> operator live-block approve
-> next section
```

Simple derivative sections may start with one strong variant and expand only if rejected.

## Asset rule

If the approved design requires a real screenshot, video, animation, photo, or other real asset and it is unavailable, the Art Director/Coder must ask the operator for it before implementation.

Do not silently replace missing real assets with generic AI imagery, random icons, or simplified placeholders.

## Reviewer rule

Frontend Coder owns the persistent section-reviewer relationship.

Preferred custom agent:

```text
visual-reviewer
```

Reviewer must remain independent and must not fix application code.

If continuation of the reviewer thread is unavailable or clearly drifting, use a fresh visual reviewer with the same canonical inputs.

After a fix, review only:

- the original findings;
- the fix diff;
- regressions caused by that fix.

Do not restart an unconstrained full review of the section unless there is a concrete reason.

## Impeccable

During implementation:

- hooks may run continuously;
- targeted refinement commands are used only for a known issue;
- `polish` is only for a block whose composition/content/implementation are already settled.

After several representative production sections exist, Art Director may run `/impeccable document` once to synchronize `DESIGN.md` with the real UI.

That synchronization must be reviewed against approved UI and must not become a redesign.

## When to return to Orchestrator

Return when the operator says the page's sections are all implemented and individually approved, or when a cross-stage blocker requires changing Strategy, Content, or Visual Direction.

## Completion check

Before marking complete, verify:

- `design/approved-sections/` contains the approved visual sources needed for the built page;
- the production page is runnable;
- the operator confirms all sections passed live-block approval.

Do not re-review every section inside the orchestrator.

## State transition

After operator confirmation:

```text
section_loop.status = done
stage = final
```

Then proceed to the final phase.
