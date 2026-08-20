# Operator Runbook

Назначение: короткая практическая инструкция для оператора website workflow.

`WORKFLOW.md` остается canonical описанием этапов, gates и ownership.
Этот файл нужен только для удобного запуска нужного окна и начала взаимодействия с агентом.

Если `OPERATOR_RUNBOOK.md` расходится с `WORKFLOW.md`, приоритет у `WORKFLOW.md`.

## Как пользоваться

Для каждого этапа:

1. открой указанное окно Codex;
2. вставь короткий launch prompt из этого файла;
3. агент сначала читает уже существующий project context;
4. агент задает только недостающие operator-вопросы;
5. отвечай одним свободным сообщением, в том числе голосом;
6. агент нормализует ответ и продолжает stage;
7. возвращайся в Website Orchestrator только на крупных gates, указанных в `WORKFLOW.md`.

Не нужно вручную запускать `seo-researcher`, `reference-researcher`, `visual-reviewer` или `technical-reviewer`.
Их вызывают соответствующие parent roles.

Общий UX вопросов определяется:

```text
.agents/OPERATOR_INTAKE.md
```

---

## 0. Start Project

**Window:** Website Orchestrator
**Skill:** `$website-workflow`

Launch prompt:

```text
$website-workflow

Start or resume this website project.
Read AGENTS.md, WORKFLOW.md, existing project files and workflow state first.

If this is a new project, begin Stage 0.
Follow .agents/OPERATOR_INTAKE.md and ask me one compact batch only for project inputs that are still missing.
I will answer free-form, usually by voice.
```

Ожидаемый interaction:

```text
agent reads repo
-> shows what is already known
-> asks max 5 compact questions
-> operator answers once
-> agent normalizes inputs
-> PRODUCT.md / state are prepared
-> agent routes to Stage 1A + 1B
```

---

## 1A. Strategy / SEO / Funnel

**Window:** Strategist
**Skill:** `$strategist`
**Mode:** `strategy`

Launch prompt:

```text
$strategist
mode: strategy

Start Stage 1A for this project.
Read PRODUCT.md, project references and existing context first.

Follow .agents/OPERATOR_INTAKE.md.
Ask only for missing operator decisions that materially affect strategy, SEO or funnel.
I will answer in one free-form voice message.
Then proceed with the research and strategy.
```

Обычно от оператора нужно не больше 0-3 решений.

Не подготавливай вручную keyword list или competitor spreadsheet, если агент может исследовать это сам.

---

## 1B. Design Context

**Window:** Design Context
**Skill:** `$design-context`

Launch prompt:

```text
$design-context

Start Stage 1B.
Read PRODUCT.md and inspect references/, existing UI and brand materials first.

Follow .agents/OPERATOR_INTAKE.md.
First tell me briefly what references/materials you actually found.
Then ask only for missing reference roles, priorities, fidelity or material visual context that cannot be derived from the project.
I will answer free-form by voice.
```

Обычно от оператора нужно 0-3 решения.

Если референсы уже имеют ясные роли, агент не должен спрашивать их повторно.

---

## Joint Gate after 1A + 1B

**Window:** Website Orchestrator

Когда `content/strategy.md` и `DESIGN.md` готовы:

```text
$website-workflow

Stage 1A and Stage 1B are ready.
Resume from current state and tell me exactly what I need to review or decide for the joint gate.
Do not redo specialist work.
```

Оператор одним проходом проверяет Strategy + Design Context.

---

## 2. Content Wireframe

**Window:** вернуться в то же окно Strategist
**Skill:** `$strategist`
**Mode:** `content`

Launch prompt:

```text
$strategist
mode: content

Continue with Stage 2.
Read the approved content/strategy.md, DESIGN.md and existing project references first.

Ask me once whether I have any additional copy, tone or content-structure references.
Then work through the page one section at a time.
For each important section, show the required variants and ask only for my choice, combination or focused correction.
```

После initial reference question это уже не intake-анкета.

Нормальный цикл:

```text
agent shows variants
-> operator chooses / combines / corrects
-> agent saves approved block to content/page.md
-> next block
```

---

## Gate after Content

**Window:** Website Orchestrator

```text
$website-workflow

content/page.md is complete.
Resume from current state and check readiness for the content gate.
Tell me only what still needs my decision before Visual Direction.
```

---

## 3. Visual Direction

**Window:** Art Director
**Skill:** `$art-director`
**Mode:** `visual-direction`

Launch prompt:

```text
$art-director
mode: visual-direction

Start Visual Direction.
Read all approved canonical artifacts and project references first.

Follow .agents/OPERATOR_INTAKE.md.
Ask only for missing reference or fidelity decisions that materially affect the visual direction.
Then create the required rendered directions.
```

Обычно от оператора нужно 0-2 initial decisions, затем выбор одного direction или комбинации.

---

## Gate after Visual Direction

**Window:** Website Orchestrator

```text
$website-workflow

Visual Direction is approved.
Resume from current state, record the gate and route me into the Section Loop.
```

---

## 4A. Design Next Section

**Window:** то же окно Art Director
**Skill:** `$art-director`
**Mode:** `section`

Launch prompt:

```text
$art-director
mode: section

Continue with the next unapproved section.
Read its approved copy, DESIGN.md, approved visual direction and existing references first.

If a specific reference or CLOSE / ADAPT / INSPIRE decision for this section is not already known, ask me that one decision.
Otherwise proceed without an intake questionnaire.
```

Если реального block reference нет, Art Director сам запускает `reference-researcher`.

После выбора composition Art Director сам формулирует конкретные asset/responsive requirements.

---

## 4B. Implement Approved Section

**Window:** Frontend Coder
**Skill:** `$frontend-coder`

Launch prompt:

```text
$frontend-coder

Implement the currently approved section.
Read the Art Director handoff, approved source and canonical project files first.

If all required inputs and assets are available, proceed without questions.
Ask me only if there is a real operator blocker that cannot be resolved from the project or by the owning specialist.
```

Coder сам:

```text
implements
-> self-checks
-> invokes visual-reviewer
-> fixes CODER findings
-> requests scoped re-review when needed
-> presents live block to operator
```

Оператор не управляет reviewer вручную.

---

## 4C. Approve Live Section

После Coder handoff:

```text
проверить блок в браузере
-> approve
или
-> дать одну пачку точечных правок
```

После approve вернуться в Art Director window и снова использовать prompt `4A`.

Не возвращаться в Orchestrator после каждого блока.

---

## 5. Final Workflow

Когда все sections approved:

**Window:** Website Orchestrator

```text
$website-workflow

Resume the project from current state.
All sections are implemented and individually approved.

If the Section Loop completion conditions are satisfied, continue with the final workflow.
Route the required fresh reviewers automatically.
Ask me only when a real human decision, approval or release authorization is required.
```

Orchestrator сам маршрутизирует:

```text
fresh visual-reviewer
-> optional POLISH if enabled
-> technical-reviewer
-> final AI gate
-> final human review
```

---

## 6. Release

Фраза:

```text
The site is ready.
```

не является разрешением на deploy.

Если публикация нужна, оператор отдельно пишет прямую команду, например:

```text
Deploy the approved production version to the existing Vercel project.
```

Release выполняется по `AGENTS.md` и `WORKFLOW.md`.

---

## Быстрый resume после закрытия окна

### Orchestrator

```text
$website-workflow

Resume this project from .website/state.md and current canonical artifacts.
Tell me the current stage, what is ready, what needs my decision and the next action.
```

### Strategist

```text
$strategist
mode: <strategy|content>

Resume the current Strategist stage from canonical project artifacts.
Read existing work before asking me anything.
```

### Design Context

```text
$design-context

Resume Stage 1B from existing project artifacts.
Read current references and DESIGN.md state before asking me anything.
```

### Art Director

```text
$art-director
mode: <visual-direction|section>

Resume from approved design artifacts and current canonical project context.
Do not reopen already approved decisions.
```

### Frontend Coder

```text
$frontend-coder

Resume the current approved section implementation.
Read the existing handoff, code and reviewer state before asking me anything.
```
