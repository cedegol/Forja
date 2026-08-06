# FORJA — Coach de transformación (PWA)

App personal de seguimiento del plan de transformación (informe 06/08/2026):
corte a **2.050 kcal**, **155 g de proteína**, rutina **PPL×2** con doble progresión,
objetivo **11–12 % de grasa**.

Sin build, sin dependencias, sin backend: un `index.html` con `localStorage`.
Funciona offline una vez instalada (service worker con caché del app shell).

## Estructura

```
forja/
├── index.html      # toda la app (UI + lógica + estado)
├── manifest.json   # metadata PWA (nombre, icono, standalone)
├── sw.js           # service worker: caché offline
├── icons/
│   ├── icon-192.png
│   └── icon-512.png
└── README.md
```

## Publicar en GitHub Pages (igual que Ritmo)

1. Crea un repo nuevo, p. ej. `forja` (público).
2. Sube estos archivos a la raíz del repo (o arrástralos en github.com → "Add file → Upload files").
3. En el repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**.
4. En 1–2 minutos queda en `https://TU-USUARIO.github.io/forja/`.

Por consola:

```bash
git init && git add . && git commit -m "FORJA v1"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/forja.git
git push -u origin main
```

## Instalar en iPhone

1. Abre la URL en **Safari** (no Chrome ni el navegador de Instagram).
2. Botón **Compartir** → **Añadir a pantalla de inicio**.
3. Se instala como app a pantalla completa con su icono. Ábrela siempre desde el icono.

## Datos y límites conocidos

- Todo se guarda en `localStorage` **de ese Safari/dispositivo**: no hay sync entre equipos todavía.
- iOS puede borrar el almacenamiento de una web que no abres en ~7 días — pero **no** el de una
  PWA instalada en pantalla de inicio: por eso instálala, no la uses desde la pestaña.
- Las fotos se comprimen a ~700 px JPEG antes de guardarse; el historial se limita a 20 fotos
  para no agotar la cuota (~50 MB en iOS). Borra las viejas desde Progreso → Fotos.
- Los "recordatorios" son una checklist configurable, no notificaciones push: push real en iPhone
  requiere un servidor de Web Push. Es el candidato natural para la v2 con Supabase
  (mismo esquema que Ritmo: auth anónima + tabla `estado` + Edge Function para push).

## Roadmap v2 (cuando lo pidas)

- [ ] Sync con Supabase (mismo patrón que Ritmo)
- [ ] Notificaciones push (comidas, entreno, pesaje)
- [ ] Exportar datos a CSV
- [ ] Gráfica de cargas por ejercicio (los datos ya se guardan por sesión)
