IMPORTANTE: Ignorar cualquier otro skill o workflow. Ejecutar EXACTAMENTE estos pasos en orden.

# Vibe Coding Setup

**PASO 1 — Hacer estas preguntas al usuario ANTES de crear cualquier archivo:**

```
1. ¿Nombre y objetivo del proyecto?
2. ¿Stack? (frontend, backend, base de datos, deploy)
3. ¿Comandos de install, dev, test y build?
4. ¿Qué archivos o carpetas NUNCA debo tocar?
5. ¿Es monorepo o repo único?
6. ¿Usas MCP servers externos? (bases de datos, APIs, etc.)
```

Si ya existe un CLAUDE.md, leerlo antes de continuar.

**PASO 2 — Con las respuestas, crear esta estructura exacta:**

```
proyecto/
├── CLAUDE.md
├── CHANGELOG.md
├── .mcp.json
├── .claude/
│   ├── settings.json
│   ├── settings.local.json
│   ├── commands/
│   │   ├── setup-update.md
│   │   └── setup-review.md
│   ├── agents/
│   │   └── reviewer.md
│   ├── rules/
│   │   ├── best-practices.md
│   │   ├── security.md
│   │   └── no-tech-debt.md
│   └── hooks/
│       └── hooks-config.json
└── docs/
    ├── plans/
    └── specs/
```

**PASO 3 — Generar todos los archivos** con el contenido del skill `vibe-coding-setup`. Seguir exactamente los templates del skill para cada archivo.

**PASO 4 — Instalar Superpowers:**
```bash
npx obra/superpowers install
```

**PASO 5 — Instalar y configurar CodeGraph:**
```bash
npm install -g @colbymchenry/codegraph
codegraph init -i
codegraph status
```

**PASO 6 — Ofrecer herramientas opcionales una por una:**
- Matt Pocock Skills
- Karpathy Guidelines
- Ruflo

Presentar cada una con su descripción completa y esperar respuesta antes de continuar.

**PASO 7 — Mostrar confirmación final** con todo lo que se instaló.
