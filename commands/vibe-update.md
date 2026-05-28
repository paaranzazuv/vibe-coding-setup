Actualizar el plugin vibe-coding-setup a la última versión publicada.

Ejecutar este comando de Superpowers:

```
/plugin update vibe-coding-setup@vibe-coding-setup
```

Si el comando falla porque el marketplace no está registrado, ejecutar primero:

```
/plugin marketplace add paaranzazuv/vibe-coding-setup
/plugin update vibe-coding-setup@vibe-coding-setup
```

Después de actualizar, confirmar al usuario:
- Qué versión había instalada (leer gitCommitSha de installed_plugins.json si es accesible)
- Que la actualización completó correctamente
- Recordar que los archivos ya generados en el proyecto (CLAUDE.md, .claude/rules/) NO se modifican — solo se actualiza el plugin en ~/.claude/
