# Bitácora Marítima

Guía independiente de trámites navales: embarcaciones, libretas de mar y certificación de personal ante la Secretaría de Marina (SEMAR), Unidad de Capitanías de Puerto y Asuntos Marítimos.

**No es un sitio oficial de SEMAR ni del Gobierno de México.** Es una herramienta de consulta y organización documental basada en formatos y requisitos publicados oficialmente.

## Contenido

- `index.html` — Landing page de venta (pago único, explicación del producto, FAQ).
- `tramites.html` — La bitácora completa: 24 trámites de embarcaciones, 18 de libretas de mar, directorio de capitanías y más, protegida detrás de una clave de acceso.
- `assets/` — Logo, favicon e imagen Open Graph.

## Estructura de carpetas

```
bitacora-maritima/
├── index.html              # Landing de venta
├── tramites.html           # App de la bitácora (protegida por clave)
├── tramites-original-backup.html   # Respaldo sin rediseño, por si se necesita
├── assets/
│   ├── logo-icon.svg       # Icono cuadrado (favicon, app icon)
│   ├── logo-horizontal.svg # Lockup horizontal (header)
│   ├── favicon-32.png
│   ├── favicon-192.png
│   ├── favicon-512.png
│   └── og-image.png        # Imagen para compartir en redes sociales
├── vercel.json
└── README.md
```

## Identidad visual

| Color | Hex | Uso |
|---|---|---|
| Azul marino | `#0C2D4E` | Fondos oscuros, texto de marca |
| Azul medio | `#15426E` | Acentos secundarios, oleaje del logo |
| Dorado | `#D4AF37` | Acento principal, ancla del logo, CTA |
| Dorado oscuro | `#A3791E` | Texto sobre fondos claros (mejor contraste que el dorado puro) |
| Marfil | `#F4EFE3` | Fondos suaves alternos |
| Blanco | `#FFFFFF` | Fondo base |

Tipografía: **Fraunces** (titulares, con carácter editorial/náutico) + **Inter** (cuerpo de texto, UI).

## Control de acceso

`tramites.html` incluye una pantalla de bloqueo que solicita una clave de acceso. Las claves válidas se gestionan manualmente en el array `VALID_CODES` dentro del script al final del archivo:

```js
var VALID_CODES = ["DEMO-2026", "MARINA-VIP"];
```

Flujo actual (manual, sin pasarela de pago):
1. La persona paga por el canal que definas (transferencia, WhatsApp, etc.).
2. Le envías manualmente una clave de la lista `VALID_CODES` (o agregas una nueva).
3. La persona la canjea en la landing (`index.html`) o directamente en `tramites.html`.
4. La clave se guarda en `localStorage` del navegador — no vuelve a pedirla en ese dispositivo.

Para agregar más claves, edita el array `VALID_CODES` y vuelve a desplegar. Si más adelante quieres automatizar el pago (Stripe, PayPal, etc.), esa lógica reemplazaría la verificación manual del array, pero el resto del flujo (gate, localStorage, redirect) no necesita cambiar.

## Desplegar en Vercel

1. Sube esta carpeta a un repositorio de GitHub.
2. En [vercel.com](https://vercel.com), importa el repositorio.
3. Framework preset: **Other** (es HTML estático, no necesita build).
4. Deploy. Vercel detectará `index.html` como página principal automáticamente.

## Desplegar en GitHub Pages (alternativa gratuita)

1. Sube esta carpeta a un repositorio de GitHub.
2. Ve a *Settings → Pages*.
3. En *Source*, selecciona la rama `main` y carpeta raíz (`/`).
4. Guarda. El sitio quedará disponible en `https://tu-usuario.github.io/nombre-repo/`.

## Actualizar contenido

Los datos de cada trámite viven en dos arreglos JavaScript dentro de `tramites.html`:

- `EMBCATS` — trámites de embarcaciones (24 actualmente).
- `LIBCATS` — trámites de libretas de mar (18 actualmente).

Cada entrada tiene `id`, `n` (nombre), `tl` (tipo/plazo), `sp` (datos clave como homoclave y vigencia), `docs` (lista de documentos requeridos) y `nota` (texto de cierre). Para agregar un trámite nuevo, se necesita además una fila clicable correspondiente en el listado visible (`<div class="row click" onclick="showDetEmb('id')">...`) con el mismo `id`.

## Aviso legal

Este proyecto recopila y organiza información pública de SEMAR con fines de consulta. Verifica siempre los requisitos, montos y formatos directamente en la capitanía de puerto correspondiente o en gob.mx/semar antes de presentar un trámite oficial.
