# Mundial FIFA 2026 Colombia PWA

Calendario móvil instalable (PWA) del Mundial FIFA 2026 con horarios de Colombia (COT), canales de TV, plataformas de streaming y estadios oficiales.

## Funciones

- **Calendario completo** de los 104 partidos con horario de Colombia, fase, grupo y estadio.
- **Canales y streaming por partido**, con los nombres de cada operador como **enlaces directos** a su sitio oficial.
- **Sección "Dónde ver"**: todos los canales y plataformas de Colombia agrupados por TV abierta y pago/streaming, con acceso directo a cada sitio.
- **Filtros y búsqueda** por equipo, ciudad, canal o estadio.
- **Vista de estadios** con capacidad oficial.
- **Instalable como app** en iPhone/Android y uso parcial sin conexión gracias al service worker.

## Archivos principales

- `index.html`: app principal (única fuente de verdad).
- `mundial_fifa_2026_colombia_movil_pwa.html`: redirección a `index.html` (mantiene el enlace antiguo).
- `manifest.webmanifest`: configuración de la PWA.
- `service-worker.js`: cache de la app para carga rápida y uso parcial sin conexión.
- `icons/`: íconos para iOS y navegadores modernos.
- `.nojekyll`: evita el procesamiento Jekyll en GitHub Pages.

## Cómo probarla en el computador

Las funciones PWA (instalación y service worker) requieren HTTPS o `localhost`. Para una prueba local:

```bash
# Python 3
python -m http.server 8080
# luego abre http://localhost:8080
```

Abrir `index.html` con doble clic sirve para revisar el diseño, pero el service worker no se registrará desde `file://`.

## Publicar en GitHub Pages

1. Sube esta carpeta al repositorio (la raíz debe contener `index.html`).
2. En GitHub: **Settings → Pages**.
3. En **Source** elige la rama (`main`) y la carpeta (`/root` o `/docs` según donde esté el contenido).
4. Guarda. La URL publicada quedará como `https://<usuario>.github.io/<repo>/`.

Todas las rutas son relativas (`./`), por lo que la app funciona correctamente bajo el subdirectorio del repositorio. El archivo `.nojekyll` evita que GitHub procese el sitio con Jekyll.

## Cómo instalarla en iPhone

1. Abre la URL publicada (HTTPS) desde Safari.
2. Toca **Compartir**.
3. Toca **Agregar a pantalla de inicio**.
4. Confirma el nombre: **Mundial 2026 COL**.

## Nota operativa

El calendario, filtros y datos principales quedan dentro de la app. Las imágenes de estadios y los logos de los canales se cargan desde fuentes públicas externas (los logos usan el servicio de favicons de DuckDuckGo) y pueden requerir conexión la primera vez; si no cargan, cada canal muestra un monograma de respaldo. Los enlaces de canales y plataformas abren los sitios oficiales de cada operador; la cobertura exacta de la fase final puede ajustarse según la programación oficial.
