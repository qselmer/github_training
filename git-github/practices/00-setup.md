# Práctica 00 — Preparar Git y la terminal

## Objetivo

Verificar la instalación de Git, configurar la identidad del autor y reconocer la carpeta de trabajo.

## Parte A. Verificar la instalación

```bash
# Muestra la versión instalada de Git.
git --version

# Abre la ayuda general de Git en la terminal.
git help
```

Si `git --version` no devuelve un número de versión, instala Git antes de continuar.

## Parte B. Configurar la identidad

Sustituye los valores de ejemplo por tus datos reales.

```bash
# Define el nombre que aparecerá como autor de tus commits.
git config --global user.name "Your Name"

# Define el correo asociado con tu cuenta de GitHub.
git config --global user.email "your@email.com"

# Establece main como nombre inicial de las nuevas ramas principales.
git config --global init.defaultBranch main

# Muestra toda la configuración global para comprobar los cambios.
git config --global --list
```

## Parte C. Practicar navegación básica

```bash
# Muestra la ruta completa de la carpeta actual.
pwd

# Lista los archivos y carpetas visibles.
ls

# Crea una carpeta temporal para practicar.
mkdir git-sandbox

# Entra en la carpeta temporal.
cd git-sandbox

# Regresa a la carpeta superior.
cd ..

# Elimina la carpeta temporal vacía.
rmdir git-sandbox
```

## Parte D. Consultar ayuda específica

```bash
# Muestra la documentación del comando status.
git help status

# Muestra una ayuda breve del comando commit.
git commit -h
```

## Ejercicios

### Básico

1. Ejecuta `git config --global --list`.
2. Identifica `user.name`, `user.email` e `init.defaultbranch`.
3. Explica qué información controla cada opción.

### Intermedio

```bash
# Muestra únicamente el nombre configurado.
git config --global user.name

# Muestra únicamente el correo configurado.
git config --global user.email
```

### Desafío

Investiga con `git help config` cómo definir un editor predeterminado. No cambies la configuración si no conoces el nombre ejecutable de tu editor.

## Evidencia

La práctica termina cuando Git responde correctamente y la identidad del autor aparece en la configuración global.