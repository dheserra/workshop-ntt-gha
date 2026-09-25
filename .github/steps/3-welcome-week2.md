# 👋 ¡Semana 2! Vamos a fondo con GitHub Actions

Este es un Issue nuevo, independiente del de la Semana 1 (ese ya quedó cerrado con tu progreso ahí guardado). Funciona exactamente igual: aquí irás recibiendo cada sesión y el feedback de tus actividades.

---

## 📘 Sesión 4 — Runners

**Teoría rápida:**

- Un **runner** es la máquina donde realmente se ejecuta tu job.
- **Hosted runners**: los administra GitHub. Puedes elegir `ubuntu-latest`, `windows-latest` o `macos-latest` con solo escribir el nombre — no hay que configurar nada.
- **Self-hosted runners**: máquinas propias (tuyas o de tu empresa) que tú registras y mantienes. Se usan cuando necesitas hardware específico, acceso a una red privada, o control total del entorno.
- Cada runner hosted viene con software **preinstalado** (Git, Node, Python, Docker, etc. — varía según el sistema operativo), pero la lista cambia con el tiempo, así que nunca asumas una versión exacta sin comprobarla.
- **Clave:** cada vez que corre un job, arranca en una **máquina completamente limpia**. Nada de lo que instalaste o generaste en una ejecución anterior sigue ahí en la siguiente.

---

## ⌨️ Actividad 4 — Un mismo job, tres sistemas operativos

1. En tu fork, crea el archivo `.github/workflows/runners.yml` con este contenido:

   ```yaml
   name: Explorando Runners

   on:
     workflow_dispatch:

   jobs:
     explorar:
       strategy:
         matrix:
           os: [ubuntu-latest, windows-latest, macos-latest]
       runs-on: ${{ matrix.os }}
       steps:
         - name: Decir en qué sistema operativo estoy
           run: echo "Corriendo en ${{ matrix.os }}"

         - name: Ver la versión de Git preinstalada
           run: git --version
   ```

2. Guarda el archivo con un commit directo a `main`. Eso disparará al checker del workshop, que te dará feedback aquí mismo.
3. Ve a la pestaña **Actions** → **"Explorando Runners"** → **Run workflow**, para verlo correr.
4. Fíjate que se crearon **tres jobs en paralelo**, uno por cada sistema operativo de la lista — eso es lo que hace `strategy.matrix`.
5. Abre el log de cada uno y compara la salida de `git --version` entre los tres sistemas.

> 💡 **Tip:** `${{ matrix.os }}` es una variable que `strategy.matrix` crea automáticamente y que puedes usar en cualquier parte del job, no solo en `runs-on`.
