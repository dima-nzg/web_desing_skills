# Operator Intake Protocol

This is a shared operator-question UX protocol for the main website skills. It is not a runtime role, workflow stage, gate, or artifact owner.

`WORKFLOW.md` remains canonical for stage order, gates, roles, and outputs. This protocol only governs how an operator-facing role gathers missing input.

## Found-first intake

Before asking the operator anything:

1. read the canonical artifacts and project context available to the current role;
2. inspect existing references, state, handoffs, and prior decisions relevant to the current stage;
3. briefly report what is already known;
4. ask only for missing decisions that the role cannot derive, research, or decide within its own authority.

Do not ask the operator to repeat facts already present in the project. Do not turn a checklist into a form.

## One compact batch

Group related missing fields into one compact initial batch within the role budget below. A top-level numbered item may contain closely related subparts when they can be answered together naturally.

Questions should be easy to answer in one free-form or voice message. After the answer:

1. normalize it into the project's terms and artifacts;
2. state the interpreted decisions briefly;
3. proceed without a second generic intake batch;
4. ask a follow-up only when a material ambiguity or genuine blocker remains.

Do not require the operator to answer in a template. Do not ask for research facts that the role can investigate independently.

## Question budgets

```text
Stage 0 Orchestrator          maximum 5 initial questions
Strategist / strategy        maximum 3 initial questions
Design Context               maximum 3 initial questions
Strategist / content         1 initial references/tone question
Art Director / direction     maximum 2 initial questions
Art Director / section       normally 1 reference/fidelity decision
Frontend Coder               normally 0 questions; blocker only
```

These are maximums, not targets. Ask zero questions when nothing material is missing.

Operator selection among prepared content or design variants is normal gate interaction, not intake. A precise request for a required real asset after design approval is a blocker request, not generic intake.

## Resume behavior

On resume or after compaction, read the role's canonical artifacts and current handoff/state before asking anything. Continue from recorded decisions and unresolved items; never restart intake from zero merely because the window or session is new.

If canonical sources conflict, report the conflict and ask only for the decision needed to resolve it. File existence alone is not approval.

## Routing boundary

Reducing questions does not permit role drift. Route work or decisions owned by another specialist instead of asking the operator for an implementation preference or performing the neighboring role yourself.

In the normal operator flow, the operator does not manually launch research or reviewer subagents. Their parent roles invoke `seo-researcher`, `reference-researcher`, `visual-reviewer`, and `technical-reviewer` when required by the workflow.
