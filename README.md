# Mundial FIFA 2026 Colombia PWA

Esta carpeta contiene la versión instalable para iPhone del calendario móvil.

## Archivos principales

- `index.html`: app principal.
- `manifest.webmanifest`: configuración de la PWA.
- `service-worker.js`: cache de la app para carga rápida y uso parcial sin conexión.
- `icons/`: íconos para iOS y navegadores modernos.

## Cómo probarla en computador

Abre `index.html` para revisar el diseño. Algunas funciones PWA, como instalación y service worker, requieren que el sitio esté publicado en HTTPS o corriendo en localhost.

## Cómo instalarla en iPhone

1. Publica la carpeta completa en un hosting con HTTPS, por ejemplo GitHub Pages, Netlify, Vercel o un sitio interno permitido.
2. Abre la URL publicada desde Safari en el iPhone.
3. Toca Compartir.
4. Toca Agregar a pantalla de inicio.
5. Confirma el nombre: Mundial 2026 COL.

## Nota operativa

El calendario, filtros y datos principales quedan dentro de la app. Las imágenes de estadios se cargan desde fuentes públicas externas y pueden requerir conexión la primera vez que se visualizan.
