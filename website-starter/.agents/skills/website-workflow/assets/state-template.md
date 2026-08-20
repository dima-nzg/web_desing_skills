# Website Workflow State

> Managed by `website-workflow`. Do not use this file as a manual task tracker.

```yaml
schema_version: 1
updated_at: null

stage: init

settings:
  seo_mode: free
  deep: false
  polish: false

tooling:
  impeccable: unknown
  mobbin_mcp: unknown
  dataforseo: unknown

artifacts:
  product: pending
  strategy: pending
  design: pending
  page: pending
  visual_direction: pending

gates:
  strategy_design_review: pending
  content: pending
  visual_direction: pending
  final_ai_review: pending

section_loop:
  status: pending

blockers: []
```

## Allowed values

`stage`:

```text
init
strategy_design
content
visual_direction
section_loop
final
done
```

Artifact statuses:

```text
pending
ready
blocked
```

Gate statuses:

```text
pending
approved
blocked
```

`section_loop.status`:

```text
pending
active
done
blocked
```

Tooling statuses:

```text
unknown
disabled
ready
blocked
```

`settings.seo_mode`:

```text
free
verified
```

## Update rule

Only the Website Orchestrator edits this file during normal runtime.

Keep state small. Fine-grained section progress belongs in canonical artifacts and production code.
