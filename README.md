# Mundial FIFA 2026 Colombia PWA

Calendario móvil instalable (PWA) del Mundial FIFA 2026 con horarios de Colombia (COT), canales de TV, plataformas de streaming y estadios oficiales.

## Funciones

- **Calendario completo** de los 104 partidos con horario de Colombia, fase, grupo y estadio.
- **Canales y streaming por partido**, con los nombres de cada operador como **enlaces directos** a su sitio oficial.
- **Sección "Dónde ver"**: todos los canales y plataformas de Colombia agrupados por TV abierta y pago/streaming, con acceso directo a cada sitio.
- **Filtros y búsqueda** por equipo, ciudad, canal o estadio.
- **Selector de día tipo calendario**: una tira de fechas para saltar a cualquier jornada con un toque.
- **Filtro por país**: menú desplegable para ver solo los partidos de una selección.
- **Vista de estadios** con capacidad oficial.
- **Calendario por días plegable**: en "Todos" solo se abre el día de hoy (o el próximo día con partidos); el resto queda colapsado.
- **Hoy y próximos primero**: los días que ya pasaron se encogen y se mueven bajo "Resultados anteriores"; arriba quedan el día actual y los siguientes.
- **Tema claro u oscuro**: botón ☀️/🌙 para cambiar de versión; respeta la preferencia del sistema y recuerda tu elección.
- **Resultados en vivo**: marcadores en tiempo real dentro de las tarjetas (badge `EN VIVO`/`Finalizado`) y alertas de gol y resultado final mediante avisos en la app.
- **Resultados anteriores**: los partidos jugados muestran su marcador final automáticamente (se cargan al abrir, sin activar el modo en vivo).
- **Cruces que se actualizan solos**: a medida que avanza el torneo, las eliminatorias reemplazan los marcadores de posición ("Segundo Grupo A", "Ganador Partido 74") por los **equipos reales que clasifican** (emparejados por fecha + sede desde ESPN). Colombia se resalta en dorado también en fase final.
- **Tablas de posiciones**: tabla de cada uno de los 12 grupos (PJ, DG, Pts), con las dos primeras posiciones resaltadas.
- **Goleadores**: ranking de máximos artilleros del torneo con su selección y número de goles.
- **Instalable como app** en iPhone/Android y uso parcial sin conexión gracias al service worker.

## Resultados en vivo (configuración)

El modo en vivo usa por defecto el **marcador público de ESPN** (`site.api.espn.com`), que es **gratis, sin clave y con CORS**, así que funciona directo desde GitHub Pages sin backend. Solo activa el botón **En vivo** en la app. Cuando hay partidos en juego muestra el marcador y dispara avisos de gol y de resultado final.

Los **resultados anteriores** (marcador de cada día), las **tablas de posiciones** y los **goleadores** vienen de los mismos endpoints públicos de ESPN (rango de fechas del scoreboard y `.../standings`); también son gratis, sin clave y con CORS, y se cargan solos.

Configuración en `LIVE_CONFIG` dentro de `index.html`:

```js
const LIVE_CONFIG = {
  espn: 'https://site.api.espn.com/apis/site/v2/sports/soccer/fifa.world/scoreboard',
  endpoint: '',   // opcional: tu propio proxy; si lo defines, tiene prioridad sobre ESPN
  pollMs: 30000,  // frecuencia de actualización
  demo: false
};
```

- **ESPN (por defecto)**: no requiere nada. Si ESPN cambiara la ruta de la liga del Mundial, ajusta `espn`. Los nombres de equipo de ESPN (inglés) se emparejan con el calendario por dupla de selecciones; la fase final mapea cuando se conozcan los clasificados.
- **Proxy propio (opcional)**: si prefieres otro proveedor (p. ej. football-data.org de pago/gratis), pon un `endpoint` a un **proxy serverless** (Cloudflare Workers, Netlify, Vercel) que devuelva `[{ "n": 1, "hs": 2, "as": 1, "status": "live", "minute": 67 }]`. El proxy mantiene la clave del API fuera del navegador.
- Las alertas de gol/resultado son avisos **dentro de la app** mientras está abierta. Las notificaciones push con la app cerrada requerirían además un backend que envíe Web Push (no incluido).
- Para una **demostración** sin partidos reales en juego, abre la app con `?demo=1` (por ejemplo `index.html?demo=1`): simula partidos en vivo, goles y resultados finales.

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
