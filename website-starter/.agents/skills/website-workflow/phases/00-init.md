# Phase 00 - Init

Covers `WORKFLOW.md` Stage 0 and optional tooling setup.

## Goal

Initialize project context and major workflow state, then route the operator into the parallel Strategy and Design Context work.

## Entry

If `.website/state.md` does not exist:

1. copy the structure from `../assets/state-template.md`;
2. set `stage: init`;
3. record currently known tooling/settings.

Do not create empty `PRODUCT.md` or `DESIGN.md` in advance.

## Collect project inputs

Collect only information required to start:

- product;
- target user;
- primary conversion/action;
- project type;
- project-specific characteristics;
- existing site/product if any;
- main visual references if any;
- brand materials if any;
- existing real screenshots, video, photos, animations, or other assets;
- key constraints;
- technical stack;
- target language and geography;
- importance of SEO.

Do not ask the operator to manually prepare keyword lists, design tokens, or a complete asset pack.

## Optional tooling

### Impeccable

Ask whether Impeccable is used for this project.

If yes and it is not installed project-locally, instruct the operator to install it from the repo root:

```bash
npx impeccable install --scope=project
```

After installation, Codex may need reload/restart and project hooks may need approval.

For product context:

- instruct the operator to run `/impeccable init`;
- use the collected project inputs for the answers;
- validate that `PRODUCT.md` exists afterward;
- if Impeccable offers to create/document the design immediately, defer that to Stage 1B.

If Impeccable is not used, create `PRODUCT.md` directly from the collected Stage 0 inputs.

### Mobbin MCP

Record whether Mobbin MCP is available.

Its absence does not block the workflow.

### DataForSEO

Ask the operator which Strategy mode to use:

```text
FREE
SEO VERIFIED
```

If `SEO VERIFIED`, verify that the DataForSEO credentials/tooling are available before routing to Strategist.

If unavailable, do not pretend verification exists. Ask the operator whether to switch to FREE or fix tooling.

## PRODUCT.md boundary

`PRODUCT.md` is created in this phase.

After Stage 0, treat it as project context.

Do not rewrite it later unless the operator changes project inputs or positioning.

## State transition

Before leaving:

- `artifacts.product = ready`
- record tooling status;
- record `settings.seo_mode`, `settings.deep`, `settings.polish`;
- set `stage = strategy_design`.

Then tell the operator to open two specialist windows:

```text
Window Strategist:
$strategist

Window Design Context:
$design-context
```

These Stage 1A and 1B tracks may run in parallel.
