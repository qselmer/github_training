# Práctica 04 — Remotos, push, fetch y pull

## Objetivo

Comprender la relación entre el repositorio local y GitHub, publicar ramas y sincronizar cambios remotos.

## Conceptos mínimos

- `origin`: alias habitual del repositorio remoto principal.
- `push`: envía commits locales al remoto.
- `fetch`: descarga referencias remotas sin modificar tus archivos.
- `pull`: ejecuta `fetch` y luego integra cambios en la rama actual.

## Parte A. Inspeccionar el remoto

```bash
# Muestra los remotos configurados y sus direcciones de lectura y escritura.
git remote -v

# Muestra información detallada del remoto origin.
git remote show origin

# Muestra las ramas locales junto con su rama remota de seguimiento.
git branch -vv
```

## Parte B. Publicar una rama

```bash
# Crea una rama para agregar documentación.
git switch -c docs/add-workflow

# Crea un archivo nuevo con un encabezado.
echo "# Daily workflow" > workflow.md

# Añade una explicación al archivo.
echo "status -> add -> commit -> push" >> workflow.md

# Prepara el archivo nuevo.
git add workflow.md

# Registra el cambio localmente.
git commit -m "docs: add daily Git workflow"

# Publica la rama y establece origin/docs/add-workflow como seguimiento.
git push -u origin docs/add-workflow
```

## Parte C. Descargar información sin integrar

Haz un cambio en GitHub desde el navegador, por ejemplo editando una línea del README. Después:

```bash
# Descarga commits y referencias remotas sin modificar la rama local.
git fetch origin

# Muestra diferencias entre tu main local y origin/main.
git log --oneline --left-right main...origin/main

# Muestra las ramas remotas conocidas localmente.
git branch --remotes
```

## Parte D. Actualizar la rama local

```bash
# Cambia a la rama principal.
git switch main

# Descarga e integra los cambios de origin/main en main.
git pull origin main

# Comprueba que el árbol de trabajo está actualizado.
git status
```

## Parte E. Evitar un push rechazado

Antes de comenzar una sesión colaborativa:

```bash
# Cambia a la rama sobre la que trabajarás.
git switch main

# Descarga e integra cambios recientes del remoto.
git pull origin main

# Crea una rama nueva desde una base actualizada.
git switch -c feature/new-task
```

Si GitHub rechaza un `push`, no uses `--force` automáticamente. Primero ejecuta:

```bash
# Descarga la información más reciente del remoto.
git fetch origin

# Muestra la divergencia entre la rama local y su seguimiento remoto.
git log --oneline --left-right HEAD...@{upstream}

# Integra los cambios remotos mediante rebase para conservar un historial lineal.
git pull --rebase

# Publica nuevamente después de resolver cualquier conflicto.
git push
```

## Ejercicios

### Básico

1. Ejecuta `git remote -v`.
2. Identifica cuál URL se usa para `fetch` y cuál para `push`.
3. Explica por qué normalmente son iguales.

### Intermedio

Crea y publica una rama propia. Luego elimínala localmente y recupérala desde el remoto.

```bash
# Elimina la rama local después de cambiar a main.
git branch -d BRANCH_NAME

# Vuelve a crear una rama local basada en la rama remota.
git switch --track origin/BRANCH_NAME
```

### Desafío

Trabaja con un compañero. Ambos deben modificar archivos distintos, hacer `pull`, realizar commits y publicar sin sobrescribir el trabajo del otro.

## Evidencia

- Puedes explicar la diferencia entre `fetch` y `pull`.
- Puedes publicar una rama con seguimiento.
- Sabes diagnosticar un push rechazado sin recurrir inmediatamente a `--force`.