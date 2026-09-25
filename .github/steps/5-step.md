## ✅ ¡Paso 2 completo!

Tu workflow ya usa una variable propia (`env`) y tres contexts distintos de GitHub. 🎉

---

## 📘 Sesión 6 — Secrets

**Teoría rápida:**

- Un **secret** es un valor sensible (API key, contraseña, token) que necesitas usar en un workflow **sin** escribirlo directamente en el YAML.
- Se configuran en **Settings → Secrets and variables → Actions → New repository secret**. Quedan cifrados y nadie puede volver a ver su valor, solo reemplazarlo.
- Se usan en el workflow con `${{ secrets.NOMBRE_DEL_SECRET }}`.
- GitHub **enmascara automáticamente** cualquier secret que aparezca en un log, aunque lo imprimas con un simple `echo` — lo verás como `***`.
- Regla de oro: **nunca** pegues un valor sensible directo en el YAML. Si algún día lo hicieras por error, ese valor queda en el historial de Git para siempre, aunque lo borres después.

---

## ⌨️ Actividad 6 — Configura y usa tu primer secret

1. Ve a **Settings → Secrets and variables → Actions → New repository secret**.
2. **Name:** `WORKSHOP_SECRET`
3. **Secret:** escribe cualquier valor de prueba, por ejemplo `mi-valor-super-secreto-123`.
4. Guarda el secret.
5. Ahora edita `.github/workflows/runners.yml` para agregar un último step:

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

         - name: Usar un secret sin exponerlo
           run: echo "Mi secret configurado es: ${{ secrets.WORKSHOP_SECRET }}"
   ```

6. Guarda con un commit directo a `main`. El checker revisará tu archivo aquí mismo.
7. Corre el workflow manualmente desde **Actions** y abre el log del último step. En vez de tu valor de prueba, deberías ver algo como `Mi secret configurado es: ***`.

> 💡 **Tip:** si el log muestra el valor completo en vez de `***`, revisa que el nombre del secret en Settings coincida exactamente con `WORKSHOP_SECRET` (mayúsculas incluidas) y con lo que escribiste en el YAML.
