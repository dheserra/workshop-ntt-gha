# 🚀 GitHub Actions — Workshop Semana 1

*Un workshop práctico y automatizado para dar tus primeros pasos con GitHub Actions.*

## Bienvenida

- **¿Para quién es esto?** Personas con conocimiento nulo o muy básico de GitHub Actions que ya saben usar Git y GitHub (clonar, hacer commit, push, abrir un Pull Request).
- **Qué vas a aprender:**
  1. Qué es GitHub Actions y qué problema resuelve.
  2. La anatomía completa de un workflow (`on`, `jobs`, `steps`, `runs-on`, `run`, `uses`).
  3. Los triggers (*events*) más comunes: `workflow_dispatch`, `push`, `pull_request` y `schedule`.
- **Qué vas a construir:** tu propio workflow de GitHub Actions, escrito desde cero, que reacciona a cuatro eventos distintos.
- **Prerrequisitos:** cuenta de GitHub y conocimientos básicos de Git (clone, commit, push, pull request). Cero experiencia previa con Actions.
- **Duración:** 3 sesiones de 1 hora (lunes, miércoles y viernes).

Este repositorio es **interactivo**: a medida que completas cada actividad, GitHub Actions revisa tu trabajo automáticamente y te va desbloqueando el siguiente paso mediante comentarios en un Issue. Literalmente vas a aprender GitHub Actions *usando* GitHub Actions — y en la Sesión 3 vas a poder abrir el código de esa automatización para ver cómo está hecha.

## Cómo empezar

> ⚠️ Este workshop funciona por medio de un **fork**, no de una copia de plantilla, para que cada asistente tenga su propio repositorio independiente conectado al original.

1. Haz clic en **Fork** (arriba a la derecha de este repositorio) y crea el fork en tu cuenta personal.
2. En tu fork, ve a **Settings → General → Features** y activa la casilla **Issues** (los forks la traen desactivada por defecto).
3. Entra a tu fork → pestaña **Actions**. GitHub deshabilita los workflows en todo fork nuevo por seguridad, así que haz clic en **"I understand my workflows, go ahead and enable them"**.
4. En la lista de workflows de la izquierda, selecciona **"Workshop 🚀 - Iniciar"**.
5. Haz clic en **Run workflow** → rama `main` → **Run workflow**.
6. Espera unos 15–20 segundos y **actualiza la página**. Se creará automáticamente un Issue llamado **"Mi progreso: GitHub Actions Semana 1 · Paso 1"** con las instrucciones de la primera actividad.
7. Sigue las instrucciones del Issue. Cada vez que hagas `push` a `main` con la actividad completa, el mismo Issue se actualizará con feedback y el contenido del siguiente paso.

**¿Problemas? 🤷**

- Verifica que estás trabajando en tu **fork**, no en este repositorio original.
- Verifica en la pestaña **Actions** de tu fork que los workflows se ejecutaron (✅ verde = éxito, ❌ rojo = falló — haz clic para leer el log).
- Si no ves el Issue después de un minuto, vuelve a correr el workflow **"Workshop 🚀 - Iniciar"** manualmente.
- Si el Issue no recibe comentarios después de un push, revisa que hayas editado exactamente el archivo `.github/workflows/hello-world.yml`.
- Si el workflow falla en un paso que dice `gh issue comment` o `gh issue create`, probablemente falta habilitar permisos de escritura: ve a **Settings → Actions → General → Workflow permissions** y selecciona **"Read and write permissions"**.

## Estructura del workshop

| Sesión | Tema | Actividad |
|---|---|---|
| 1 | ¿Qué es GitHub Actions? | Crear tu primer workflow con `workflow_dispatch` |
| 2 | Anatomía de un workflow | Disparar el workflow con `push`, agregar `checkout` y un script |
| 3 | Events y triggers | Agregar `pull_request` y `schedule`, abrir un Pull Request real |

## Cómo funciona por dentro

Todo el "bot" que te da feedback es, en sí mismo, GitHub Actions:

- `.github/workflows/0-start-workshop.yml` crea tu Issue de seguimiento.
- `.github/workflows/1-check-progress.yml` revisa el contenido de tu `hello-world.yml` cada vez que haces push a `main`, comenta el resultado y desbloquea el siguiente paso.
- `.github/workflows/2-celebrate-pr.yml` comenta en tu Pull Request en cuanto lo abres.

No necesitas entenderlos para completar el workshop, pero una vez termines la Sesión 3 ya tendrás las herramientas para leerlos y entender exactamente cómo funcionan.
