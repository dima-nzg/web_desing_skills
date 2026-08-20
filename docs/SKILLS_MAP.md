# Skills Map v1.1

Назначение: карта skills, custom agents, рабочих окон и контрактов для website workflow.

Статус: архитектурная спецификация перед созданием реальных `SKILL.md` и `.toml`.

## 1. Базовый принцип

Website workflow существует только внутри website-project.

```text
website-starter/
├─ AGENTS.md
├─ WORKFLOW.md
├─ OPERATOR_RUNBOOK.md
├─ .agents/
│  ├─ OPERATOR_INTAKE.md
│  └─ skills/
├─ .codex/
│  ├─ agents/
│  └─ config.toml
├─ references/
├─ content/
└─ design/
```

Website-specific skills и agents не устанавливаются глобально.

`PRODUCT.md`, `DESIGN.md`, `content/strategy.md`, `content/page.md` и approved design artifacts создаются уже по ходу workflow.

---

## 2. Маленький state для Orchestrator

При инициализации проекта `website-workflow` создает:

```text
.website/state.md
```

Это не документ для ручного заполнения оператором. Его автоматически ведет только Orchestrator.

State хранит **только крупное состояние workflow**, а не прогресс каждого section. Иначе файл будет устаревать, потому что во время Section Loop оператор работает напрямую с Art Director и Coder и не обязан возвращаться к Orchestrator после каждого блока.

Минимальное содержимое:

```yaml
stage: init

settings:
  seo_mode: free
  deep: false
  polish: false

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

Допустимые значения `settings.seo_mode`:

```text
free
verified
```

Fine-grained source of truth для секций:

```text
content/page.md
design/approved-sections/
реальный production code
```

Когда Orchestrator снова получает управление, он сверяет эти artifacts и обновляет major state.

Цель: после закрытия окна или compaction Orchestrator восстанавливает маршрут проекта из одного маленького файла, не пытаясь вести параллельный task tracker.

## 2.1 Shared operator UX protocol

`OPERATOR_RUNBOOK.md` содержит короткие copy/paste launch prompts для правильных окон и explicit skill modes. Он не заменяет canonical порядок stages и gates из `WORKFLOW.md`.

`.agents/OPERATOR_INTAKE.md` — общий voice-friendly protocol вопросов оператору, а не runtime role, agent, stage или artifact owner.

Его используют все operator-facing main skills:

```text
website-workflow
strategist
design-context
art-director
frontend-coder
```

Каждая роль сначала читает доступные canonical artifacts и project context, сообщает уже найденное, затем задает одной компактной пачкой только недостающие вопросы в пределах своего budget. Resume не перезапускает intake с нуля.

Research subagents и reviewers по-прежнему запускаются их parent roles; operator runbook не превращает их в ручные рабочие окна и не меняет isolation/ownership architecture.


---

# 3. Рабочие окна

Каждое specialist-окно запускается **явным invocation нужного skill**, а не общей фразой вроде «продолжи сайт».

Пример:

```text
$strategist
$design-context
$art-director
$frontend-coder
```

Descriptions у role-skills должны быть узкими и явно говорить, когда skill **не** должен активироваться. Это снижает риск implicit cross-role activation, потому что Codex может выбирать skill по его `description`.


## Window 1 - Website Orchestrator

Живет весь проект.

Skill:

```text
website-workflow
```

Задача:

- держать stage и gates;
- обновлять `.website/state.md`;
- говорить оператору, какое окно/роль нужна следующей;
- проверять наличие необходимых artifacts;
- передавать настройки specialist-ролям;
- не заниматься тяжелым research, дизайном или production-кодом.

Orchestrator возвращается в фокус на крупных переходах между этапами. Не нужно возвращаться к нему после каждой мелкой правки блока.

---

## Window 2 - Strategist

Живет минимум до завершения Stage 2.

Skill:

```text
strategist
```

Использование:

```text
Stage 1A -> Strategy / SEO / Funnel
пауза, пока параллельно идет Design Context
Stage 2  -> Content Wireframe
```

Используется то же окно, чтобы Strategist сохранял контекст SEO, funnel, конкурентов и принятых content-решений.

---

## Window 3 - Design Context

Одноразовое специализированное окно.

Skill:

```text
design-context
```

Использование:

```text
Stage 1B -> DESIGN.md
```

После завершения Stage 1B окно обычно закрывается.

---

## Window 4 - Art Director

Живет от Visual Direction до утверждения последнего section design.

Skill:

```text
art-director
```

Использование:

```text
Stage 3 -> Visual Direction
Stage 4 -> design части Section Loop
```

Окно сохраняется, чтобы не терять visual memory и approved patterns страницы.

---

## Window 5 - Frontend Coder

Живет весь Section Loop.

Skill:

```text
frontend-coder
```

Использование:

```text
approved section
-> implementation
-> refinement
-> следующий approved section
```

Окно сохраняется, чтобы Coder не переизобретал компоненты, CSS conventions и технические решения.

---

# 4. Runtime skills

| Skill | Основная роль | Главное окно | Пишет production code | Spawn subagents |
|---|---|---|---:|---:|
| `website-workflow` | orchestration / gates / state | Orchestrator | нет | только final reviewer при необходимости |
| `strategist` | research, SEO, funnel, copy | Strategist | нет | `seo-researcher` |
| `design-context` | initial design system | Design Context | нет | нет в v1 |
| `art-director` | visual direction + section design | Art Director | только exploration/mockup code | `reference-researcher` |
| `frontend-coder` | production implementation + refinement | Frontend Coder | да | persistent `reviewer` |
| `reviewer` | independent review | только subagent | никогда | нет |

---

# 5. Skill contracts

## 5.1 `website-workflow`

### Owns

```text
.website/state.md
```

Stage 0 exception:

```text
PRODUCT.md
```

Orchestrator отвечает за первичное создание `PRODUCT.md` из исходных данных оператора:

- через `/impeccable init`, если Impeccable используется;
- либо прямым созданием по Stage 0 workflow.

После завершения Stage 0 `PRODUCT.md` считается project context и не переписывается Orchestrator без явного изменения вводных оператором.

### Reads

```text
WORKFLOW.md
AGENTS.md
.website/state.md
```

На gates проверяет наличие/статус:

```text
PRODUCT.md
content/strategy.md
DESIGN.md
content/page.md
design/approved-direction/
design/approved-sections/
```

Не обязан постоянно читать содержимое всех этих файлов целиком.

### Writes

```text
.website/state.md
PRODUCT.md   только на Stage 0 или при явном изменении project inputs
```

Не редактирует:

```text
DESIGN.md
content/*
production UI
```

### Tools

Минимальный surface:

```text
filesystem
shell для status/validation при необходимости
subagent dispatch
```

Не нужны:

```text
DataForSEO
Mobbin
design search
Impeccable refinement commands
```

### Internal structure

По принципу lazy loading:

```text
website-workflow/
├─ SKILL.md
└─ phases/
   ├─ 00-init.md
   ├─ 10-strategy-design-context.md
   ├─ 20-content.md
   ├─ 30-visual-direction.md
   ├─ 40-section-loop.md
   └─ 50-final.md
```

`SKILL.md` содержит только маршрут, gates и правила переключения стадий.

Конкретный `phases/*.md` читается только при входе в эту фазу.

### Relation to `WORKFLOW.md`

`WORKFLOW.md` — human-facing canonical order процесса.

`website-workflow` — его executable implementation.

Они не должны тихо расходиться:

- изменение порядка/gates сначала утверждается в `WORKFLOW.md`;
- Skill Builder обновляет соответствующие phase files в том же commit;
- если Orchestrator обнаружил конфликт между `WORKFLOW.md` и skill logic, он останавливается и сообщает об этом вместо выбора одной версии «по смыслу».

---

## 5.2 `strategist`

### Owns

```text
content/strategy.md
content/page.md
```

### Reads

Stage 1A:

```text
PRODUCT.md
references/
```

Stage 2 дополнительно:

```text
DESIGN.md
content/strategy.md
```

### Tools

```text
Web Search
browser
DataForSEO tool/CLI только в SEO VERIFIED
```

Не нужны:

```text
Mobbin
Impeccable design commands
production-code tools
```

### Subagent

Может спавнить:

```text
seo-researcher
```

Только для read-heavy:

```text
competitor research
SERP research
keyword evidence
```

Strategist остается владельцем анализа, clustering, funnel и финальных решений.

### Content ownership after Stage 2

`content/page.md` остается canonical source of copy.

После Stage 2:

- Art Director и Coder могут предложить сокращение/изменение текста;
- они не меняют copy самостоятельно;
- оператор или Strategist сначала обновляет `content/page.md`;
- только затем изменение переносится в implementation.

Это предотвращает расхождение между approved content и live site.

### Human gates

Stage 1A:

```text
один joint review вместе с DESIGN.md
```

Stage 2:

```text
2-3 content variants для каждого важного блока
operator selects / combines
```

---

## 5.3 `design-context`

### Owns

```text
DESIGN.md
.impeccable/design.json   если Impeccable установлен
```

### Reads

```text
PRODUCT.md
references/
existing product UI/assets
```

### Tools

```text
browser / screenshots
Web при необходимости для открытия предоставленных references
Impeccable:
  document --seed
  document
  doctor при проблемах
```

Не использовать Mobbin как источник случайного нового style direction.

### Responsibilities

1. Извлечь реальный visual DNA из references.
2. Сообщить оператору обо всех существенных пробелах.
3. Только затем использовать `document --seed`.
4. Проверить итоговый `DESIGN.md`, а не принимать output Impeccable автоматически.

### Stops

После approved `DESIGN.md`.

После joint Gate 1 ownership меняется:

```text
design-context -> initial author
art-director   -> ongoing steward
```

Design Context window можно закрыть.

---

## 5.4 `art-director`

### Owns

```text
design/explorations/
design/approved-direction/
design/approved-sections/
```

После Gate 1 становится steward файла `DESIGN.md`.

Может обновлять его только если:

- появился действительно повторяемый visual principle;
- approved Visual Direction уточнил системный принцип;
- выполняется контролируемая синхронизация Impeccable с реальным UI.

После нескольких representative sections Art Director один раз запускает `/impeccable document`, проверяет diff `DESIGN.md` и принимает только изменения, которые соответствуют approved UI. Эта команда синхронизирует документацию с production-кодом, а не переизобретает visual direction.

### Reads

```text
PRODUCT.md
DESIGN.md
content/page.md
references/
already approved sections
```

### Tools

```text
browser
Web Search
lightweight mockup implementation
Impeccable design/refinement commands при необходимости
```

Mobbin используется через отдельного `reference-researcher`, а не как случайная библиотека готовых компонентов.

### Subagent

```text
reference-researcher
```

Запускается, когда:

```text
для нужного блока нет прямого reference
или существующий reference не решает задачу секции
```

Parent Art Director получает от него curated evidence, а не весь шум поиска.

### Human gates

Для каждого блока:

```text
reference?
CLOSE / ADAPT / INSPIRE?
↓
2-3 variants для важных/неочевидных sections
↓
operator selects / combines
```

После выбора Art Director выполняет asset + responsive check.

---

## 5.5 `frontend-coder`

### Owns

```text
production application code
```

### Reads

```text
AGENTS.md
DESIGN.md
content/page.md
approved section mockup
approved assets
responsive intent
existing production code
```

### Tools

```text
shell
browser
tests / lint / build
Impeccable hooks
Impeccable targeted refinement commands
Impeccable polish только после фиксации структуры блока
```

Не нужны:

```text
DataForSEO
Mobbin
reference research
```

### Hard boundary

Coder не меняет самостоятельно:

```text
approved copy
approved composition
visual direction
```

Если реализация показывает, что approved решение проблемное, возвращает вопрос Art Director/operator.

### Subagent

В начале Section Loop Coder спавнит:

```text
persistent visual-reviewer
```

Этот reviewer используется для последовательных section reviews.

Причина: именно Coder window живет весь implementation loop и может переиспользовать один subagent thread.

Если reviewer начинает drift'овать, повторять старые findings или путать sections, он заменяется fresh instance.

---

## 5.6 `reviewer`

Один skill, несколько lazy-loaded modes:

```text
reviewer/
├─ SKILL.md
└─ modes/
   ├─ section.md
   ├─ whole-page.md
   ├─ seo-tech.md
   └─ polish.md
```

Reviewer всегда независим и никогда не исправляет application code.

### Два custom-agent профиля, один skill

Один `reviewer.toml` недостаточен для всех режимов из-за разных sandbox needs.

```text
.codex/agents/
├─ visual-reviewer.toml
└─ technical-reviewer.toml
```

Оба используют один `reviewer` skill, но разный tool surface.

#### `visual-reviewer`

Для:

```text
section
whole-page
polish critic
```

Config:

```text
sandbox_mode = read-only
browser / screenshots
Impeccable critique
Impeccable detector / read-only audit where possible
```

В v1 изоляция опирается на explicit invocation, `allow_implicit_invocation: false`, узкие descriptions, custom-agent `developer_instructions` и явный `sandbox_mode`. Hard `skills.config` / MCP allowlists откладываются, пока portable paths и реальные MCP identities не подтверждены; omitted settings наследуются от parent.

#### `technical-reviewer`

Для:

```text
seo-tech
```

Может иметь `workspace-write`, потому что build/test/performance tools иногда создают caches или output artifacts.

При этом developer instructions жестко запрещают:

```text
редактировать application source
apply patches
исправлять findings самостоятельно
```

Перед/после technical checks фиксируется `git status`, чтобы временные outputs не маскировали source changes.

### Common inputs

```text
browser / screenshots
relevant canonical artifacts
approved mockups/references
project code in appropriate sandbox
```

Не нужны без явной задачи:

```text
Mobbin
DataForSEO
art-director skill
frontend-coder skill
```

### `section`

Используется persistent `visual-reviewer` из Coder window.

Проверяет:

```text
approved mockup vs live render
typography / spacing / proportions
responsive
layout / interaction bugs
AI-slop introduced during implementation
cross-section consistency
```

После fix:

```text
review old findings + fix diff
```

Не запускает полный review блока заново без причины.

Если текущий Codex harness не позволяет надежно продолжать тот же completed reviewer thread, используется fresh `visual-reviewer` с теми же canonical inputs. Workflow не должен зависеть от persistence как от обязательной возможности.

### `whole-page`

Всегда fresh `visual-reviewer`.

Спавнится из Orchestrator после завершения всех sections.

Проверяет только whole-page issues:

```text
rhythm
repeated composition
visual density
cross-section hierarchy
funnel continuity
desktop/mobile coherence
```

### `seo-tech`

Использует `technical-reviewer`.

Проверяет финальную реализацию против:

```text
PRODUCT.md
content/strategy.md
content/page.md
```

### `polish`

Только если включен `POLISH`.

Каждый round может использовать fresh `visual-reviewer` / critic.

Hard precondition:

```text
есть внешний reference / comparable
```

Без reference loop не запускается.

Максимум:

```text
3 rounds
```

После fix проверяется только найденное различие и возможная regression.


---

# 6. Custom subagents

## `seo-researcher`

Parent:

```text
Strategist
```

Scope:

```text
read-only
```

Tools:

```text
Web
browser
DataForSEO только если SEO VERIFIED
```

Writes repo:

```text
нет
```

Returns:

```text
sources
SERP evidence
keyword evidence
competitor observations
uncertainties
```

Не принимает финальные SEO/content решения.

Рекомендуется держать protocol не отдельным глобальным skill, а внутри:

```text
strategist/prompts/seo-researcher.md
```

---

## `reference-researcher`

Parent:

```text
Art Director
```

Scope:

```text
read-only
```

Tools:

```text
Mobbin MCP
Web Search
image/reference search
```

Writes repo:

```text
нет
```

Returns:

```text
3-5 strongest candidates
direct URLs
что конкретно полезно взять
какая композиционная идея релевантна текущему section
```

Не создает финальный дизайн.

Protocol:

```text
art-director/prompts/reference-researcher.md
```

---

## Reviewer agents

`visual-reviewer` parent during Section Loop:

```text
Frontend Coder
```

`visual-reviewer` parent during Final Page Review:

```text
Website Orchestrator
```

Scope:

```text
read-only
```

Application-code writes:

```text
запрещены
```

`technical-reviewer` используется на SEO / Technical Pass.

Оба custom agent config явно задают собственный `sandbox_mode` и узкие `developer_instructions`. Hard `skills.config` и MCP allowlists добавляются только после подтверждения portable paths и стабильных MCP identities; до этого omitted settings наследуются от parent.

---

# 7. Spawn matrix

```text
Website Orchestrator
├─ fresh visual-reviewer
│  └─ whole-page / optional polish critic
└─ technical-reviewer
   └─ seo-tech final pass

Strategist
└─ seo-researcher
   └─ competitor / SERP / keyword research

Art Director
└─ reference-researcher
   └─ targeted block references

Frontend Coder
└─ persistent visual-reviewer
   └─ sequential section reviews
      (fresh fallback if persistence is unavailable/unreliable)
```

`design-context` в v1 subagents не спавнит.

Никакой subagent не получает tool surface "на всякий случай".

---

# 8. Human gate map

```text
Stage 0
operator gives project inputs

Stage 1A + 1B
one joint review:
strategy.md + DESIGN.md

Stage 2
operator selects/combines content block by block

Stage 3
operator selects/combines Visual Direction

Stage 4 Section Loop
for each important block:
  reference fidelity
  mockup choice
  missing real assets if needed
  final live-block approve

Final
operator reviews full live site
explicit deploy/release only after operator command
```

---

# 9. Settings ownership

Пока настройки не реализуются как parser/slash-command.

Orchestrator просто хранит их flags в `.website/state.md`.

```text
SEO VERIFIED
owner logic: strategist

DEEP
owner logic: strategist + art-director

POLISH
owner logic: reviewer + art-director/frontend-coder
```

Per-section:

```text
CLOSE / ADAPT / INSPIRE
```

не является project setting. Это решение оператора для конкретного блока.

---

# 10. Handoff между окнами

Не создаем отдельный handoff-документ после каждого этапа.

Source of truth - файлы проекта.

Specialist завершает этап так:

```text
1. обновляет свой canonical artifact
2. коротко пишет оператору:
   - что готово
   - что требует решения
   - какие blockers остались
3. Orchestrator на крупном gate обновляет `.website/state.md`
```

Это позволяет держать процесс компактным.

---

# 11. Skill Builder / Maintainer

Это не runtime role website-проекта.

Это локальный агент, который получает от Architect точную спецификацию и физически меняет приватный repository с website starter / skills.

Каждое задание Skill Builder обязательно заканчивается:

```text
1. проверить итоговые файлы и дерево
2. проверить согласованность `WORKFLOW.md` ↔ `website-workflow`
3. выполнить предусмотренные validation / smoke checks
4. git status
5. commit с конкретным сообщением
6. push в настроенный private remote
7. вернуть:
   - branch
   - commit hash
   - push status
   - changed files
   - checks performed
```

Если commit или push не удался:

```text
не считать задачу завершенной
сообщить точную причину
не скрывать локальные uncommitted changes
```

Skill Builder не имеет права самостоятельно менять архитектуру ролей или workflow.

Изменение архитектуры сначала согласуется здесь, затем уходит ему как implementation task.

---

# 12. Порядок создания v1

Не писать всё одновременно.

Рекомендуемый порядок:

```text
1. website-workflow
   + .website/state.md schema

2. reviewer
   + visual-reviewer.toml
   + technical-reviewer.toml
   + modes/

3. strategist
   + seo-researcher.toml
   + researcher prompt

4. design-context

5. art-director
   + reference-researcher.toml
   + researcher prompt

6. frontend-coder

7. project .codex/config.toml
   + custom-agent sandbox isolation
   + explicit skill invocation / implicit-off
   + MCP/skills hard allowlists only when portable identities/paths are verified

8. smoke-test disposable website repo

9. independent architecture review

10. fixes -> scoped re-test
```

Почему reviewer создается раньше остальных specialists:

- через него сразу можно проверять последующие skills;
- isolation reviewer является одним из самых важных технических рисков;
- section/final review уже хорошо определены workflow.

---

# 13. Что специально НЕ делаем в v1

```text
- не создаем десятки specialist roles
- не делаем новый subagent на каждый section
- не даем всем ролям все skills/MCP
- не превращаем WORKFLOW.md в prompt каждого агента
- не заставляем specialist читать все phases заранее
- не создаем отдельный handoff/report файл после каждого действия
- не автоматизируем SEO/DEEP/POLISH parser до smoke-test базовой системы
```

---

# 14. Главная архитектура

```text
                 WEBSITE ORCHESTRATOR
                 website-workflow
                        |
          +-------------+-------------+
          |                           |
     STRATEGIST                  DESIGN CONTEXT
          |                           |
    seo-researcher                    |
          |                           |
          +-------------+-------------+
                        |
                  CONTENT READY
                        |
                  ART DIRECTOR
                        |
              reference-researcher
                        |
                  approved mockup
                        |
                 FRONTEND CODER
                        |
                persistent visual-reviewer
                        |
                 operator approve
                        |
                   next section
                        |
                  all sections done
                        |
             FRESH VISUAL REVIEWER
                        |
              [optional POLISH]
                        |
                 TECHNICAL REVIEWER / SEO-TECH PASS
                        |
                HUMAN FINAL REVIEW
```
