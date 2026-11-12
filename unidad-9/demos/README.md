# Demos de la Unidad 9 · ArriendoWeb

Las tres demos de la unidad ocurren sobre **un solo proyecto**, `arriendo-web/`, y siguen la historia de las demos de la Unidad 8: *ArriendoWeb ya tiene reglas, un revisor y un guardián. ¿Cómo hacemos que otro equipo los tenga con un comando?*

`arriendo-web` es el **estado de la U8 con la gobernanza ya incorporada**: `TarifaBase` migrada (golden master), el hook `PostToolUse` de la U5, `ci.yml` y `claude.yml` (U6), `REVIEW.md` y el subagente `revisor` (U7), y de la U8 el `deny` para leer `.env`, el `deny` sobre `legado/`, los `ask` sobre el golden master, `curl` y `WebFetch`, y el hook `PreToolUse` con `.claude/hooks/guardian.sh`. Lo que se construye en vivo **no** viene incluido: se pega desde `insumos/`.

Historia: **1 Empaqueta → 2 Instala → 3 Súmale MCP**

| Demo | Lámina | Concepto | Qué se hace |
|---|---|---|---|
| 1 · Empaqueta lo que ya funciona | 15 | Playbook como código | Se pegan `plugin.json` y `hooks.json` en `plugins/arriendo-playbook/`. Claude Code copia el `revisor`, el `guardian.sh` y una plantilla de `AGENTS.md` dentro del plugin. Se valida con `claude plugin validate .` |
| 2 · Instálalo como otro equipo | 16 | Marketplace | Se pega `marketplace.json` en `arriendo-web/.claude-plugin/`. Desde una carpeta `otro-equipo/`, se agrega el marketplace local y se instala `arriendo-playbook@arriendo-vela`. El guardián bloquea leer el `.env` de `otro-equipo/`. |
| 3 · Súmale datos de solo lectura | 21 | Herramienta justa | Se pega `academy.mcp.json` como `.mcp.json` del plugin y se sube `version` a 1.1.0. `/mcp` muestra `claude-academy`; una búsqueda en Claude Academy trae enlaces y un pedido de escritura no tiene herramienta. |

> El paso a paso completo (prompts exactos, resultados esperados, commits y contingencias) está en las notas del instructor de la Unidad 9.

## Qué hay aquí

```
demos/
├── arriendo-web/                      ← proyecto de las 3 demos (estado inicial)
│   ├── AGENTS.md
│   ├── REVIEW.md                      ← U7
│   ├── ArriendoWeb.sln
│   ├── .claude/
│   │   ├── settings.json              ← U5 (PostToolUse) + U8 (deny, ask y PreToolUse)
│   │   ├── hooks/guardian.sh          ← U8
│   │   └── agents/                    ← analista-legado y revisor (U7)
│   ├── .github/workflows/             ← ci.yml y claude.yml (U6)
│   ├── legado/                        ← solo lectura
│   ├── migracion/tarifas-golden.csv
│   ├── src/  ·  tests/
└── insumos/                           ← se pegan en vivo
    ├── plugin.json                    → plugins/arriendo-playbook/.claude-plugin/plugin.json   (demo 1)
    ├── hooks.json                     → plugins/arriendo-playbook/hooks/hooks.json             (demo 1)
    ├── marketplace.json               → arriendo-web/.claude-plugin/marketplace.json           (demo 2)
    ├── academy.mcp.json               → plugins/arriendo-playbook/.mcp.json                    (demo 3)
    └── env-falso.txt                  → otro-equipo/.env y arriendo-web/.env                    (antes de la demo 2)
```

`env-falso.txt` trae **solo valores inventados**. Se guarda con otro nombre para que este repo público no tenga un `.env`.

## Cómo prepararlas

1. Copia la carpeta `arriendo-web/` a una carpeta de trabajo **fuera** de tu clon de este repo, para que tenga su propio historial de Git.
2. Ábrela en Rider con `ArriendoWeb.sln` y compila. En la terminal, `dotnet test` debe dar **20 tests en verde**.
3. Crea el repositorio y el primer commit en `main`:

   ```bash
   git init -b main
   git add .
   git commit -m "chore: estado inicial de arriendo-web para la U9"
   ```

4. Copia `insumos/env-falso.txt` a la raíz de tu copia con el nombre `.env`. `git status` no debe mostrarlo: lo ignora `.gitignore`.
5. Crea la carpeta `otro-equipo/` **al lado** de tu copia de `arriendo-web` (no adentro) y copia ahí también `env-falso.txt` con el nombre `.env`. Representa a otro equipo de la BU.
6. Comprueba la versión de Claude Code: `claude --version` (2.1.281 o superior, para que `claude plugin validate` revise el `.mcp.json`). Si es menor: `claude update`.
7. Ensaya las tres demos y anota tus resultados. Los puntos de restauración (los commits de cada demo) los creas tú al ensayar.
8. Para repetir desde cero: en `otro-equipo/`, desinstala el plugin y quita el marketplace desde `/plugin`; luego borra tu carpeta de trabajo y vuelve a copiarla desde aquí.

Las demos son **locales**: el marketplace es una carpeta de tu equipo, sin GitHub. La única conexión a internet es la de la demo 3 (Claude Academy).

## Regla de las demos

Los archivos de configuración (`plugin.json`, `hooks.json`, `marketplace.json` y `.mcp.json`) se **pegan a mano** desde `insumos/`, no se le piden a Claude: así la demo es repetible. A Claude Code solo se le pide copiar lo que ya existe (el revisor, el guardián y la plantilla de `AGENTS.md`). Usa solo el `.env` falso.

## Licencias

- Claude Pro (incluye Claude Code). Plugins, marketplaces, hooks y MCP funcionan en cualquier plan.
- JetBrains Rider y .NET 10 SDK (solo para el `dotnet test` de la preparación).
- El MCP de Claude Academy es público y no pide cuenta.
- `guardian.sh` es bash: en Windows, Claude Code corre los hooks con Git Bash.

*(Verificar en tu equipo: el C# no fue compilado al preparar este material; `guardian.sh` como hook de plugin no se probó en Windows.)*
