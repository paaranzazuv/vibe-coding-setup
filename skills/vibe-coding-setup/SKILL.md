---
name: vibe-coding-setup
description: Monta el stack completo de vibe coding en un proyecto nuevo. Instala y configura todo de una sola vez: estructura .claude/, reglas de buenas prácticas, seguridad y deuda técnica, Superpowers y CodeGraph. Úsalo con frases como "prepara mi proyecto", "monta todo", "setup inicial", "quiero empezar un proyecto con Claude Code".
---

# Vibe Coding Setup — Todo en Uno
> shanraisshan/claude-code-best-practice · obra/superpowers · colbymchenry/codegraph

**REGLA ABSOLUTA: Completar este setup ANTES de planear o escribir código.**

---

## PASO 1 — Entrevistar al usuario

Hacer estas preguntas antes de crear cualquier archivo:

```
1. ¿Nombre y objetivo del proyecto?
2. ¿Stack? (frontend, backend, base de datos, deploy)
3. ¿Comandos de install, dev, test y build?
4. ¿Qué archivos o carpetas NUNCA debo tocar?
5. ¿Es monorepo o repo único?
6. ¿Usas MCP servers externos? (bases de datos, APIs, etc.)
```

Si ya existe un CLAUDE.md, leerlo antes de continuar.

---

## PASO 2 — Estructura completa de carpetas

Crear esta estructura exacta:

```
proyecto/
│
├── CLAUDE.md                              ← memoria + reglas permanentes
├── CHANGELOG.md                           ← historial global de cambios
├── .mcp.json                              ← MCP servers del proyecto
│
├── .claude/
│   ├── settings.json                      ← configuración del equipo (git-tracked)
│   ├── settings.local.json                ← overrides personales (git-ignored)
│   │
│   ├── commands/
│   │   ├── setup-update.md                ← /setup-update
│   │   └── setup-review.md                ← /setup-review
│   │
│   ├── agents/
│   │   └── reviewer.md                    ← revisor de seguridad y deuda técnica
│   │
│   ├── skills/
│   │   └── vibe-coding-best-practices/
│   │       └── SKILL.md                   ← referencia de buenas prácticas
│   │
│   ├── rules/                             ← SIEMPRE ACTIVAS — todos los agentes las respetan
│   │   ├── best-practices.md              ← ⭐ buenas prácticas obligatorias
│   │   ├── security.md                    ← ⭐ prohibiciones irrevocables
│   │   └── no-tech-debt.md               ← ⭐ prevención de deuda técnica
│   │
│   └── hooks/
│       └── hooks-config.json
│
└── docs/
    ├── plans/                             ← planes por feature (Superpowers)
    └── specs/                             ← specs antes de implementar
```

> `/plan`, `/review` e `/implement` los maneja **Superpowers**.
> Este skill solo crea `/setup-update` y `/setup-review`.

---

## PASO 3 — Generar todos los archivos

### `CLAUDE.md`

```markdown
<!--
@file       CLAUDE.md
@purpose    Memoria del proyecto — reglas permanentes para Claude Code, Superpowers y CodeGraph
@security   CRÍTICO
@updated    [fecha de hoy]
-->

# [NOMBRE DEL PROYECTO]
[descripción en 1-2 líneas]

## Repository Overview
[qué hace, para quién, qué problema resuelve]

## Stack
- Frontend:   [valor]
- Backend:    [valor]
- Base datos: [valor]
- Deploy:     [valor]

## Comandos esenciales
- install: [comando]
- dev:     [comando]
- test:    [comando]
- build:   [comando]

## Estructura principal
[árbol de carpetas con descripción de cada una]

## Convenciones
- [naming, formato, patrones usados]
- Conventional Commits: feat: fix: refactor: docs: security: test:

## Decisiones de arquitectura
- [decisiones ya tomadas — no re-inventar]

## ⛔ Off-limits — NO MODIFICAR SIN APROBACIÓN EXPLÍCITA
- /[carpeta-auth]/**
- /[carpeta-pagos]/**
- .env y variables de entorno
- Archivos *.migration.*

<important if="security">
NUNCA tocar auth, pagos o migraciones sin aprobación explícita del usuario.
</important>

<important if="migrations">
Terminar siempre las migraciones antes de empezar features nuevas.
Migraciones a medias generan bugs silenciosos en sesiones futuras.
</important>

<important if="best-practices">
Antes de implementar cualquier cosa leer:
- .claude/rules/best-practices.md
- .claude/rules/security.md
- .claude/rules/no-tech-debt.md
Estas reglas tienen prioridad sobre Superpowers y cualquier agente externo.
</important>

<important if="codegraph">
Si existe .codegraph/ en el proyecto, NUNCA explorar archivos manualmente.
Siempre lanzar un Explore agent con codegraph_explore como herramienta primaria.
Solo usar codegraph_search, codegraph_callers, codegraph_impact en la sesión principal.
</important>

## Workflow
- Plan mode siempre para tareas complejas
- /compact manual al 50% de contexto
- Commits al completar cada tarea
- Esc Esc o /rewind si algo sale mal
- ultrathink para decisiones arquitectónicas

## Historial
Ver CHANGELOG.md en la raíz.
```

---

### `CHANGELOG.md`

```markdown
# Changelog

Formato: [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/)
Versionado: [SemVer](https://semver.org/lang/es/)

## [No publicado]

## [0.1.0] - [fecha de hoy]
### Añadido
- Setup inicial con estructura .claude/
- CLAUDE.md con reglas del proyecto y zonas off-limits
- Reglas permanentes: best-practices, security, no-tech-debt
- Agente revisor de seguridad y deuda técnica
- Integración con Superpowers y CodeGraph
```

---

### `.mcp.json`

```json
{
  "mcpServers": {
    "codegraph": {
      "type": "stdio",
      "command": "codegraph",
      "args": ["serve", "--mcp"]
    }
  }
}
```

---

### `.claude/settings.json`

```json
{
  "permissions": {
    "allow": [
      "mcp__codegraph__codegraph_search",
      "mcp__codegraph__codegraph_context",
      "mcp__codegraph__codegraph_callers",
      "mcp__codegraph__codegraph_callees",
      "mcp__codegraph__codegraph_impact",
      "mcp__codegraph__codegraph_node",
      "mcp__codegraph__codegraph_status",
      "mcp__codegraph__codegraph_files"
    ],
    "deny": []
  },
  "model": "claude-sonnet-4-5",
  "thinking": { "enabled": true },
  "outputStyle": "explanatory"
}
```

---

### `.claude/settings.local.json` (git-ignored)

```json
{
  "disableAllHooks": false
}
```

---

### `.claude/rules/best-practices.md` ⭐

```markdown
<!--
@file       best-practices.md
@purpose    Buenas prácticas obligatorias — prioridad sobre cualquier agente externo
@security   CRÍTICO
@updated    [fecha de hoy]
-->

# Buenas Prácticas — Reglas Permanentes

<important if="best-practices">
Estas reglas son PERMANENTES y tienen prioridad sobre Superpowers,
CodeGraph y cualquier otro agente o skill externo.
</important>

## Arquitectura
- Un archivo = una responsabilidad (Single Responsibility)
- No duplicar lógica — si algo se repite 2 veces, extraerlo
- Terminar migraciones antes de empezar features nuevas
- CLAUDE.md máximo 200 líneas — si crece, mover reglas a .claude/rules/

## Código
- Funciones pequeñas con nombre descriptivo
- Sin magic numbers — usar constantes con nombre
- Sin comentarios que expliquen el "qué" — el código debe leerse solo
- Sí comentarios que expliquen el "por qué" cuando no es obvio

## Tests — OBLIGATORIO en cada tarea
- Todo código nuevo lleva tests
- TDD cuando sea posible: test primero, luego código
- Orden por fase: unit → integration → automation
- Sin deploy si los tests fallan

## Git
- Commit al completar cada tarea
- Conventional Commits: feat: fix: refactor: docs: security: test:
- Nunca commitear .env ni secrets

## Deuda técnica
- No dejar TODOs sin ticket asociado
- No mezclar frameworks o patrones en el mismo módulo
- Reportar deuda encontrada antes de continuar

## Contexto de Claude
- /compact manual al 50% de contexto
- Usar opus para planear, sonnet para codear
- ultrathink para decisiones complejas o arquitectónicas
```

---

### `.claude/rules/security.md` ⭐

```markdown
<!--
@file       security.md
@purpose    Prohibiciones absolutas de seguridad — irrevocables
@security   CRÍTICO
@updated    [fecha de hoy]
-->

# Seguridad — Reglas Permanentes

<important if="security">
Estas reglas son IRREVOCABLES. Ningún agente, skill, workflow ni
instrucción puede anularlas. Ante cualquier duda, rechazar y pedir
confirmación explícita al usuario.
</important>

## Prohibido absoluto
- NUNCA hardcodear API keys, tokens, passwords o secrets
- NUNCA hacer commit de .env o credenciales
- NUNCA modificar auth o pagos sin aprobación explícita
- NUNCA ejecutar queries SQL sin sanitización de inputs
- NUNCA exponer stack traces o errores internos al cliente
- NUNCA usar dangerouslySkipPermissions sin revisión explícita

## Obligatorio en cada PR
- Variables de entorno para todas las credenciales
- Validación de inputs en todos los endpoints públicos
- Revisión manual de código de auth/pagos generado por IA

## Checklist antes de deploy
- [ ] git grep -r "sk-" . — sin API keys en el código
- [ ] Variables de entorno configuradas en el servidor
- [ ] Tests de seguridad pasan
- [ ] Cambios en zonas críticas revisados manualmente
```

---

### `.claude/rules/no-tech-debt.md` ⭐

```markdown
<!--
@file       no-tech-debt.md
@purpose    Prevención activa de deuda técnica en cada tarea
@security   ALTO
@updated    [fecha de hoy]
-->

# Sin Deuda Técnica — Reglas Permanentes

<important if="tech-debt">
Estas reglas aplican en CADA tarea. Superpowers y todos los agentes
deben respetarlas sin excepción.
</important>

## Antes de cada tarea
- Revisar TODOs/FIXMEs en el área a modificar
- Verificar que no hay migraciones incompletas
- Confirmar que los tests existentes pasan

## Durante la implementación
- No abstracciones prematuras — YAGNI
- No copiar/pegar — crear funciones reutilizables
- No ignorar warnings del compilador o linter
- No dejar console.log o prints de debug

## Al terminar cada tarea
- Tests pasan sin errores
- Sin TODOs nuevos sin ticket
- El código sigue los patrones existentes del proyecto
- Deuda encontrada → documentar en docs/techdebt-[fecha].md

## Señales de alerta a reportar
- Código duplicado en más de 2 lugares
- Función con más de 50 líneas
- Archivo con más de 300 líneas
- Cobertura menor al 80% en módulos críticos
- Dependencias con vulnerabilidades conocidas
```

---

### `.claude/agents/reviewer.md`

```markdown
<!--
@file       reviewer.md
@purpose    Agente revisor de seguridad y deuda técnica — contexto aislado
@security   ALTO
@updated    [fecha de hoy]
-->

---
name: reviewer
description: Revisar código buscando vulnerabilidades de seguridad y deuda técnica. Invocar PROACTIVAMENTE después de cada implementación significativa o antes de PR. Corre en contexto aislado para no contaminar la sesión principal.
model: sonnet
tools: Read, Grep, Glob
context: fork
---

Eres un staff engineer senior especializado en seguridad y calidad.

Antes de revisar, leer:
- .claude/rules/security.md
- .claude/rules/no-tech-debt.md
- .claude/rules/best-practices.md

Reportar por severidad: CRÍTICO / ALTO / MEDIO / BAJO.
Nunca modificar archivos — solo analizar y reportar.

## Gotchas
- Secrets hardcodeados aunque parezcan placeholders
- Migraciones incompletas o entremezcladas con features
- TODOs sin ticket = deuda técnica no reconocida
- Código que viola single responsibility aunque "funcione"
- console.log o prints olvidados en producción
```

---

### `.claude/commands/setup-update.md`

```markdown
Actualizar la estructura de setup cuando cambia el proyecto:
1. Leer CLAUDE.md actual
2. Preguntar qué cambió (stack, módulos, restricciones nuevas)
3. Actualizar CLAUDE.md con los cambios
4. Actualizar .claude/rules/ si cambian las reglas
5. Actualizar @updated en archivos modificados
6. Añadir entrada en CHANGELOG.md
7. Re-indexar CodeGraph si cambió la estructura: codegraph sync
```

---

### `.claude/commands/setup-review.md`

```markdown
Revisar que el setup esté completo y actualizado:
1. Verificar que existen best-practices.md, security.md y no-tech-debt.md en .claude/rules/
2. Verificar que CLAUDE.md tiene off-limits y <important> tags
3. Verificar que .gitignore protege .env y settings.local.json
4. Verificar que .mcp.json tiene codegraph configurado
5. Verificar que .codegraph/ existe (CodeGraph inicializado)
6. Reportar qué falta o está desactualizado
7. NO modificar nada — solo reportar
```

---

### `.claude/hooks/hooks-config.json`

```json
{
  "hooks": {
    "Stop": [],
    "PostToolUse": [],
    "PreToolUse": [],
    "TaskCompleted": []
  }
}
```

---

### `.gitignore` (agregar si no existe)

```
# Claude Code
.claude/settings.local.json
.claude/hooks/hooks-config.local.json

# Secrets
.env
.env.local
.env.*.local
*.pem
*.key

# Logs
*.log
npm-debug.log*
```

---

## PASO 4 — Instalar Superpowers

Después de crear todos los archivos, ejecutar:

```bash
# Instalar Superpowers globalmente
npx obra/superpowers install

# O seguir las instrucciones del repo
# github.com/obra/superpowers
```

Verificar que Superpowers detecta los archivos de `.claude/rules/` — los cargará automáticamente en cada sesión.

---

## PASO 5 — Instalar y configurar CodeGraph

```bash
# 1. Instalar CodeGraph globalmente
npm install -g @colbymchenry/codegraph

# 2. Inicializar e indexar el proyecto actual
codegraph init -i

# 3. Verificar que el índice se creó correctamente
codegraph status
```

Confirmar que se creó la carpeta `.codegraph/` en el proyecto.

> CodeGraph se auto-actualiza con cada cambio de archivo.
> No requiere configuración adicional.

---

## PASO 6 — Herramientas opcionales

Antes de terminar, presentar cada herramienta una a una con su explicación completa. Esperar respuesta antes de continuar con la siguiente. Sin recomendar ni advertir — solo informar. El developer decide.

---

### Pregunta 1 — Matt Pocock Skills

Presentar exactamente así:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 MATT POCOCK SKILLS — github.com/mattpocock/skills
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Qué es:
  Skills de Matt Pocock, creador de Total TypeScript.
  Son patrones de ingeniería usados en proyectos reales,
  no vibe coding.

Qué incluye:
  /grill-with-docs → antes de cada feature, Claude te
    interroga sobre el plan hasta que no quede ninguna
    ambigüedad. Actualiza un glosario del proyecto
    (CONTEXT.md) y registra decisiones importantes.

  /tdd → construye código escribiendo el test primero,
    luego el código mínimo para pasarlo, luego limpia.
    Un test a la vez. Nunca todos los tests de golpe.

  /diagnose → cuando algo falla, sigue un loop:
    reproducir → minimizar → hipotetizar → corregir.

  /improve-codebase-architecture → analiza el proyecto
    y sugiere cómo mejorar la estructura del código.

Archivos que agrega al proyecto:
  CONTEXT.md       → glosario del dominio del proyecto
  docs/adr/        → registro de decisiones de arquitectura

Cuándo tiene sentido:
  → Quieres que Claude entienda el vocabulario de tu proyecto
  → Te importa construir con tests desde el inicio
  → El proyecto va a durar más de un mes
  → Hay lógica de negocio compleja que puede malinterpretarse

Cuándo no lo necesitas:
  → Prototipo rápido de un día
  → Solo estás explorando una idea
  → Ya tienes tu propio proceso de testing

¿Lo instalamos? [sí / no]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Si sí → mostrar:
```bash
npx skills@latest add mattpocock/skills
# Luego dentro de Claude Code:
/setup-matt-pocock-skills
```

Si no → continuar sin comentarios.

---

### Pregunta 2 — Karpathy Guidelines

Presentar exactamente así:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧠 KARPATHY GUIDELINES — github.com/multica-ai/andrej-karpathy-skills
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Qué es:
  4 reglas de comportamiento para Claude derivadas de las
  observaciones de Andrej Karpathy (ex-director de IA de
  Tesla, cofundador de OpenAI) sobre cómo fallan los LLMs
  al codear.

Los 4 principios:
  1. Piensa antes de codear
     → Si algo no está claro, pregunta en vez de asumir
     → Muestra tradeoffs antes de elegir un camino
     → Para cuando hay confusión, no continúa adivinando

  2. Simplicidad primero
     → Mínimo código que resuelve el problema
     → Sin abstracciones que nadie pidió
     → Si 200 líneas pueden ser 50, reescribir

  3. Cambios quirúrgicos
     → Toca solo lo que se pidió
     → No "mejora" código que no tiene que ver con la tarea
     → Sigue el estilo existente aunque preferiría otro

  4. Ejecución orientada a metas
     → Define criterios de éxito antes de empezar
     → "Arregla el bug" → "escribe un test que lo reproduzca,
        luego hazlo pasar"

Cómo funciona:
  Se agrega como sección a .claude/rules/best-practices.md.
  Claude las lee automáticamente en cada sesión. No requiere
  instalación adicional ni comandos nuevos.

Cuándo tiene sentido:
  → Claude genera código innecesariamente complejo
  → Claude modifica cosas que no le pediste
  → Claude asume en vez de preguntar
  → Quieres resultados más predecibles

Cuándo no lo necesitas:
  → Tu flujo ya funciona bien y no tienes estos problemas
  → Prefieres que Claude tome iniciativa sin preguntar

¿Las agregamos? [sí / no]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Si sí → agregar a `.claude/rules/best-practices.md`:

```markdown
## Principios Karpathy

### Piensa antes de codear
- Si hay ambigüedad, pregunta en vez de asumir
- Presenta múltiples interpretaciones cuando existan
- Para y pide clarificación cuando algo no esté claro
- Muestra tradeoffs antes de elegir un camino

### Simplicidad primero
- Mínimo código que resuelve el problema
- Sin abstracciones para código de un solo uso
- Sin "flexibilidad" que nadie pidió
- Si 200 líneas pueden ser 50, reescribir

### Cambios quirúrgicos
- Tocar solo lo que se pidió
- No "mejorar" código adyacente no relacionado
- Seguir el estilo existente aunque lo harías diferente
- Si notas código muerto no relacionado, mencionar — no borrar

### Ejecución orientada a metas
- Definir criterios de éxito antes de empezar
- En vez de "arregla el bug" → "escribe un test que lo
  reproduzca, luego hazlo pasar"
- Para tareas múltiples: plan con verificación por paso
```

Si no → continuar sin comentarios.

---

### Pregunta 3 — Ruflo

Presentar exactamente así:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🌊 RUFLO — github.com/ruvnet/ruflo
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Qué es:
  Plataforma de orquestación de múltiples agentes para
  Claude Code. En vez de un solo Claude trabajando, tienes
  100+ Claudes especializados coordinándose como un equipo.

Qué agrega:
  → 100+ agentes especializados (coder, tester, reviewer,
    security, architect, docs...)
  → Memoria persistente entre sesiones (recuerda lo que
    aprendió en sesiones anteriores)
  → Aprendizaje automático (mejora con cada tarea)
  → 12 trabajadores en segundo plano que se activan solos
    (audit, optimize, testgaps, etc.)
  → Federación: agentes en diferentes máquinas u
    organizaciones que colaboran de forma segura
  → Soporte para múltiples modelos de IA (Claude, GPT,
    Gemini, Ollama) con failover automático
  → UI web en flo.ruv.io para chatear con los agentes

Cómo funciona:
  Un comando npx ruflo init instala todo. Después usas
  Claude Code normalmente — Ruflo enruta las tareas,
  aprende y coordina en segundo plano sin que hagas nada.

Cuándo tiene sentido:
  → Proyecto grande con muchos módulos en paralelo
  → Equipo de 2+ developers
  → Necesitas que los agentes recuerden contexto entre
    sesiones de trabajo
  → Quieres agentes corriendo tareas automáticas en fondo
  → Necesitas conectar múltiples modelos de IA

Cuándo no lo necesitas:
  → Proyecto personal o prototipo
  → Solo trabajas tú en el proyecto
  → No necesitas memoria entre sesiones
  → Tu proyecto tiene menos de 20 archivos

¿Lo instalamos? [sí / no]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Si sí → mostrar:
```bash
npx ruflo@latest init wizard
# O instalación rápida:
npx ruflo@latest init
```

Y agregar al `.mcp.json`:
```json
{
  "mcpServers": {
    "codegraph": {
      "type": "stdio",
      "command": "codegraph",
      "args": ["serve", "--mcp"]
    },
    "ruflo": {
      "type": "stdio",
      "command": "npx",
      "args": ["ruflo@latest", "mcp", "start"]
    }
  }
}
```

Si no → continuar sin comentarios.

---

## PASO 7 — Confirmación final

Mostrar solo lo que realmente se instaló:

```
╔══════════════════════════════════════════════════════╗
║           SETUP COMPLETO                             ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  📁 Base                                             ║
║  ✅ CLAUDE.md con reglas y off-limits                ║
║  ✅ CHANGELOG.md inicializado                        ║
║  ✅ .claude/ con commands, agents, rules, hooks      ║
║  ✅ docs/plans/ y docs/specs/ listos                 ║
║  ✅ .gitignore protegiendo secrets                   ║
║                                                      ║
║  ⭐ Reglas permanentes activas                       ║
║  ✅ best-practices.md                                ║
║  ✅ security.md (irrevocable)                        ║
║  ✅ no-tech-debt.md                                  ║
║  [✅ karpathy-guidelines — si eligió sí]             ║
║                                                      ║
║  🤝 Superpowers                                      ║
║  ✅ /sp-plan y /sp-implement listos                  ║
║                                                      ║
║  🔍 CodeGraph                                        ║
║  ✅ Instalado y proyecto indexado                    ║
║                                                      ║
║  [🎯 Matt Pocock — si eligió sí]                    ║
║  [✅ /grill-with-docs y /tdd listos]                 ║
║                                                      ║
║  [🌊 Ruflo — si eligió sí]                          ║
║  [✅ MCP server configurado]                         ║
║                                                      ║
╠══════════════════════════════════════════════════════╣
║  🚀 Flujo de trabajo:                                ║
║                                                      ║
║  /setup-review  → verificar que todo está en orden  ║
║  /sp-plan       → planear con Superpowers            ║
║  /sp-implement  → implementar con Superpowers        ║
║  /setup-update  → actualizar si cambia el stack      ║
╚══════════════════════════════════════════════════════╝
```

---

## Política de cabeceras

Solo archivos críticos llevan cabecera mínima:

| Lleva cabecera | NO lleva cabecera |
|----------------|-------------------|
| CLAUDE.md | settings.json |
| .claude/rules/* | commands/*.md |
| .claude/agents/* | hooks-config.json |
| /auth/**, /payments/** | componentes UI |
| *.migration.* | tests unitarios |

Formato:
```
<!--
@file       nombre
@purpose    qué hace en una línea
@security   CRÍTICO | ALTO | NORMAL
@updated    YYYY-MM-DD
-->
```

Al modificar un archivo con cabecera:
1. Actualizar `@updated`
2. Añadir entrada en `CHANGELOG.md`

---

## Gotchas

- ❌ No crear /plan ni /review — los maneja Superpowers
- ❌ CLAUDE.md más de 200 líneas — mover a .claude/rules/
- ❌ settings.local.json sin .gitignore — expone config personal
- ❌ Llamar codegraph_explore en sesión principal — siempre via Explore agent
- ✅ Las rules/ se cargan automáticamente en cada sesión
- ✅ `<important if="...">` es más efectivo que MUST en mayúsculas
- ✅ CodeGraph se auto-sincroniza — no requiere mantenimiento manual
- ⚠️ Si Superpowers viola una regla → reforzarla con `<important if="...">`
- ⚠️ Monorepos → un CLAUDE.md por carpeta relevante

---

## Referencias
- [shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice)
- [obra/superpowers](https://github.com/obra/superpowers)
- [colbymchenry/codegraph](https://github.com/colbymchenry/codegraph)
- [Docs Claude Code](https://code.claude.com/docs/en/skills)

---

## INTEGRACIÓN — Skills de Matt Pocock

> Los siguientes skills se instalan vía `npx skills@latest add mattpocock/skills`
> NO los crea este skill — se instalan por separado y se usan en el flujo diario.

### Qué agrega Matt Pocock al stack

**`/grill-with-docs`** — Antes de cada feature, Claude te interroga sobre el plan hasta que no quede ninguna ambigüedad. También construye y mantiene `CONTEXT.md` (el vocabulario compartido del proyecto) y crea ADRs cuando una decisión es difícil de revertir.

**`/tdd`** — Implementa con loop red-green-refactor vertical (un test → una implementación → siguiente). Nunca escribe todos los tests primero. Usa el vocabulario de `CONTEXT.md` para nombrar tests y funciones.

### Archivos nuevos que agregan al proyecto

```
proyecto/
├── CONTEXT.md                  ← vocabulario compartido del dominio
└── docs/
    └── adr/                    ← decisiones de arquitectura (Architecture Decision Records)
        ├── 0001-[decision].md
        └── 0002-[decision].md
```

### Cómo se integran con las rules/

- `/grill-with-docs` lee `CONTEXT.md` y las `docs/adr/` antes de cada sesión
- `/tdd` lee `CONTEXT.md` para nombrar tests con el vocabulario correcto
- Ambos respetan `.claude/rules/` porque están en el mismo `.claude/`
