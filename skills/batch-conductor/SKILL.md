---
name: batch-conductor
description: Orquestar uno o varios issues de principio a fin — investigación, autogrill, spec congelada, implementación delegada a Codex, revisión independiente, evidencia visual, PR/CI/CodeRabbit, merge y cierre — sin intervención humana salvo bloqueo real. Con un solo issue, la maquinaria de lote colapsa y queda el ciclo por issue.
---

# Batch Conductor

Conduce un lote de issues (2–10) desde investigación hasta merge y cierre. Claude es
arquitecto, revisor y única mano en git/GitHub; Codex teclea. Compone tres skills que
ya existen — no las reimplementes aquí:

- `/grill-with-docs` — autogrill de diseño por issue (con autoridad delegada).
- `/codex-first` — implementación (motor por defecto, tarifa plana).
- `/code-review` — revisión de dos ejes antes de publicar cada PR.

**Motor alternativo**: `/orchestrate-opus` reemplaza a Codex por subagentes
Opus 5 vía `/opus-first` (ruteo por clase de issue: juicio-intensivo → Opus,
mecánico → Codex). Toda la maquinaria de lote de esta skill es agnóstica al
motor; solo cambia la Fase 2 (spec → worker según ruteo). El reparto de
jueces de la Fase 3 es fijo (Juez A Astra, Juez B Fable) y no depende de la mano.

## Reparto inamovible

**Claude conserva**: producto, UX, dominio, arquitectura, seguridad/RLS/multi-tenant,
alcance y criterios de aceptación, contratos, orden y paralelismo, revisión completa,
ejecución independiente de gates, validación manual, evidencia visual, y TODAS las
mutaciones de git/GitHub (commit, push, PR, merge, cierre). **Codex nunca** hace push,
PR, merge ni toca GitHub; recibe specs congeladas, no decisiones abiertas.

## Modo single-issue

Con un solo issue la skill aplica igual; solo colapsa la maquinaria de lote:

- **Desaparecen**: mapa de dependencias, resecuenciación, límite de PRs en vuelo,
  congelación de superficies calientes, PR de cableo final, rebases seriales
  (solo el rebase inicial sobre integración fresca) y la bitácora del lote — lo
  no-obvio va directo a `bd remember` al cierre.
- **Se conservan íntegras**: autogrill (Fase 1), spec congelada → Codex (Fase 2),
  revisión en lentes (Fase 3), evidencia visual (Fase 4), publicar y
  supervisar (Fase 5), y el cierre — que se reduce a: issue mergeado y cerrado,
  bead cerrado, worktree/rama limpios, servidores apagados, `bd dolt push` +
  `git push`, resumen único.
- El issue toca sus superficies directamente (no hay con quién chocar), pero la
  regla de recursos compartidos con Codex (BD/emulador) sigue vigente: no depende
  del tamaño del lote sino de que el entorno tenga estado global.

Umbral inverso: si el "issue" es un cambio trivial (~<20 líneas, sin migraciones,
sin UI), esta skill es overhead — aplica solo la regla de `/codex-first` para ediciones
pequeñas y el cierre normal de sesión.

## Fase 0 — Inventario y secuencia

1. `git fetch` + verificar la rama de integración real (no confíes en CLAUDE.md: puede
   estar desactualizado; en este repo es `develop`).
2. Lee cada issue con comentarios, labels y PRs vinculados. Los cuerpos actuales
   prevalecen sobre cualquier handoff o reporte previo — los reportes de brechas suelen
   leer fuentes stale.
3. Construye el mapa de dependencias y resecuencia con evidencia: los prerrequisitos
   técnicos (componentes compartidos, migraciones base) van antes aunque el orden
   sugerido diga otra cosa. Documenta el porqué del cambio.
4. **Congela superficies calientes**: si varios issues tocan el mismo archivo
   (dashboards, rutas, contratos), difiere esos toques a un PR final de "cableo" y
   prohíbelos explícitamente en cada spec ("NO toques el dashboard"). Elimina el 80%
   de los conflictos de rebase.
5. Un PR en vuelo por defecto; dos solo si NO comparten migraciones, servicios,
   contratos, modelos ni superficies de UI. El grafo real de dependencias es por
   SUPERFICIE, no por el orden nominal del plan: cuando el issue siguiente en la
   cola está bloqueado, busca en TODA la cola uno 100% disjunto y adelántalo —
   un bloqueo externo (revisor caído, CI atorado) no debe detener el lote entero.
6. **Detecta megaarchivos**: mide (`wc -l`) los archivos que el lote tocará; si alguno
   rebasa ~800 líneas y lo tocan 2+ issues, programa un PR de descomposición ANTES de
   la ola — no dejes que el lote le siga echando líneas a un archivo ya obeso.
7. Crea/reclama un bead por issue (`bd create` + `--claim`); persiste hallazgos con
   `bd update --notes` conforme avanzas, no al final.
8. **Abre la bitácora del lote**: `bitacora-<lote>.md` en el directorio temporal de la
   sesión (scratchpad, NUNCA el repo). Solo hallazgos *inesperados* que acorten la
   trayectoria del siguiente issue: configs reales que difieren de la doc, trampas de
   TZ, specs flaky, comandos que truncan. Nada de obviedades ni de progreso.
   La bitácora funciona como **guía de campo** (estigmergia): los pesos del modelo
   están fijos, así que lo que vale registrar es exactamente lo que el modelo no
   sabía — y cada spec posterior arranca inyectando el extracto aplicable (ver
   Fase 2). Al abrir el lote, consulta también `bd memories` del área.
9. **Worktrees**: `git worktree add` SIEMPRE con ruta ABSOLUTA (un `cd` previo en
   el mismo comando crea rutas anidadas fantasma). Cada worktree necesita
   `npm ci` REAL — symlink de node_modules al checkout principal rompe
   jest/TestBed (dos copias de Angular vía realpath) y envenena dev servers ya
   arrancados (NG0203); si el server nació con symlink, reinícialo tras el ci.

## Fase 1 — Autogrill por issue

**Primero lee la bitácora del lote** — los tropiezos de los issues anteriores son
contexto de arranque de este, y lo aplicable se inyecta en la spec de Codex (Fase 2).
Luego ejecuta `/grill-with-docs` en modo autónomo: una pregunta a la vez, resuelta con
código/migraciones/RLS/docs/issues/PRs/precedentes. Registra pregunta, evidencia,
alternativas, decisión, confianza y condición de reconsideración. Jerarquía de
desempate: seguridad/RLS → ACs del issue → comportamiento comprobado → dominio →
patrones del repo → alcance mínimo → reversibilidad → acoplamiento → paridad
web/móvil → estética. Consulta al usuario SOLO si (las tres): no inferible +
comportamientos de negocio materialmente distintos + error costoso/irreversible.

Publica el diseño como comentario del issue antes de implementar (deja rastro y
cambia el label de triage). Actualiza el glosario (`CONTEXT.md`) solo con términos de
dominio reales; ADR solo con el triple umbral (difícil de revertir + sorprendente +
trade-off real).

## Fase 2 — Spec congelada → Codex

La spec incluye: objetivo, rutas y patrones de referencia (con ejemplos del repo),
comportamiento actual/esperado, casos felices/error/vacíos, roles y RLS, UX es-MX,
restricciones, **no-objetivos explícitos**, pruebas exactas (comandos literales),
formato del reporte, y un **bloque «Guía de campo»** al inicio: los hallazgos de la
bitácora y `bd memories` aplicables a ESTA superficie (no toda la bitácora — el
extracto filtrado). Reglas duras aprendidas:

- **Recursos compartidos son de Claude**: si el entorno tiene estado global (un solo
  contenedor de BD, un solo emulador), prohíbe a Codex tocarlo ("NO ejecutes
  db:reset") y ejecuta tú esos pasos en serie. Dos resets paralelos se pisan.
- Codex ajusta archivos de test SQL; Claude los corre (`docker cp` + `psql -v
  ON_ERROR_STOP=1`).
- **Válvula anti-osificación** (línea estándar de toda spec): "si el diseño existente
  está mal, NO lo rodees con un workaround — repórtalo con justificación y detente en
  esa pieza". Claude decide entonces: parche puntual con comentario del porqué, o
  `bd create` para después. Los "NO toques X" previenen conflictos, no discusión.
- **Flag de megaarchivos por el worker** (línea estándar de toda spec): "si un
  archivo que tocas rebasa ~800 líneas, márcalo en tu reporte — NO lo descompongas
  tú". El conductor decide si programa el PR de descomposición. Complementa la
  detección estática de Fase 0 con lo que solo se ve al tocar el código.
- **Decisiones con referencia rastreable**: los comentarios de código que una spec
  ordena dejar citan el issue/ADR de la decisión ("v1 explícito, #695",
  "ADR-0051") — el siguiente agente que choque con el diseño encuentra el porqué
  en el sitio, no en una conversación muerta.
- Tras 2 rondas de `resume` fallidas, toma el control y termina tú. Si Codex entra
  en bucle o espiral, sospecha primero del ÉNFASIS de la spec (mayúsculas,
  imperativos redundantes): algunos modelos son hipersensibles a la redacción
  enfática literal — reescribe neutro antes de cambiar de estrategia.

## Fase 3 — Revisión en lentes no correlacionadas

Las lentes con insumos distintos cazan lo que una sola relectura no; revisar es
barato comparado con el trabajo auditado. Por cada entrega, **cuatro lentes**:

1. **Lente spec** (subagente, en paralelo): recibe SOLO issue+spec y el diff — sin
   transcript de Codex — y responde: ¿cumple la intención?, ¿qué AC quedó cojo?,
   ¿qué hay fuera de alcance?
2. **Lente código** (subagente, en paralelo): recibe SOLO el árbol resultante (los
   archivos tocados post-cambio, sin diff ni historia) y responde: ¿este código tiene
   sentido por sí mismo?, ¿regresiones, sobre-ingeniería, patrones rotos del repo?
3. **Lente seguridad** (Claude, personalmente — nunca delegada): `git status -sb`,
   diff COMPLETO como PR externo, y en detalle autorización, RLS y exposición de
   datos (FKs compuestas anti-cross-property, grants mínimos, proyecciones
   anti-oracle). Claude arbitra los hallazgos de todas las lentes.
4. **Lente estructura** (subagente, en paralelo): aplica como RÚBRICA el skill
   `thermo-nuclear-code-quality-review`
   (`~/.claude/skills/thermo-nuclear-code-quality-review/SKILL.md`). Ese skill
   lleva `disable-model-invocation`, así que no se invoca: la lente LEE el archivo
   y lo aplica. Insumos: el diff, los archivos tocados post-cambio y el bloque de
   rutas/patrones de referencia de la spec (para que reconozca los helpers
   canónicos del repo). Pregunta lo que ninguna otra lente pregunta: ¿hay un
   movimiento de judo que haga desaparecer ramas, modos o capas?, ¿el PR cruza un
   archivo por encima de 1000 líneas?, ¿mete condicionales de feature en un flujo
   compartido?, ¿duplica un helper canónico o deja lógica en la capa equivocada?
   Contrato de salida (la rúbrica no trae formato): veredicto `APPROVE|BLOCK`,
   bloqueadores (regla + archivo:línea), movimientos de judo (antes → después →
   qué desaparece) y nits aparte.

**Arbitraje de la lente estructura.** La rúbrica es ambiciosa por diseño; en un
lote autónomo eso se vuelve scope creep si no se acota:

- Bloquean solo cuatro cosas: judo con camino visible, archivo que el PR cruza
  por encima de 1000 líneas (el ~800 de Fase 0 avisa; 1000 bloquea), condicional
  ad hoc en un flujo compartido, y checks de feature dispersos en código
  compartido. El resto son directivas si son baratas y nits si no.
- Un movimiento de judo DENTRO de las superficies del issue se aplica ahora:
  viaja literal al `resume` de Codex como directiva obligatoria. Uno que cruza a
  superficies congeladas o compartidas NUNCA entra en el PR del issue: `bd
  create` de refactor o PR de descomposición (Fase 0.6).
- Una sola ronda: tras el `resume` que aplica las directivas no se relanza la
  lente completa; solo se verifica que las directivas quedaron aplicadas.
- Lo canónico que la lente descubra («X ya existe en data-access, no escribir
  bespoke») va a `bd remember` y, si es regla del repo, al wiki o a la guía de UI.

**Asignación de modelo por lente (jueces).** La potencia de las lentes
viene de que fallen distinto; el modelo es una fuente de correlación tan real
como los insumos. Reparto fijo, independiente de quién tecleó:

| Lente | Modelo | Effort | Por qué |
|---|---|---|---|
| Spec | Sonnet 5 | n/a | Checklist con insumos completos, no juicio profundo |
| Código (**Juez A**) | GPT-6 Astra vía `codex exec` en modo lectura (`-s read-only`) | `high` | Revisión profunda a tarifa plana; recibe SOLO el árbol resultante |
| Estructura (**Juez B**) | Fable 5.1 (u Opus 5 como subagente) | n/a | Revisión independiente y cross-model; aplica la rúbrica thermo-nuclear |
| Seguridad | Fable 5.1, personalmente | n/a | Nunca delegada |

La decorrelación se garantiza porque los dos jueces son de familias distintas
entre sí: al menos uno nunca comparte familia con la mano que tecleó. Si tecleó
Codex, el Juez B (Fable) es la lente cross-family; si tecleó Opus, lo es el Juez
A (Astra). Un juez de la misma familia que la mano no se elimina — su valor
está en los insumos distintos (árbol sin diff, sin transcript). Corolarios: (a)
las ediciones directas de Claude no-triviales (fixes de arbitraje, regex sobre
archivos) reciben la pasada del Juez A — es justo donde se cuelan los errores
tontos porque es el único código sin lente; (b) para PRs que tocan
RLS/migraciones/auth, una lente adicional barata (Sonnet/Haiku) con prompt de
refutación («demuestra que esta política filtra datos») agrega una familia de
error más por centavos — condicional a la superficie, no siempre.

Ejecutar personalmente los gates: tests focalizados, lint **con la config real del
proyecto** (no la raíz — `npx eslint -c apps/<app>/eslint.config.mjs <files>`; la
salida de nx trunca igual en éxito y fallo), build y tests SQL. El reporte de Codex
es publicidad, no prueba. Gates ampliados por superficie: si el cambio toca
**contratos compartidos** (schemas zod, tipos que parsean varios clientes), el gate
es el conjunto COMPLETO de consumidores (web + data-access + mobile + build de
templates estricto — jest no typecheckea templates ni fixtures ajenos; el build y
los parsers zod sí revientan). Tras CADA rebase, re-correr los tests focalizados
ANTES de push (fixtures vs schemas nuevos es la clase de rotura silenciosa).
Prettier/format SIEMPRE con el binario del repo (`node_modules/prettier` del
worktree), nunca un npx suelto — el gate de CI usa la versión pineada y las
opiniones difieren entre mayores. Cosecha a la bitácora del lote lo inesperado que
las lentes o los gates hayan revelado.

## Fase 4 — Evidencia visual (antes del PR)

- Web: Playwright (`@playwright/test` chromium) contra el dev server del worktree;
  el script vive DENTRO del worktree (resolución de módulos).
- Móvil: emulador + `adb exec-out screencap`; Metro desde el worktree; verifica cada
  captura LEYÉNDOLA (una pantalla equivocada invalida la evidencia).
- Cubre flujo feliz + al menos un estado de error/vacío.
- Empaqueta en `docs/evidence/<rama>/` con `NOTES.md` (tabla captura → qué demuestra).
- Si una pantalla no es alcanzable aún (entrada diferida al PR de cableo), decláralo
  en NOTES.md como promesa explícita y cúmplela en ese PR.

## Fase 5 — Publicar y supervisar

1. `/code-review` (fixed point = base de integración) antes de publicar.
2. Commit convencional; PR contra la rama de integración con issue, problema/solución,
   decisiones, migraciones, pruebas, evidencia, riesgos y rollback.
3. Monitor en background sobre `gh pr view/checks` (corta en CLEAN+APPROVED o
   fails>0). No hagas polling manual; sigue trabajando.
4. CodeRabbit: corrige lo válido (commit + respuesta con hash), rebate lo inválido con
   evidencia del repo, `@coderabbitai resolve`, espera re-aprobación. CI puede cazar
   lo que tus gates locales no cubrieron (specs de la otra plataforma, TZ) — al tocar
   código compartido, re-corre los specs de AMBAS plataformas.
   Patologías conocidas del revisor externo: (a) **rate limit** — detectar por el
   TEXTO del check ("rate limited"), no por su conclusion; re-trigger con
   `@coderabbitai review`. Si bloquea >1h con CI verde y revisión propia completa,
   NO hagas merge documentado: corre el **gate sustituto** — la lente estructura de
   Fase 3 (misma rúbrica `thermo-nuclear-code-quality-review`, mismo contrato de
   salida, mismo modelo decorrelacionado) sobre el diff completo del PR contra la
   base, o solo sobre el delta desde la ronda de Fase 3 (fixes de arbitraje +
   rebase) si esa ronda ya dio `APPROVE`. Merge solo con `APPROVE`; con `BLOCK`,
   atiende los bloqueadores como en Fase 3 y repite. Deja en el PR un comentario
   con el veredicto y el hash revisado (instrucción del 2026-08-15, lote PRD
   #1006); (b) **veredicto stale** — tras
   aplicar fixes, el CHANGES_REQUESTED puede quedar pegado (follow-ups COMMENTED +
   check en pass): dismiss de la review vía API con justificación y merge. Un
   monitor que solo mira `reviewDecision` no ve ninguna de las dos — vigilar
   también el estado del check y las reviews reales.
5. Merge (squash) solo con: revisión propia satisfactoria + CI verde + CodeRabbit
   atendido (o gate sustituto en `APPROVE`, ver 4a) + evidencia adjunta. Luego:
   cerrar issue, `bd close`, borrar rama y worktree, seguir con el siguiente SIN
   pausa.

## Rebases entre PRs seriales

- Rebase sobre la integración fresca antes de cada PR nuevo.
- **Conflicto no trivial → reconciliador neutral**: spawn de un agente fresco con
  `/resolving-merge-conflicts` cuyo único objetivo es la fusión fiel de ambos lados.
  Las partes involucradas resuelven mal por diseño — tú, con el contexto del issue
  cargado, tiendes a favorecer "tu" cambio. Los triviales (imports, línea adyacente)
  los resuelves tú.
- NUNCA `git add -A` durante un rebase (sella marcadores de conflicto).
- Los "keep-both" automáticos corrompen: rutas adyacentes fusionadas (reinsertar
  `},\n{`) y specs de contratos desbalanceados. Ante corrupción: `git checkout
  origin/<int> -- <archivo>` + re-aplicar el bloque limpio desde el diff del commit
  original.
- Nunca `git stash` a secas (pila compartida entre worktrees/sesiones).

## Cierre del lote

Todos los issues mergeados y cerrados — a MANO si la integración no es la rama
default (los `Closes #N` de un PR a `develop` no auto-cierran; solo la default lo
hace). Después: PR de cableo final (entradas diferidas + glosario + promesas de
evidencia pendientes), verificación de la rama de integración, cero
PRs/ramas/worktrees huérfanos propios (`git worktree prune`; no toques los ajenos)
**incluidas las ramas REMOTAS mergeadas** (`git push origin --delete`), matar
servidores/emulador, `bd dolt push` + `git push`, y resumen final por issue con
la **tabla de economía y salud de coordinación**:

| Métrica | Por qué importa |
|---|---|
| Rondas de `resume` de Codex | ¿El autogrill sobre/sub-especa? |
| Effort del worker por corrida (`low`…`ultra`) y cuelgues | ¿Un effort menor rinde igual en trabajo acotado? Hoy solo `xhigh` está probado (licitaciones 10/10); los cuelgues nunca se registraron junto al effort, así que siguen confundidos |
| Conflictos de rebase (meta: 0) | ¿Funcionó la congelación de superficies? |
| Fallos de CI por PR y su clase | ¿Qué no cubre el gate local? |
| Hallazgos por lente (spec/código/estructura/seguridad/CR/CI) | ¿Qué lente paga y cuál duplica? |
| LOC por issue y duración aproximada | ¿Qué clase de issue amerita worker más barato? |

Los números de coordinación (conflictos, fallos, LOC) son el diagnóstico del
harness, no del código: una tasa de conflictos que acelera es señal de
superficies mal congeladas u orden mal secuenciado, no de mala suerte. Al final,
migra lo no-obvio de la bitácora del lote a `bd remember` y descarta el archivo —
la bitácora es memoria de trabajo del lote, no del proyecto.
