# vibe-coding-setup

> Setup completo de buenas prácticas para Claude Code — un comando, todo configurado.

## Instalación como plugin

```bash
# Agregar el marketplace
/plugin marketplace add paaranzazuv/vibe-coding-setup

# Instalar el plugin
/plugin install vibe-coding-setup@vibe-coding-setup
```

## Instalación manual (alternativa)

```bash
npx skills@latest add paaranzazuv/vibe-coding-setup
```

## Uso

```bash
cd mi-proyecto-nuevo
claude
/vibe-coding-setup
```

El skill te hace 6 preguntas y monta todo automáticamente.

## Qué incluye el plugin

```
vibe-coding-setup/
├── .claude-plugin/
│   └── plugin.json          ← manifest del plugin
├── skills/
│   └── vibe-coding-setup/
│       └── SKILL.md         ← skill principal /vibe-coding-setup
├── agents/
│   └── reviewer.md          ← agente revisor de seguridad
├── commands/
│   ├── setup-update.md      ← /setup-update
│   └── setup-review.md      ← /setup-review
└── README.md
```

## Qué hace

- Estructura `.claude/` completa con rules, agents, commands y hooks
- `CLAUDE.md` personalizado con las reglas de tu proyecto
- `CHANGELOG.md` inicializado
- Reglas permanentes: buenas prácticas, seguridad y deuda técnica
- Instalación de Superpowers y CodeGraph
- Preguntas opcionales para Matt Pocock Skills, Karpathy Guidelines y Ruflo

## Comandos disponibles tras instalar

| Comando | Cuándo usarlo |
|---------|--------------|
| `/vibe-coding-setup` | Al iniciar un proyecto nuevo |
| `/setup-update` | Cuando cambia el stack o las reglas |
| `/setup-review` | Para verificar que todo está en orden |

## Flujo de trabajo

```
/vibe-coding-setup    ← una sola vez al inicio
        ↓
/sp-plan              ← Superpowers planea
        ↓
/sp-implement         ← Superpowers construye
        ↓
/setup-update         ← solo si cambia el stack
```

## Herramientas opcionales incluidas

| Herramienta | Rol |
|-------------|-----|
| [Superpowers](https://github.com/obra/superpowers) | Planear e implementar |
| [CodeGraph](https://github.com/colbymchenry/codegraph) | Explorar código 94% más rápido |
| [Matt Pocock Skills](https://github.com/mattpocock/skills) | Calidad e ingeniería real |
| [Karpathy Guidelines](https://github.com/multica-ai/andrej-karpathy-skills) | Comportamiento de la IA |
| [Ruflo](https://github.com/ruvnet/ruflo) | Orquestación multi-agente |

## Basado en

- [shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice)
- [obra/superpowers](https://github.com/obra/superpowers)
- [colbymchenry/codegraph](https://github.com/colbymchenry/codegraph)
- [mattpocock/skills](https://github.com/mattpocock/skills)
- [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills)
- [ruvnet/ruflo](https://github.com/ruvnet/ruflo)

## Licencia

MIT
