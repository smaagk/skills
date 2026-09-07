# skills

Cuarenta y dos skills para Claude Code (y harnesses compatibles con `SKILL.md`), ordenadas por el ciclo de vida
de una pieza de trabajo: planear → decidir → implementar → diagnosticar → revisar → cerrar. La categoría 0
es el harness que las orquesta; la 7 es transversal, el ritmo de la sesión. Cada skill es un principio con
nombre propio convertido en pasos con criterio de terminado, según `/writing-great-skills`.

Solo las cinco del harness (0) se asumen entre sí. Las otras treinta y siete son agnósticas: no suponen
orquestador, worker ni herramienta, y no se cablean solas — se instalan y se invocan, o se apuntan desde
tus propias skills.

Cada skill fuera de `0-harness` incluye una sección `Example` con una petición y su
aplicación concreta. Las rutas, comandos, cifras y resultados de esos ejemplos son
ilustrativos; adáptalos al proyecto donde invoques la skill.

## Instalar

```bash
git clone https://github.com/smaagk/skills.git
cp -r skills/skills/*/* .claude/skills/        # todas
cp -r skills/skills/3-implementar/* .claude/skills/   # o una categoría
```

Cada carpeta de skill se copia entera (algunas traen archivos auxiliares). A `~/.claude/skills/` para uso global.

## 0 · Harness

Reparto fijo de modelos: **Fable 5.1** orquesta, diseña, revisa y es la única mano en git/GitHub; **GPT-6 Astra**
(Codex CLI) y **Opus 5** teclean; los jueces son de familias distintas para que fallen distinto.

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

| Skill | Qué hace |
|---|---|
| [`orchestrate-opus`](skills/0-harness/orchestrate-opus/SKILL.md) | Modo operativo: Fable orquesta, Opus implementa, Codex es worker mecánico y Juez A. Ciclo de siete pasos. |
| [`batch-conductor`](skills/0-harness/batch-conductor/SKILL.md) | Conduce uno o varios issues de principio a fin: autogrill, spec congelada, implementación delegada, lentes decorrelacionadas, evidencia, PR/CI, merge y cierre. |
| [`opus-research`](skills/0-harness/opus-research/SKILL.md) | Research de código con scouts Opus 5: Fable briefa, el scout lee y cita `path:line`, Fable debriefa. |
| [`opus-first`](skills/0-harness/opus-first/SKILL.md) | Implementación con juicio en subagentes Opus 5, que heredan el harness (CLAUDE.md, skills, MCP). |
| [`codex-first`](skills/0-harness/codex-first/SKILL.md) | Implementación mecánica en Codex CLI (GPT-6 Astra) con spec congelada; modelo y effort siempre explícitos. |

Dependencias externas del harness, de [mattpocock/skills](https://github.com/mattpocock/skills) y no republicadas aquí:
`grill-with-docs` (con `grilling` y `domain-modeling`), `code-review` (dos ejes) y `resolving-merge-conflicts`.
`codex-first` menciona `$maintainer-orchestrator` y `$autoreview` como referencias opcionales que no forman parte de este repo.
Algunas rutas de ejemplo vienen de un monorepo Nx + Angular + Supabase; ajústalas.

## 1 · Planear

| Skill | Principio | Corrige |
|---|---|---|
| [`working-backwards`](skills/1-planear/working-backwards/SKILL.md) | Amazon | Planes hacia adelante que acumulan pasos innecesarios |
| [`riskiest-assumption`](skills/1-planear/riskiest-assumption/SKILL.md) | Lean | Probar al final la creencia que podía matar el plan al principio |
| [`outside-view`](skills/1-planear/outside-view/SKILL.md) | Kahneman | Estimar desde el plan y no desde la clase de referencia |
| [`critical-path`](skills/1-planear/critical-path/SKILL.md) | Goldratt | Paralelizar y rescatar pasos fuera de la cadena crítica |
| [`rolling-wave`](skills/1-planear/rolling-wave/SKILL.md) | Fog of war | Detallar lo que aún no se sabe y reescribirlo después |
| [`spike`](skills/1-planear/spike/SKILL.md) | XP | Código escrito para aprender que termina en producción |
| [`essentialism`](skills/1-planear/essentialism/SKILL.md) | McKeown, con minimalismo | Meterlo todo en vez de elegir; cortes silenciosos que vuelven como scope creep |
| [`lindy`](skills/1-planear/lindy/SKILL.md) | Efecto Lindy | Elegir lo nuevo sin un hueco concreto que lo justifique |

## 2 · Decidir

| Skill | Principio | Corrige |
|---|---|---|
| [`one-way-doors`](skills/2-decidir/one-way-doors/SKILL.md) | Bezos | Preguntar de más en lo reversible y de menos en lo irreversible |
| [`satisficing`](skills/2-decidir/satisficing/SKILL.md) | Herbert Simon | Búsqueda de alternativas sin condición de fin |
| [`thirty-seven-percent`](skills/2-decidir/thirty-seven-percent/SKILL.md) | Optimal stopping | Candidatos secuenciales sin regla de parada (sin vuelta atrás) |
| [`pre-mortem`](skills/2-decidir/pre-mortem/SKILL.md) | Klein | Checklists que solo cubren lo que ya falló una vez |

## 3 · Implementar

| Skill | Principio | Corrige |
|---|---|---|
| [`frictionless-focus`](skills/3-implementar/frictionless-focus/SKILL.md) | Flow / single-piece flow | Preguntas que el repo respondía, tangentes, decisiones reabiertas |
| [`tracer-bullet`](skills/3-implementar/tracer-bullet/SKILL.md) | Pragmatic Programmer | Construir una capa entera antes de tocar la siguiente |
| [`batching`](skills/3-implementar/batching/SKILL.md) | Batching | Alternar leer, editar y correr de uno en uno |
| [`two-minute-rule`](skills/3-implementar/two-minute-rule/SKILL.md) | GTD | Estacionar trivialidades que costaban menos hacer que anotar |
| [`lab-notebook`](skills/3-implementar/lab-notebook/SKILL.md) | Cuaderno de laboratorio | Reportes reconstruidos de memoria |

## 4 · Diagnosticar

| Skill | Principio | Corrige |
|---|---|---|
| [`falsification`](skills/4-diagnosticar/falsification/SKILL.md) | Popper, con Occam | El fix que "funciona" sin diagnóstico probado |
| [`survivorship-bias`](skills/4-diagnosticar/survivorship-bias/SKILL.md) | Wald | Fixtures y muestras con solo los casos que volvieron |
| [`five-whys`](skills/4-diagnosticar/five-whys/SKILL.md) | Ohno | Lecciones que registran el síntoma y no la causa |

## 5 · Revisar

| Skill | Principio | Corrige |
|---|---|---|
| [`thermo-nuclear-code-quality-review`](skills/5-revisar/thermo-nuclear-code-quality-review/SKILL.md) | Judo de código | Revisiones que aceptan "funciona" y dejan el diseño peor. Rúbrica, no se invoca |
| [`chestertons-fence`](skills/5-revisar/chestertons-fence/SKILL.md) | Chesterton | Borrar guards, flags o helpers sin saber quién los puso |
| [`via-negativa`](skills/5-revisar/via-negativa/SKILL.md) | Taleb | Refactors que añaden antes de quitar |
| [`veil-of-ignorance`](skills/5-revisar/veil-of-ignorance/SKILL.md) | Rawls | Políticas de acceso escritas desde el rol que las pidió |
| [`steelman`](skills/5-revisar/steelman/SKILL.md) | Steelman | Rebatir la redacción débil de un hallazgo válido |
| [`pareto`](skills/5-revisar/pareto/SKILL.md) | 80/20 | Diez nits arreglados y el bloqueador abierto |

## 6 · Cerrar y entregar

| Skill | Principio | Corrige |
|---|---|---|
| [`definition-of-done`](skills/6-cerrar/definition-of-done/SKILL.md) | Scrum | "Terminado" definido en cuatro sitios con diferencias |
| [`sbar`](skills/6-cerrar/sbar/SKILL.md) | Protocolo de enfermería | Handoffs y escaladas que obligan a leer el transcript |
| [`hansei`](skills/6-cerrar/hansei/SKILL.md) | Toyota | Cierres que atribuyen a la suerte lo que fue decisión propia |

## 7 · Ritmo de sesión (transversal)

| Skill | Principio | Corrige |
|---|---|---|
| [`eat-the-frog`](skills/7-ritmo/eat-the-frog/SKILL.md) | Brian Tracy | Lo difícil se queda para cuando el contexto ya está lleno |
| [`ivy-lee`](skills/7-ritmo/ivy-lee/SKILL.md) | Ivy Lee | Listas que se hojean y abren ítems en paralelo |
| [`wip-limit`](skills/7-ritmo/wip-limit/SKILL.md) | Kanban | Ramas, worktrees y PRs huérfanos |
| [`parkinson`](skills/7-ritmo/parkinson/SKILL.md) | Parkinson | "Casi termino" dicho dos veces |
| [`maker-manager-schedule`](skills/7-ritmo/maker-manager-schedule/SKILL.md) | Paul Graham | Revisar un diff con media atención en un monitor |
| [`interruption-marker`](skills/7-ritmo/interruption-marker/SKILL.md) | Práctica del cirujano | Reorientación costosa tras una interrupción |
| [`separation-of-space`](skills/7-ritmo/separation-of-space/SKILL.md) | Un espacio, un uso | Spikes en el árbol de entrega; diseño reabierto a mitad de implementación |
| [`zeigarnik`](skills/7-ritmo/zeigarnik/SKILL.md) | Zeigarnik | El "luego lo hago" que muere con la sesión |

## Pares deliberados

Varias skills existen en pareja y se nombran entre sí: `spike` (se tira) y `tracer-bullet` (se queda);
`two-minute-rule` es el contrapeso del *park* de `frictionless-focus`; `parkinson` generaliza el timebox de `spike`;
`satisficing` y `thirty-seven-percent` resuelven la misma parada con y sin vuelta atrás;
`essentialism` decide qué entra y `via-negativa` qué sale del código que ya existe; `separation-of-space` es el suelo
que `spike` y `lab-notebook` asumen; `chestertons-fence` frena lo que
`via-negativa` y la rúbrica thermo-nuclear empujan a quitar; `lindy` es la cerca aplicada a dependencias.

## Licencia

MIT
