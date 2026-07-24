# Práctica 03 — Ramas, merge y conflictos

## Objetivo

Crear una rama, desarrollar un cambio aislado, integrarlo en `main` y resolver un conflicto básico.

## Parte A. Crear una rama de trabajo

```bash
# Muestra las ramas locales y marca la rama activa con un asterisco.
git branch

# Crea la rama feature/add-profile y cambia inmediatamente a ella.
git switch -c feature/add-profile

# Confirma que ahora estás trabajando en la nueva rama.
git branch
```

## Parte B. Registrar un cambio en la rama

```bash
# Crea un archivo de perfil con un encabezado inicial.
echo "# Student profile" > profile.md

# Añade una segunda línea al perfil.
echo "Learning Git branches." >> profile.md

# Revisa los archivos modificados o nuevos.
git status

# Prepara únicamente profile.md.
git add profile.md

# Guarda el nuevo archivo en la rama actual.
git commit -m "docs: add student profile"

# Muestra el historial y la posición de las ramas.
git log --oneline --graph --decorate --all
```

## Parte C. Integrar la rama

```bash
# Cambia a la rama principal.
git switch main

# Integra los commits de feature/add-profile en main.
git merge feature/add-profile

# Elimina la rama local porque ya fue integrada.
git branch -d feature/add-profile

# Comprueba el historial final.
git log --oneline --graph --decorate --all
```

## Parte D. Crear intencionalmente un conflicto

```bash
# Crea una rama para cambiar la primera línea del perfil.
git switch -c feature/change-title

# Reemplaza profile.md con una versión creada desde esta rama.
printf "# Marine data student\nLearning Git branches.\n" > profile.md

# Prepara el cambio de título.
git add profile.md

# Registra el cambio en la rama.
git commit -m "docs: revise profile title"

# Regresa a main.
git switch main

# Crea un cambio incompatible sobre la misma primera línea.
printf "# Git and GitHub student\nLearning Git branches.\n" > profile.md

# Prepara el cambio realizado en main.
git add profile.md

# Registra la versión alternativa del título.
git commit -m "docs: update profile heading on main"

# Intenta integrar la rama; Git detendrá el proceso por el conflicto.
git merge feature/change-title
```

## Parte E. Resolver el conflicto

Abre `profile.md`. Git mostrará marcadores similares a estos:

```text
<<<<<<< HEAD
versión de main
=======
versión de la rama
>>>>>>> feature/change-title
```

Edita el archivo y conserva una versión final coherente. Luego ejecuta:

```bash
# Muestra qué archivos siguen en conflicto.
git status

# Marca profile.md como resuelto después de editarlo.
git add profile.md

# Crea el commit que finaliza el merge.
git commit -m "merge: resolve profile title conflict"

# Comprueba gráficamente cómo convergieron las ramas.
git log --oneline --graph --decorate --all

# Elimina la rama ya integrada.
git branch -d feature/change-title
```

## Ejercicios

### Básico

Crea una rama `feature/add-notes`, añade `notes.md`, realiza un commit e intégralo en `main`.

### Intermedio

Publica una rama en GitHub:

```bash
# Publica la rama actual y establece su seguimiento remoto.
git push -u origin feature/add-notes
```

### Desafío

Genera un conflicto en un archivo de texto, resuélvelo sin eliminar contenido válido y explica qué representan `HEAD`, `=======` y el nombre de la rama en los marcadores.

## Evidencia

- El historial contiene al menos un merge.
- Puedes crear, cambiar, integrar y eliminar ramas.
- Puedes reconocer y resolver un conflicto básico.