# Práctica 02 — Cambios, historial y correcciones seguras

## Objetivo

Comparar versiones, inspeccionar el historial y corregir cambios antes y después del staging.

## Preparación

Trabaja dentro del repositorio creado en la Práctica 01.

```bash
# Entra en el repositorio de práctica; ajusta la ruta si es necesario.
cd my-first-repo

# Confirma que estás dentro de un repositorio y revisa su estado.
git status
```

## Parte A. Comparar cambios

```bash
# Añade una línea nueva al final del README.
echo "Learning to inspect changes." >> README.md

# Muestra los cambios no preparados respecto al último commit.
git diff

# Muestra un resumen corto del estado.
git status --short
```

## Parte B. Descartar un cambio no preparado

```bash
# Restaura README.md desde el último commit y descarta la modificación local.
git restore README.md

# Verifica que el archivo dejó de aparecer como modificado.
git status
```

`git restore FILE` elimina cambios no guardados en ese archivo. Debe usarse después de revisar `git diff`.

## Parte C. Retirar un archivo del staging

```bash
# Vuelve a modificar README.md.
echo "Learning the staging area." >> README.md

# Añade README.md al staging.
git add README.md

# Confirma que el cambio está preparado.
git status

# Retira README.md del staging sin borrar la modificación local.
git restore --staged README.md

# Comprueba que el cambio sigue existiendo, pero ya no está preparado.
git status
```

## Parte D. Confirmar e inspeccionar el historial

```bash
# Prepara nuevamente el archivo.
git add README.md

# Registra el cambio en un commit.
git commit -m "docs: explain staging area"

# Muestra el historial como una línea por commit.
git log --oneline

# Muestra el historial con ramas y referencias visibles.
git log --oneline --graph --decorate --all

# Muestra el contenido y metadatos del commit más reciente.
git show HEAD
```

## Parte E. Corregir el último commit

Usa `--amend` solo si el commit todavía no fue compartido o si sabes que reescribirlo es aceptable.

```bash
# Añade una corrección al README.
echo "A commit should represent one coherent change." >> README.md

# Prepara la corrección.
git add README.md

# Incorpora la corrección al último commit y conserva su mensaje.
git commit --amend --no-edit

# Comprueba que el identificador del último commit cambió.
git log --oneline -3
```

## Ejercicios

### Básico

1. Modifica `README.md`.
2. Observa `git diff`.
3. Descarta la modificación con `git restore`.

### Intermedio

1. Modifica dos archivos.
2. Añade solo uno al staging.
3. Compara `git diff` con `git diff --staged`.

```bash
# Muestra cambios que todavía no están en staging.
git diff

# Muestra cambios que ya están en staging.
git diff --staged
```

### Desafío

Crea un commit con un error tipográfico, corrígelo y usa `git commit --amend --no-edit`. Explica por qué el hash del commit cambia aunque el mensaje permanezca igual.

## Evidencia

- Puedes diferenciar working directory, staging y commit.
- Puedes explicar `restore` y `restore --staged`.
- El historial final está limpio y comprensible.