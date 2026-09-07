# skills

Skills públicas para Claude Code (y harnesses compatibles con `SKILL.md`).
Forman un harness de trabajo con reparto fijo de modelos: **Fable 5.1** orquesta,
diseña, revisa y es la única mano en git/GitHub; **GPT-6 Astra** (Codex CLI) y
**Opus 5** teclean; los jueces son de familias distintas para que fallen distinto.

| Rol | Modelo | Effort | Skill |
|---|---|---|---|
| Orquestador / arquitecto / spec | Fable 5.1 | n/a | `orchestrate-opus`, `batch-conductor` |
| Research de código (scouts) | Opus 5 | n/a | `opus-research` |
| Worker mecánico (spec congelada) | GPT-6 Astra vía Codex | `high` (`xhigh` duro) | `codex-first` + `frictionless-focus` |
| Worker de juicio (contratos, RLS, UX, MCP) | Opus 5 | n/a | `opus-first` + `frictionless-focus` |
| Lente spec | Sonnet 5 | n/a | `batch-conductor` Fase 3 |
| Juez A (código) | GPT-6 Astra, Codex en modo lectura | `high` | `batch-conductor` Fase 3 |
| Juez B (estructura) | Fable 5.1 / Opus 5 | n/a | `thermo-nuclear-code-quality-review` como rúbrica |
| Seguridad / RLS, gates, evidencia, git | Fable 5.1 | n/a | `batch-conductor` |

## Skills

| Skill | Qué hace |
|---|---|
| [`batch-conductor`](skills/batch-conductor/SKILL.md) | Conduce uno o varios issues de principio a fin: autogrill, spec congelada, implementación delegada, revisión en lentes decorrelacionadas, evidencia visual, PR/CI/CodeRabbit, merge y cierre. |
| [`orchestrate-opus`](skills/orchestrate-opus/SKILL.md) | Modo operativo: Fable orquesta, Opus implementa, Codex es worker mecánico y Juez A. Ciclo de siete pasos. |
| [`codex-first`](skills/codex-first/SKILL.md) | Ruteo de implementación a Codex CLI (GPT-6 Astra) con spec congelada; Claude verifica. Modelo y effort siempre explícitos. |
| [`opus-first`](skills/opus-first/SKILL.md) | Ruteo de implementación con juicio a subagentes Opus 5 (heredan el harness: CLAUDE.md, skills, MCP). |
| [`opus-research`](skills/opus-research/SKILL.md) | Research de código con scouts Opus 5: Fable briefa, el scout lee y cita `path:line`, Fable debriefa. |
| [`frictionless-focus`](skills/frictionless-focus/SKILL.md) | Disciplina de la mano que implementa: una unidad, una prueba, tangentes estacionadas, decisiones por precedente sin preguntas. Los workers (Opus o Codex) la cargan al recibir una spec congelada. |
| [`chestertons-fence`](skills/chestertons-fence/SKILL.md) | Antes de quitar o rodear código existente: nombrar la cerca, encontrar al constructor (cita inline, `git log -S`, PR/issue, ADR, wiki), veredicto holds/expired/unknown, dejar marcador rastreable. El Juez B la aplica antes de proponer borrar. |
| [`sbar`](skills/sbar/SKILL.md) | Handoff entre agentes o sesiones en cuatro bloques: Situation, Background, Assessment, Recommendation. Para `gt handoff`, HELP al Witness, notas de bead antes de morir y el Stopped-at de un reporte. |
| [`thermo-nuclear-code-quality-review`](skills/thermo-nuclear-code-quality-review/SKILL.md) | Rúbrica de revisión estructural extrema (judo de código, megaarchivos, spaghetti). Lleva `disable-model-invocation`: se lee y se aplica, no se invoca. |

## Principios como skills

Independientes del harness anterior: no asumen orquestador, worker ni herramienta. Cada una es un principio con nombre propio en el
entrenamiento del modelo, convertido en pasos con criterio de terminado.

| Skill | Principio | Corrige |
|---|---|---|
| [`falsification`](skills/falsification/SKILL.md) | Popper, con Occam como paso | El fix que "funciona" sin diagnóstico probado |
| [`survivorship-bias`](skills/survivorship-bias/SKILL.md) | Wald, los aviones | Fixtures y muestras que solo contienen los casos que volvieron |
| [`pre-mortem`](skills/pre-mortem/SKILL.md) | Klein | Checklists que solo cubren lo que ya falló una vez |
| [`veil-of-ignorance`](skills/veil-of-ignorance/SKILL.md) | Rawls | Políticas de acceso escritas desde el rol que las pidió |
| [`steelman`](skills/steelman/SKILL.md) | Steelman | Rebatir la redacción débil de un hallazgo válido |
| [`via-negativa`](skills/via-negativa/SKILL.md) | Taleb | Refactors que añaden antes de quitar |
| [`lindy`](skills/lindy/SKILL.md) | Efecto Lindy | Elegir lo nuevo sin un hueco concreto que lo justifique |
| [`hansei`](skills/hansei/SKILL.md) | Toyota | Cierres que atribuyen a la suerte lo que fue decisión propia |
| [`five-whys`](skills/five-whys/SKILL.md) | Ohno | Lecciones que registran el síntoma y no la causa |
| [`one-way-doors`](skills/one-way-doors/SKILL.md) | Bezos | Preguntar de más en lo reversible y de menos en lo irreversible |

## Instalar

Copia las carpetas que quieras a `.claude/skills/` de tu repo (o a `~/.claude/skills/` para uso global):

```bash
git clone https://github.com/smaagk/skills.git
cp -r skills/skills/* .claude/skills/
```

## Dependencias externas

`batch-conductor` compone tres skills de [mattpocock/skills](https://github.com/mattpocock/skills) que no se republican aquí:
`grill-with-docs` (que a su vez usa `grilling` y `domain-modeling`), `code-review` (dos ejes: estándares y spec) y
`resolving-merge-conflicts`. Instálalas desde ese repo con el mismo nombre.

`codex-first` menciona `$maintainer-orchestrator` y `$autoreview` como referencias opcionales; no forman parte de este repo.

Las skills asumen Codex CLI instalado (`codex exec`) y, para las de Opus, el Agent tool de Claude Code.
Algunas rutas de ejemplo (`libs/shared/data-access`, `supabase/migrations`, lentes `ui/data/db/flow`) vienen de un monorepo
Nx + Angular + Supabase; ajústalas a tu repo.

## Licencia

MIT
