# Demos de la Unidad 10 · ArriendoWeb

Las tres demos de la unidad ocurren sobre **un solo proyecto**, `arriendo-web/`, y cierran la historia de las demos de las unidades 5 a 9: *ArriendoWeb ya migró, prueba, revisa, gobierna y comparte su forma de trabajar. ¿Vale lo que cuesta?*

`arriendo-web` es el **estado al final de las demos de la U9**: `TarifaBase` migrada (golden master), `ci.yml` y `claude.yml` (U6), `REVIEW.md` y el subagente `revisor` (U7), el `deny`, los `ask` y el hook `PreToolUse` con `guardian.sh` (U8), y el plugin `arriendo-playbook` 1.1.0 con su marketplace `arriendo-vela` (U9). La U10 no toca el código: todo lo nuevo queda en `docs/roi/`, y lo que se construye en vivo **no** viene incluido: se pega desde `insumos/`.

Historia: **1 Mide → 2 Calcula → 3 Cuenta**

| Demo | Lámina | Concepto | Qué se hace |
|---|---|---|---|
| 1 · La métrica trampa | 7 | Medir lo que importa | Se pega `metricas-equipos.csv` en `docs/roi/`. Claude Code responde primero solo con las líneas aceptadas y luego con las métricas DORA, los defectos y el retrabajo. Deja `docs/roi/lectura-metricas.md`. |
| 2 · ROI con supuestos | 11 | ROI con supuestos | Se pega `supuestos-roi.md` en `docs/roi/`. Claude Code arma `docs/roi/modelo-roi.md` con escenarios conservador y optimista, y luego la sensibilidad con el ahorro a la mitad. |
| 3 · El informe en 1 página | 14 | Contar para decidir | Se pega `informe-malo.md` en `docs/roi/`. Claude Code lo critica con las 5 franjas y lo reescribe en `docs/roi/informe-ejecutivo.md`, con una línea de Diligencia. |

Las tres demos se hacen con **Claude Pro** y Claude Code. Los datos son **ficticios**.

> El paso a paso completo (prompts exactos, resultados esperados y commits) está en las notas del instructor de la Unidad 10.

## Qué hay aquí

```
demos/
├── arriendo-web/                       ← proyecto de las 3 demos (estado inicial)
│   ├── AGENTS.md  ·  REVIEW.md  ·  ArriendoWeb.sln
│   ├── .claude/                        ← settings.json, hooks/guardian.sh, agents/ (U5, U7, U8)
│   ├── .claude-plugin/marketplace.json ← marketplace arriendo-vela (U9)
│   ├── plugins/arriendo-playbook/      ← plugin 1.1.0 con revisor, guardián, plantilla y MCP (U9)
│   ├── .github/workflows/              ← ci.yml y claude.yml (U6)
│   ├── legado/                         ← solo lectura
│   ├── migracion/tarifas-golden.csv
│   └── src/  ·  tests/
└── insumos/                            ← se pegan en vivo en arriendo-web/docs/roi/
    ├── metricas-equipos.csv            (demo 1) 2 equipos × 8 semanas
    ├── supuestos-roi.md                (demo 2) horizonte 6 meses, 8 devs
    └── informe-malo.md                 (demo 3)
```

## Cómo prepararlas

1. Copia la carpeta `arriendo-web/` a una carpeta de trabajo **fuera** de tu clon de este repo, para que tenga su propio historial de Git.
2. Ábrela en Rider con `ArriendoWeb.sln`. Las demos no compilan ni cambian código, así que compilar es opcional.
3. Crea el repositorio y el primer commit en `main`:

   ```bash
   git init -b main
   git add .
   git commit -m "chore: estado inicial de arriendo-web para la U10"
   ```

4. Ten `insumos/` a mano: cada demo empieza copiando un archivo a `arriendo-web/docs/roi/` (la carpeta se crea en la demo 1).
5. Ensaya las tres demos y anota tus resultados. Los puntos de restauración (los commits de cada demo) los creas tú al ensayar.
6. Para repetir desde cero: borra tu carpeta de trabajo y vuelve a copiarla desde aquí.
