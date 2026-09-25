## ✅ ¡Paso 1 completo!

Tu workflow `runners.yml` corre el mismo job en tres sistemas operativos distintos usando `strategy.matrix`. 🎉

---

## 📘 Sesión 5 — Variables y contexts

**Teoría rápida:**

- **`env`**: variables propias que tú defines. Pueden ir a nivel workflow (aplica a todos los jobs), a nivel job (solo ese job) o a nivel step (solo ese step).
- **Contexts**: información que GitHub te da automáticamente sobre la ejecución actual, usando la sintaxis `${{ github.* }}`. Algunos de los más útiles:
  - `github.actor` → quién disparó el workflow.
  - `github.ref` → la rama o tag que disparó el evento.
  - `github.sha` → el hash del commit exacto.
- Dentro de un `run:`, para leer una variable de `env` en bash usas `$NOMBRE`; para leer un context usas la sintaxis `${{ }}` directamente.

---

## ⌨️ Actividad 5 — Imprime variables y contexts

Edita `.github/workflows/runners.yml` para que quede así:

```yaml
name: Explorando Runners

on:
  workflow_dispatch:

env:
  SALUDO: "Aprendiendo GitHub Actions"

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

      - name: Mostrar variables y contexts
        run: |
          echo "Mi variable: $SALUDO"
          echo "Quién disparó el workflow: ${{ github.actor }}"
          echo "Rama: ${{ github.ref }}"
          echo "Commit: ${{ github.sha }}"
```

Guarda con un commit directo a `main`. El checker revisará tu archivo y te dará feedback aquí. Después, corre el workflow manualmente desde **Actions** y confirma en el log que las cuatro líneas se imprimen correctamente en los tres sistemas operativos.

> 💡 **Tip:** los contexts no son exclusivos de `run:` — puedes usarlos en casi cualquier parte del YAML, incluyendo `if:`, `env:` o como parte de un nombre de step.
