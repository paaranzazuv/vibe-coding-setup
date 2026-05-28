<div align="center">

# 🛠️ vibe-coding-setup

**Setup completo de buenas prácticas para Claude Code**  
Un comando. Todo configurado. Listo para construir.

[![Claude Code](https://img.shields.io/badge/Claude_Code-Plugin-D97757?style=flat-square&logo=anthropic&logoColor=white)](https://code.claude.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/paaranzazuv/vibe-coding-setup?style=flat-square&color=gold)](https://github.com/paaranzazuv/vibe-coding-setup/stargazers)

</div>

---

## ¿Qué es?

Un plugin para Claude Code que monta toda la estructura de buenas prácticas antes de empezar cualquier proyecto. Te hace 6 preguntas y genera automáticamente el `CLAUDE.md`, las reglas de seguridad, la estructura `.claude/` y conecta las herramientas del stack.

Basado en los mejores repos de la comunidad Claude Code en 2026.

---

## Instalación

Dentro de Claude Code, ejecutar en orden:

```
/plugin marketplace add paaranzazuv/vibe-coding-setup
! claude plugin install vibe-coding-setup@vibe-coding-setup
```

Reiniciar Claude Code después de instalar.

## Actualización

```
/vibe-update
```

O directamente:

```
! claude plugin update vibe-coding-setup@vibe-coding-setup
```

---

## Uso

```bash
cd mi-proyecto-nuevo
claude
/vibe-coding-setup
```

---

## Qué genera

```
proyecto/
├── CLAUDE.md                        ← memoria + reglas del proyecto
├── CHANGELOG.md                     ← historial de cambios
├── .mcp.json                        ← configuración MCP servers
└── .claude/
    ├── settings.json                ← configuración del equipo
    ├── settings.local.json          ← overrides personales
    ├── commands/
    │   ├── setup-update.md          ← /setup-update
    │   └── setup-review.md          ← /setup-review
    ├── agents/
    │   └── reviewer.md              ← revisor de seguridad y deuda técnica
    ├── rules/
    │   ├── best-practices.md        ← ⭐ buenas prácticas permanentes
    │   ├── security.md              ← ⭐ prohibiciones irrevocables
    │   └── no-tech-debt.md          ← ⭐ prevención de deuda técnica
    └── hooks/
        └── hooks-config.json
```

---

## Reglas permanentes incluidas

Las reglas en `.claude/rules/` están **siempre activas** — todos los agentes y herramientas externas las respetan automáticamente.

| Archivo | Qué hace |
|---------|---------|
| `best-practices.md` | Arquitectura, tests obligatorios, git, contexto |
| `security.md` | Prohibiciones absolutas — secrets, auth, pagos |
| `no-tech-debt.md` | Prevención activa de deuda en cada tarea |

---

## Herramientas opcionales

Al final del setup el plugin pregunta una a una si quieres instalar cada herramienta. Tú decides.

| Herramienta | Qué hace |
|-------------|---------|
| [Superpowers](https://github.com/obra/superpowers) | Planear e implementar features |
| [CodeGraph](https://github.com/colbymchenry/codegraph) | Explorar código 94% más rápido |
| [Matt Pocock Skills](https://github.com/mattpocock/skills) | Calidad e ingeniería real |
| [Karpathy Guidelines](https://github.com/multica-ai/andrej-karpathy-skills) | Comportamiento de la IA |
| [Ruflo](https://github.com/ruvnet/ruflo) | Orquestación multi-agente |

---

## Flujo de trabajo

```
/vibe-coding-setup     → una sola vez al iniciar el proyecto
        ↓
/sp-plan               → Superpowers planea cada feature
        ↓
/sp-implement          → Superpowers construye
        ↓
/setup-update          → cuando cambia el stack o las reglas
```

---

## Comandos disponibles

| Comando | Cuándo usarlo |
|---------|--------------|
| `/vibe-setup` | Al iniciar un proyecto nuevo |
| `/vibe-update` | Para actualizar el plugin a la última versión |
| `/setup-update` | Cuando cambia el stack o las reglas del proyecto |
| `/setup-review` | Para verificar que todo está en orden |

---

## Basado en

| Repo | Contribución |
|------|-------------|
| [shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice) | Estructura y buenas prácticas |
| [mattpocock/skills](https://github.com/mattpocock/skills) | Ingeniería real y TDD |
| [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) | Comportamiento de la IA |
| [colbymchenry/codegraph](https://github.com/colbymchenry/codegraph) | Exploración de código |
| [obra/superpowers](https://github.com/obra/superpowers) | Planificación e implementación |
| [ruvnet/ruflo](https://github.com/ruvnet/ruflo) | Orquestación multi-agente |

---

<div align="center">

MIT License · Hecho para la comunidad de Claude Code

</div>
