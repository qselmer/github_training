# Práctica 06 — Regresar y recuperar versiones

## Objetivo

Elegir correctamente entre `restore`, `revert`, `reset` y `reflog` según el estado del cambio y si el historial ya fue compartido.

## Regla de seguridad

Antes de modificar el historial:

```bash
# Muestra cambios pendientes para evitar perder trabajo no guardado.
git status

# Muestra el historial con identificadores cortos y referencias.
git log --oneline --graph --decorate --all

# Crea una rama de respaldo apuntando al estado actual.
git branch backup-before-recovery
```

## Mapa de decisión

| Situación | Comando recomendado |
|---|---|
| Cambio sin commit que deseas descartar | `git restore FILE` |
| Archivo en staging que deseas retirar | `git restore --staged FILE` |
| Commit compartido que debe deshacerse | `git revert COMMIT` |
| Commit local que deseas rehacer conservando cambios | `git reset --soft COMMIT` |
| Commits locales que deseas retirar del staging | `git reset --mixed COMMIT` |
| Recuperar una referencia perdida | `git reflog` |
| Borrar commits y archivos locales deliberadamente | `git reset --hard COMMIT` |

## Parte A. Restaurar un archivo desde un commit anterior

```bash
# Muestra los commits que modificaron README.md.
git log --oneline -- README.md

# Muestra cómo era README.md en el commit anterior sin modificar archivos.
git show HEAD~1:README.md

# Restaura README.md usando la versión del commit anterior.
git restore --source=HEAD~1 README.md

# Revisa la diferencia producida por la restauración.
git diff

# Prepara la versión restaurada.
git add README.md

# Registra la restauración como un nuevo commit.
git commit -m "docs: restore previous README content"
```

Este método conserva el historial existente y crea una nueva versión del archivo.

## Parte B. Deshacer un commit publicado con revert

Crea primero un commit de prueba:

```bash
# Crea un archivo que simula un cambio equivocado.
echo "temporary incorrect content" > mistake.txt

# Prepara el archivo de prueba.
git add mistake.txt

# Registra el cambio equivocado.
git commit -m "test: add intentional mistake"

# Guarda visualmente el identificador del commit reciente.
git log --oneline -3
```

Ahora deshazlo:

```bash
# Crea un nuevo commit que invierte el último commit sin borrar el historial.
git revert HEAD

# Muestra el commit original y el commit de reversión.
git log --oneline -4
```

`revert` es la opción preferida cuando el commit ya fue enviado a GitHub o compartido con otras personas.

## Parte C. Rehacer commits locales con reset --soft

Trabaja en una rama exclusiva:

```bash
# Crea una rama de laboratorio para no afectar main.
git switch -c lab/reset-soft

# Crea el primer cambio de laboratorio.
echo "first line" > reset-demo.txt

# Prepara el archivo.
git add reset-demo.txt

# Registra el primer commit de laboratorio.
git commit -m "test: add first reset example"

# Añade un segundo cambio.
echo "second line" >> reset-demo.txt

# Prepara el segundo cambio.
git add reset-demo.txt

# Registra el segundo commit de laboratorio.
git commit -m "test: add second reset example"

# Muestra los commits antes del reset.
git log --oneline -4

# Mueve HEAD un commit atrás y conserva los cambios en staging.
git reset --soft HEAD~1

# Comprueba que el segundo cambio sigue preparado.
git status

# Reemplaza el commit anterior con un mensaje mejor.
git commit -m "test: complete reset example"
```

## Parte D. Usar reset --mixed

```bash
# Mueve HEAD un commit atrás y conserva los cambios fuera del staging.
git reset --mixed HEAD~1

# Comprueba que los archivos siguen modificados, pero no preparados.
git status

# Revisa el contenido que quedó en el working directory.
git diff
```

`--mixed` es el modo predeterminado de `git reset`.

## Parte E. Recuperar una referencia con reflog

```bash
# Muestra movimientos recientes de HEAD, incluidos resets y cambios de rama.
git reflog

# Crea una rama de recuperación desde un identificador encontrado en reflog.
git branch recovered-work COMMIT_ID

# Muestra todas las ramas y verifica la referencia recuperada.
git log --oneline --graph --decorate --all
```

Reemplaza `COMMIT_ID` por el identificador correcto mostrado por `git reflog`.

## Parte F. reset --hard, solo en laboratorio

`git reset --hard` cambia la rama y elimina cambios rastreados no confirmados. Antes de usarlo, crea una rama de respaldo y confirma que no existe trabajo importante.

```bash
# Guarda una referencia de respaldo antes de la operación destructiva.
git branch backup-before-hard-reset

# Muestra el estado y verifica que entiendes qué se eliminará.
git status

# Mueve la rama al commit anterior y sincroniza los archivos con ese commit.
git reset --hard HEAD~1

# Comprueba el nuevo estado del historial.
git log --oneline -4
```

No ejecutes `git push --force` sobre una rama compartida para publicar este cambio.

## Ejercicios

### Básico

Restaura un archivo modificado sin commit mediante `git restore FILE`.

### Intermedio

Crea un commit de prueba y deshazlo mediante `git revert`. Compara los dos commits con `git show`.

### Difícil

1. Crea dos commits en una rama de laboratorio.
2. Ejecuta `git reset --soft HEAD~1`.
3. Vuelve a crear el commit con otro mensaje.
4. Usa `git reflog` para identificar el commit original.
5. Crea una rama que lo recupere.

## Evidencia

Debes poder justificar por qué `revert` es apropiado para historial compartido y por qué `reset` debe reservarse principalmente para historial local.