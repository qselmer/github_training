# Git y GitHub — laboratorio de prácticas

Este directorio contiene una ruta progresiva para aprender control de versiones desde cero hasta un flujo colaborativo con ramas, pull requests y GitHub Actions.

> **Repositorio de práctica:** `qselmer/.hub`. Los estudiantes pueden hacer un fork de este repositorio y trabajar en `git-github/playground/`.

## Resultados de aprendizaje

Al terminar, el estudiante podrá:

1. configurar Git y reconocer las partes de un repositorio;
2. crear commits pequeños y descriptivos;
3. consultar diferencias e historial;
4. deshacer cambios de forma segura;
5. trabajar con ramas y resolver un conflicto básico;
6. sincronizar cambios con `push`, `fetch` y `pull`;
7. crear un fork y enviar un pull request;
8. recuperar versiones anteriores con `restore`, `revert`, `reset` y `reflog`;
9. interpretar y ejecutar una GitHub Action básica.

## Ruta de prácticas

| Nivel | Práctica | Producto esperado |
|---|---|---|
| Inicial | [00 — Preparación](practices/00-setup.md) | Git configurado y verificado |
| Inicial | [01 — Primer repositorio](practices/01-first-repository.md) | Repositorio con dos commits |
| Básico | [02 — Cambios, historial y correcciones](practices/02-history-and-undo.md) | Historial inspeccionado y cambios restaurados |
| Intermedio | [03 — Ramas, merge y conflictos](practices/03-branches-and-merge.md) | Rama integrada mediante merge |
| Intermedio | [04 — Remotos, push, fetch y pull](practices/04-remotes-and-sync.md) | Repositorio local sincronizado con GitHub |
| Colaborativo | [05 — Fork y pull request](practices/05-fork-and-pull-request.md) | Pull request enviado a este repositorio |
| Avanzado | [06 — Recuperación de versiones](practices/06-commit-recovery.md) | Uso razonado de revert, reset y reflog |
| Avanzado | [07 — GitHub Actions](practices/07-github-actions.md) | Workflow ejecutado correctamente |

## Estructura

```text
# Material de estudio y ejercicios guiados.
git-github/
├── README.md
├── practices/
├── cheatsheets/
│   └── basic-commands.md
└── playground/
    ├── README.md
    └── submissions/
        └── TEMPLATE.md

# Workflow ejecutado por GitHub Actions.
.github/
└── workflows/
    └── training-check.yml
```

## Regla de trabajo

Antes de ejecutar un comando que pueda eliminar o reescribir cambios:

```bash
# Muestra el estado actual del repositorio.
git status

# Muestra los cambios que todavía no están en staging.
git diff

# Muestra un historial compacto para identificar commits.
git log --oneline --graph --decorate --all
```

No copies una secuencia completa sin leerla. Ejecuta un comando, observa su salida y recién continúa con el siguiente.

## Referencia rápida

Consulta [Basic Git commands](cheatsheets/basic-commands.md) para revisar sintaxis, propósito y nivel de riesgo de cada comando.