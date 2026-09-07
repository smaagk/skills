# skills

Skills públicas para Claude Code (y harnesses compatibles con `SKILL.md`).

| Skill | Qué hace |
|---|---|
| [`batch-conductor`](skills/batch-conductor/SKILL.md) | Conduce uno o varios issues de principio a fin: autogrill, spec congelada, implementación delegada (Codex / Opus), revisión en lentes decorrelacionadas (Juez A Astra, Juez B Fable), evidencia visual, PR/CI/CodeRabbit, merge y cierre. |

## Instalar

Copia la carpeta de la skill a `.claude/skills/` de tu repo (o a `~/.claude/skills/` para uso global):

```bash
git clone https://github.com/smaagk/skills.git
cp -r skills/skills/batch-conductor .claude/skills/
```

## Dependencias de `batch-conductor`

La skill compone otras que asume presentes y no reimplementa: `/grill-with-docs`, `/codex-first`, `/code-review`, `/resolving-merge-conflicts`, y la rúbrica `thermo-nuclear-code-quality-review`. Está escrita para un flujo con Codex CLI (GPT-6 Astra) como worker a tarifa plana y Claude como arquitecto, revisor y única mano en git/GitHub.

## Licencia

MIT
