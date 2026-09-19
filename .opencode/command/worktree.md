---
description: Crea un worktree de git bajo .worktrees/ con el nombre dado en kebab-case.
agent: build
---

Ejecuta exactamente este comando git:

1. Toma el argumento del usuario como nombre del worktree.
2. Conviértelo a kebab-case: minúsculas, sin espacios (conecta las palabras con un guion `-`).
3. Ejecuta, sin hacer nada más:
4. Si los argumentos son muy largos, simplificalo a un nombre significativo.

git worktree add ".worktrees/<nombre-kebab>"

No ejecutes otros comandos ni hagas otros cambios.