# Práctica 05 — Fork, rama y pull request

## Objetivo

Contribuir a este repositorio sin acceso directo de escritura mediante el flujo:

```text
fork → clone → branch → edit → commit → push → pull request
```

## Repositorio de laboratorio

Usa este repositorio como proyecto de prueba:

```text
https://github.com/qselmer/.hub
```

La contribución se realizará dentro de:

```text
git-github/playground/submissions/
```

## Parte A. Crear el fork

1. Abre `https://github.com/qselmer/.hub`.
2. Presiona **Fork**.
3. Conserva el nombre `.hub` en tu cuenta.
4. Espera hasta que GitHub muestre `TU_USUARIO/.hub`.

Un fork es una copia del repositorio bajo tu propia cuenta. Puedes escribir en tu fork aunque no tengas permisos sobre el repositorio original.

## Parte B. Clonar tu fork

Reemplaza `TU_USUARIO` por tu nombre de GitHub.

```bash
# Descarga tu fork a la computadora y crea la carpeta .hub.
git clone https://github.com/TU_USUARIO/.hub.git

# Entra en el repositorio clonado.
cd .hub

# Muestra el remoto origin, que debe apuntar a tu fork.
git remote -v

# Añade el repositorio original con el alias upstream.
git remote add upstream https://github.com/qselmer/.hub.git

# Comprueba que origin y upstream apuntan a repositorios diferentes.
git remote -v
```

## Parte C. Actualizar el fork antes de trabajar

```bash
# Descarga las referencias más recientes del repositorio original.
git fetch upstream

# Cambia a la rama principal local.
git switch master

# Integra la versión reciente de upstream/master sin crear un merge innecesario.
git merge --ff-only upstream/master

# Actualiza también la rama master de tu fork.
git push origin master
```

## Parte D. Crear una rama de contribución

Usa un nombre breve y reemplaza `TU_USUARIO`.

```bash
# Crea una rama independiente para tu contribución.
git switch -c student/TU_USUARIO

# Copia la plantilla y crea un archivo propio.
cp git-github/playground/submissions/TEMPLATE.md git-github/playground/submissions/TU_USUARIO.md

# Abre el archivo en VS Code para completar la información.
code git-github/playground/submissions/TU_USUARIO.md
```

Si `code` no está disponible, abre el archivo con cualquier editor de texto.

## Parte E. Revisar y registrar la contribución

```bash
# Muestra qué archivo cambió.
git status

# Revisa línea por línea la modificación realizada.
git diff

# Prepara únicamente tu archivo de estudiante.
git add git-github/playground/submissions/TU_USUARIO.md

# Comprueba el contenido que será incluido en el commit.
git diff --staged

# Registra la contribución con un mensaje específico.
git commit -m "docs: add TU_USUARIO training submission"

# Publica la rama en tu fork y configura su seguimiento.
git push -u origin student/TU_USUARIO
```

## Parte F. Crear el pull request

1. Abre tu fork en GitHub.
2. Presiona **Compare & pull request**.
3. Comprueba las ramas:
   - base repository: `qselmer/.hub`;
   - base: `master`;
   - head repository: `TU_USUARIO/.hub`;
   - compare: `student/TU_USUARIO`.
4. Usa el título `docs: add TU_USUARIO training submission`.
5. Describe qué archivo agregaste y qué aprendiste.
6. Presiona **Create pull request**.

## Parte G. Incorporar correcciones solicitadas

No se crea otro pull request. Se actualiza la misma rama:

```bash
# Cambia a la rama asociada con el pull request.
git switch student/TU_USUARIO

# Edita nuevamente el archivo solicitado.
code git-github/playground/submissions/TU_USUARIO.md

# Revisa los cambios antes de guardarlos en el historial.
git diff

# Prepara el archivo corregido.
git add git-github/playground/submissions/TU_USUARIO.md

# Registra la corrección solicitada durante la revisión.
git commit -m "docs: address pull request feedback"

# Publica el nuevo commit; el pull request se actualiza automáticamente.
git push
```

## Ejercicios

### Básico

Completa el archivo personal, crea un commit y publica la rama en tu fork.

### Intermedio

Solicita a un compañero que revise el pull request y deja una respuesta explicando qué corrección aplicaste.

### Difícil

Actualiza tu rama cuando `upstream/master` haya avanzado:

```bash
# Descarga la versión más reciente del repositorio original.
git fetch upstream

# Reaplica tus commits sobre la versión reciente de master.
git rebase upstream/master

# Actualiza la rama remota de forma segura después del rebase.
git push --force-with-lease
```

`--force-with-lease` verifica que la rama remota no haya cambiado inesperadamente. Es más segura que `--force`, pero solo debe usarse en una rama propia, nunca sobre una rama compartida.

## Evidencia

La práctica termina cuando existe un pull request abierto desde tu fork hacia `qselmer/.hub:master` y la GitHub Action del repositorio finaliza correctamente.