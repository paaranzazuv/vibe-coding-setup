Actualizar el plugin vibe-coding-setup a la última versión publicada.

Ejecutar en Claude Code:

```
! claude plugin update vibe-coding-setup@vibe-coding-setup
```

Si falla porque el marketplace no está registrado, ejecutar primero:

```
/plugin marketplace add paaranzazuv/vibe-coding-setup
! claude plugin update vibe-coding-setup@vibe-coding-setup
```

Después de actualizar, pedir al usuario que reinicie Claude Code para que los cambios tomen efecto.

Aclarar: los archivos ya generados en el proyecto (CLAUDE.md, .claude/rules/, etc.) NO se modifican. Solo se actualiza el plugin en ~/.claude/.
