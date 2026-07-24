# Git commands — referencia comentada

Esta hoja resume los comandos empleados en las prácticas. Lee el comentario antes de ejecutar cada línea.

## 1. Instalación y configuración

```bash
# Muestra la versión instalada de Git.
git --version

# Define el nombre del autor para todos los repositorios del usuario.
git config --global user.name "Your Name"

# Define el correo del autor para todos los repositorios del usuario.
git config --global user.email "your@email.com"

# Usa main como rama inicial de los nuevos repositorios.
git config --global init.defaultBranch main

# Muestra la configuración global activa.
git config --global --list
```

## 2. Crear y obtener repositorios

```bash
# Inicializa un repositorio dentro de la carpeta actual.
git init

# Descarga un repositorio remoto y crea una copia local.
git clone REPOSITORY_URL

# Descarga un repositorio remoto usando un nombre de carpeta específico.
git clone REPOSITORY_URL LOCAL_FOLDER
```

## 3. Inspeccionar el estado

```bash
# Muestra la rama, el staging y los archivos modificados o no rastreados.
git status

# Muestra una versión compacta del estado.
git status --short

# Muestra cambios que todavía no están en staging.
git diff

# Muestra cambios que ya fueron añadidos al staging.
git diff --staged
```

## 4. Preparar y confirmar cambios

```bash
# Añade un archivo específico al staging.
git add FILE

# Añade todos los cambios de la carpeta actual y sus subcarpetas.
git add .

# Registra el contenido del staging como un nuevo commit.
git commit -m "type: concise description"

# Incorpora cambios preparados al último commit y conserva su mensaje.
git commit --amend --no-edit
```

Prefiere `git add FILE` durante el aprendizaje porque obliga a seleccionar conscientemente qué entra en cada commit.

## 5. Consultar el historial

```bash
# Muestra el historial completo.
git log

# Muestra un commit por línea.
git log --oneline

# Muestra ramas, referencias y estructura del historial.
git log --oneline --graph --decorate --all

# Muestra los detalles del commit más reciente.
git show HEAD

# Muestra los detalles de un commit específico.
git show COMMIT_ID

# Muestra los commits que modificaron un archivo.
git log --oneline -- FILE
```

## 6. Ramas

```bash
# Lista las ramas locales y marca la activa.
git branch

# Crea una rama sin cambiar a ella.
git branch BRANCH_NAME

# Crea una rama y cambia inmediatamente a ella.
git switch -c BRANCH_NAME

# Cambia a una rama existente.
git switch BRANCH_NAME

# Integra la rama indicada en la rama actual.
git merge BRANCH_NAME

# Elimina una rama local que ya fue integrada.
git branch -d BRANCH_NAME

# Fuerza la eliminación de una rama local no integrada; úsalo con cautela.
git branch -D BRANCH_NAME
```

## 7. Repositorios remotos

```bash
# Muestra los remotos y sus direcciones.
git remote -v

# Añade un remoto llamado origin.
git remote add origin REPOSITORY_URL

# Añade el repositorio original de un fork con el alias upstream.
git remote add upstream ORIGINAL_REPOSITORY_URL

# Muestra información detallada del remoto origin.
git remote show origin

# Cambia la URL asociada con origin.
git remote set-url origin NEW_REPOSITORY_URL
```

## 8. Push, fetch y pull

```bash
# Publica main y establece su rama remota de seguimiento.
git push -u origin main

# Publica la rama actual cuando ya tiene seguimiento configurado.
git push

# Descarga referencias remotas sin modificar archivos locales.
git fetch origin

# Descarga referencias del repositorio original de un fork.
git fetch upstream

# Descarga e integra origin/main en la rama actual.
git pull origin main

# Descarga cambios y reaplica commits locales encima de la versión remota.
git pull --rebase
```

## 9. Fork y colaboración

```bash
# Clona el fork del estudiante.
git clone https://github.com/USERNAME/REPOSITORY.git

# Añade el repositorio original como upstream.
git remote add upstream https://github.com/OWNER/REPOSITORY.git

# Descarga los cambios recientes del repositorio original.
git fetch upstream

# Integra upstream/master solo cuando es posible avanzar directamente.
git merge --ff-only upstream/master

# Publica una rama de contribución en el fork.
git push -u origin BRANCH_NAME
```

La creación del fork y del pull request se realiza normalmente desde la interfaz de GitHub.

## 10. Correcciones seguras

```bash
# Descarta cambios no preparados de un archivo y recupera su última versión confirmada.
git restore FILE

# Retira un archivo del staging sin borrar su modificación local.
git restore --staged FILE

# Restaura un archivo usando una versión histórica específica.
git restore --source=COMMIT_ID FILE

# Crea un commit nuevo que invierte un commit anterior.
git revert COMMIT_ID
```

`git revert` es apropiado para historial compartido porque no elimina commits existentes.

## 11. Reset y recuperación avanzada

```bash
# Mueve HEAD al commit indicado y conserva los cambios en staging.
git reset --soft COMMIT_ID

# Mueve HEAD al commit indicado y conserva los cambios fuera del staging.
git reset --mixed COMMIT_ID

# Mueve HEAD y reemplaza los archivos locales; puede eliminar trabajo no confirmado.
git reset --hard COMMIT_ID

# Muestra movimientos recientes de HEAD, incluidos resets y cambios de rama.
git reflog

# Crea una rama que apunta a un commit recuperado.
git branch RECOVERY_BRANCH COMMIT_ID
```

Antes de `reset --hard`:

```bash
# Comprueba qué trabajo local está pendiente.
git status

# Crea una referencia de respaldo al estado actual.
git branch backup-before-reset

# Revisa el historial antes de mover la rama.
git log --oneline --graph --decorate --all
```

## 12. Referencias útiles

```bash
# Representa el commit actual.
HEAD

# Representa el commit inmediatamente anterior.
HEAD~1

# Representa dos commits antes del actual.
HEAD~2

# Representa la rama remota seguida por la rama actual.
@{upstream}
```

## 13. Nivel de riesgo

| Comando | Riesgo habitual | Observación |
|---|---:|---|
| `git status` | Ninguno | Solo consulta información. |
| `git diff` | Ninguno | Solo compara contenido. |
| `git add` | Bajo | Puede revertirse con `restore --staged`. |
| `git commit` | Bajo | Crea historial local. |
| `git restore FILE` | Medio | Descarta cambios no confirmados del archivo. |
| `git revert` | Bajo | Conserva el historial y añade una reversión. |
| `git reset --soft` | Medio | Reescribe historial local, pero conserva cambios. |
| `git reset --mixed` | Medio | Reescribe historial local y modifica staging. |
| `git reset --hard` | Alto | Puede eliminar cambios y commits locales. |
| `git push --force` | Muy alto | Puede sobrescribir historial remoto compartido. |
| `git push --force-with-lease` | Alto | Más seguro que `--force`, pero solo para ramas propias. |

## Regla final

Antes de ejecutar un comando destructivo, revisa siempre:

```bash
# Inspecciona archivos modificados y staging.
git status

# Inspecciona cambios no preparados.
git diff

# Inspecciona historial y ramas.
git log --oneline --graph --decorate --all
```