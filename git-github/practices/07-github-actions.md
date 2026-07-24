# Práctica 07 — Primera GitHub Action

## Objetivo

Comprender cómo un workflow automatiza verificaciones cada vez que se hace `push` o se actualiza un pull request.

## Workflow incluido

El repositorio contiene:

```text
.github/workflows/training-check.yml
```

Este workflow realiza tres comprobaciones:

1. verifica que existan archivos esenciales del curso;
2. detecta marcadores de conflictos sin resolver;
3. informa si todas las comprobaciones finalizaron correctamente.

## Parte A. Leer la estructura del workflow

Un workflow de GitHub Actions contiene:

- `name`: nombre visible;
- `on`: eventos que lo activan;
- `permissions`: permisos mínimos;
- `jobs`: trabajos que se ejecutan;
- `steps`: pasos secuenciales de cada trabajo;
- `uses`: acción reutilizable;
- `run`: comandos ejecutados en la máquina virtual.

Abre el archivo y relaciona cada línea comentada con estos componentes.

## Parte B. Activar la Action mediante un cambio válido

Trabaja en una rama nueva.

```bash
# Actualiza las referencias remotas antes de iniciar.
git fetch origin

# Crea una rama específica para probar la automatización.
git switch -c lab/action-success

# Añade una línea válida al archivo del playground.
echo "Action test completed." >> git-github/playground/README.md

# Revisa exactamente qué cambió.
git diff

# Prepara el archivo modificado.
git add git-github/playground/README.md

# Registra el cambio que activará el workflow.
git commit -m "test: trigger training action"

# Publica la rama en GitHub.
git push -u origin lab/action-success
```

Después:

1. abre el repositorio en GitHub;
2. entra en la pestaña **Actions**;
3. selecciona **Training repository checks**;
4. abre la ejecución más reciente;
5. revisa cada step y su salida.

## Parte C. Activar un fallo controlado

Hazlo únicamente en una rama de laboratorio.

```bash
# Crea una rama separada para generar un fallo deliberado.
git switch -c lab/action-failure

# Crea un archivo con un marcador de conflicto sin resolver.
echo "<<<<<<< HEAD" > git-github/playground/conflict-demo.md

# Añade una línea que simula una versión del archivo.
echo "version A" >> git-github/playground/conflict-demo.md

# Añade el separador típico de un conflicto.
echo "=======" >> git-github/playground/conflict-demo.md

# Añade una segunda versión simulada.
echo "version B" >> git-github/playground/conflict-demo.md

# Añade el marcador final del conflicto.
echo ">>>>>>> feature/demo" >> git-github/playground/conflict-demo.md

# Prepara el archivo que debe provocar el fallo.
git add git-github/playground/conflict-demo.md

# Registra el ejemplo intencionalmente incorrecto.
git commit -m "test: demonstrate failing action"

# Publica la rama para ejecutar el workflow.
git push -u origin lab/action-failure
```

La Action debe fallar en **Detect unresolved merge markers**.

## Parte D. Corregir el fallo

```bash
# Reemplaza el archivo conflictivo con contenido válido.
echo "Conflict resolved successfully." > git-github/playground/conflict-demo.md

# Revisa la corrección.
git diff

# Prepara el archivo corregido.
git add git-github/playground/conflict-demo.md

# Registra la solución del problema detectado por CI.
git commit -m "fix: remove unresolved conflict markers"

# Publica el nuevo commit en la misma rama.
git push
```

La nueva ejecución debe pasar. Este ciclo reproduce una idea central de integración continua:

```text
change → automated check → failure → correction → successful check
```

## Parte E. Interpretar el archivo YAML

Responde:

1. ¿Qué eventos activan el workflow?
2. ¿Por qué se utiliza `actions/checkout@v4`?
3. ¿Qué significa `runs-on: ubuntu-latest`?
4. ¿Por qué `permissions` solo concede lectura?
5. ¿Qué condición produce `exit 1`?
6. ¿Cómo influye el estado de la Action en un pull request?

## Ejercicios

### Básico

Ejecuta el workflow mediante un cambio válido y localiza el mensaje final de éxito.

### Intermedio

Agrega un archivo obligatorio nuevo al arreglo `required_files` y comprueba que el workflow falle cuando ese archivo no existe.

### Difícil

Amplía el workflow para verificar que ningún archivo Markdown del playground esté vacío. Mantén comentarios que expliquen cada comando del script.

Pista:

```bash
# Busca archivos Markdown vacíos y devuelve sus rutas.
find git-github/playground -name "*.md" -type f -empty
```

## Evidencia

- Puedes localizar una ejecución de Actions.
- Puedes interpretar logs de steps.
- Puedes provocar, diagnosticar y corregir un fallo automatizado.
- Entiendes que una Action no reemplaza la revisión humana, sino que automatiza comprobaciones repetibles.