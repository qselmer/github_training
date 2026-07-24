# Práctica 01 — Crear el primer repositorio

## Objetivo

Crear un repositorio local, registrar dos versiones de un archivo y publicarlo en GitHub.

## Requisitos

- Haber completado la [Práctica 00](00-setup.md).
- Usar Git Bash, una terminal de Linux/macOS o la terminal integrada de VS Code.
- Crear previamente en GitHub un repositorio vacío llamado `my-first-repo`, sin README ni licencia.

## Parte A. Crear el proyecto local

```bash
# Crea una carpeta nueva para el proyecto.
mkdir my-first-repo

# Entra en la carpeta recién creada.
cd my-first-repo

# Convierte la carpeta actual en un repositorio Git.
git init

# Comprueba la rama actual y los archivos sin seguimiento.
git status
```

### Comprueba qué ocurrió

```bash
# Muestra archivos ocultos; debería aparecer la carpeta interna .git.
ls -la
```

La carpeta `.git` contiene el historial y la configuración local. No debe editarse manualmente.

## Parte B. Crear el primer archivo

```bash
# Crea README.md y escribe su primera línea; > reemplaza el contenido existente.
echo "# My First Repository" > README.md

# Muestra el contenido del archivo en la terminal.
cat README.md

# Confirma que README.md aparece como archivo no rastreado.
git status
```

## Parte C. Crear el primer commit

```bash
# Añade únicamente README.md al área de preparación o staging.
git add README.md

# Verifica que README.md está preparado para el próximo commit.
git status

# Guarda una versión permanente con un mensaje descriptivo.
git commit -m "docs: add initial README"

# Muestra el historial resumido del repositorio.
git log --oneline
```

## Parte D. Conectar el repositorio con GitHub

Reemplaza `USERNAME` por tu usuario real de GitHub.

```bash
# Renombra la rama actual como main.
git branch -M main

# Registra el repositorio de GitHub con el alias origin.
git remote add origin https://github.com/USERNAME/my-first-repo.git

# Comprueba la dirección configurada para origin.
git remote -v

# Publica main y establece origin/main como rama de seguimiento.
git push -u origin main
```

## Parte E. Crear una segunda versión

```bash
# Añade una línea al final de README.md; >> conserva el contenido anterior.
echo "This repository contains my Git practice." >> README.md

# Muestra exactamente qué líneas cambiaron.
git diff

# Prepara el archivo modificado para el siguiente commit.
git add README.md

# Registra la segunda versión del archivo.
git commit -m "docs: describe repository purpose"

# Envía el nuevo commit a GitHub.
git push

# Confirma que no quedan cambios pendientes.
git status
```

## Ejercicios

### Básico

1. Agrega tu nombre al README.
2. Crea un commit con el mensaje `docs: add author name`.
3. Publica el commit con `git push`.

### Intermedio

1. Crea un archivo `notes.md`.
2. Escribe tres comandos aprendidos y su función.
3. Añade y confirma solo `notes.md`, sin usar `git add .`.

### Desafío

Crea tres cambios separados y tres commits pequeños. Usa `git log --oneline` para explicar por qué un historial con commits específicos es más fácil de revisar que un único commit grande.

## Criterios de finalización

- El repositorio existe localmente y en GitHub.
- `README.md` contiene al menos tres líneas.
- Hay al menos tres commits.
- `git remote -v` muestra `origin`.
- `git status` informa `working tree clean`.