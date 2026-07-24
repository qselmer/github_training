# Git and GitHub playground

Esta carpeta es el espacio de práctica colaborativa del curso.

## Actividad principal

Cada estudiante debe:

1. hacer un fork de `qselmer/.hub`;
2. clonar su fork;
3. configurar el remoto `upstream`;
4. crear una rama `student/USERNAME`;
5. copiar `submissions/TEMPLATE.md` como `submissions/USERNAME.md`;
6. completar el archivo;
7. crear un commit;
8. publicar la rama;
9. abrir un pull request hacia `qselmer/.hub:master`.

La guía completa se encuentra en [Práctica 05](../practices/05-fork-and-pull-request.md).

## Reglas

- No modifiques ni elimines archivos de otros estudiantes.
- Trabaja en una rama propia.
- Incluye solo tu archivo en el pull request.
- Usa un mensaje de commit descriptivo.
- Comprueba que la GitHub Action termine correctamente.
- Responde a los comentarios de revisión con nuevos commits en la misma rama.

## Convención de nombres

```text
# Rama de trabajo del estudiante.
student/USERNAME

# Archivo que será enviado mediante pull request.
git-github/playground/submissions/USERNAME.md
```

## Comandos mínimos

```bash
# Crea una rama individual y cambia a ella.
git switch -c student/USERNAME

# Copia la plantilla como un archivo propio.
cp git-github/playground/submissions/TEMPLATE.md git-github/playground/submissions/USERNAME.md

# Prepara únicamente el archivo propio.
git add git-github/playground/submissions/USERNAME.md

# Registra la contribución en el historial local.
git commit -m "docs: add USERNAME training submission"

# Publica la rama en el fork del estudiante.
git push -u origin student/USERNAME
```

Reemplaza `USERNAME` por el nombre real de la cuenta de GitHub.