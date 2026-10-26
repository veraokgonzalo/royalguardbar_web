# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Proyecto

Rediseño de la página del **Royal Guard Bar** (bar físico de la marca Royal Guard, Av. Italia 1442, Barrio Italia, Providencia, Santiago). El objetivo es convertir la landing en una herramienta de captación: el visitante debe poder reservar, ver la carta y cómo llegar dentro del primer scroll.

## Flujo de trabajo

Después de cada desarrollo, abrir `index.html` en el navegador para verificar el resultado visualmente antes de reportar la tarea como terminada.

## Stack

HTML + CSS vanilla en un único archivo autocontenido (`index.html`). Sin framework, sin bundler, sin build step. Para previsualizar: abrir `index.html` directamente en el navegador.

El mockup usa Google Fonts como sustitutos temporales. En producción se reemplazan por las fuentes licenciadas (ver sección Tipografía).

## Sistema de diseño

### Paleta de colores (CSS variables en `:root`)

| Variable | Hex | Rol |
|---|---|---|
| `--navy` | `#114495` | Fondo principal, secciones, footer |
| `--navy-deep` | `#0c3274` | Nav, footer (más oscuro para separación) |
| `--mustard` | `#F6A605` | **Solo para acción**: botones CTA, links activos, eyebrows sobre navy, estados de focus |
| `--terracotta` | `#AF4C1B` | Acento secundario: bloque newsletter, badges, eyebrows sobre fondo claro |
| `--cream` | `#FAF5EA` | Fondo claro (sección Carta, Mapa) |
| `--ink` | `#0A1A33` | Texto sobre fondos claros |

Regla crítica: **el amarillo (`--mustard`) es solo para acción** — nunca para títulos decorativos ni etiquetas de contenido (ese fue el problema #3 del sitio original).

### Tipografía

Fuentes oficiales en `assets/fonts/oficial/`, cargadas con `@font-face` al inicio de `index.html`:

| Variable | Fuente | Uso |
|---|---|---|
| `--font-display` | Lulo Clean W01 One Bold | H1, H2, precios destacados, botones |
| `--font-impact` | Lulo Clean W01 One (regular) | Eyebrows, nav links, UI labels |
| `--font-body` | Neusa DemiBold | Cuerpo de texto, descripciones |

Lulo es muy ancha: usar `letter-spacing` bajo (≤ 0.08em) en textos largos como el menú.

### Breakpoints

- **≥ 960px**: layout completo, nav inline
- **560–959px**: grids de 4 → 2 columnas, nav colapsa a burger
- **< 560px**: una columna, paddings reducidos (32px → 22px)

## Arquitectura de la página

Secciones en orden:

1. **`.nav`** — Sticky, navy-deep. Logo lockup (SVG escudo + wordmark) · links principales · CTA "Reservar" (siempre visible) · sociales. En mobile colapsa a burger.
2. **`.hero`** — 88vh, imagen full-bleed con doble overlay (gradiente + radial) para garantizar contraste. Shield centrado, H1 con segunda línea en mustard, dos CTAs.
3. **`.info-strip`** — Banda de 4 columnas (Dirección, Horario, Reservas, Ambiente). Borde izquierdo mustard como acento.
4. **`.carta-section`** — Fondo cream. Grid de 4 tarjetas `.card` con imagen 4:3, categoría terracota, título, descripción y precio. CTA terciario terracota al final.
5. **`.split`** — Dos columnas sobre navy: eventos (lista con fecha grande mustard) + Instagram grid 3×3 con hover overlay.
6. **`.map-section`** — Fondo cream. Panel izquierdo navy (dirección, badge pet-friendly terracota, botón "Cómo llegar") + iframe Google Maps a la derecha.
7. **`.newsletter`** — Bloque terracota full-bleed. Form con nombre + email + botón mustard.
8. **`.footer`** — Navy-deep. 4 columnas: brand · dirección · links · info. Bottom bar con copyright y nota "+18 años".

## Convenciones del código

- **Selectores**: BEM-lite con clases descriptivas (`.nav-inner`, `.card-body`, `.evento-date`). Sin IDs para estilos.
- **Orden de propiedades CSS**: layout → box model → tipografía → colores → transiciones.
- **SVGs**: todos los logos e iconos son SVG inline (no fuentes de iconos). El escudo de Royal Guard existe en tres tamaños: 38×44 (nav), 54×62 (hero), 46×54 (footer).
- **Imágenes**: en producción → WebP con fallback JPG, `loading="lazy"` en todo excepto el hero. Hero necesita `<link rel="preload">`.
- **Accesibilidad**: cada `<section>` tiene `aria-label`, iconos decorativos llevan `aria-hidden="true"`, todos los interactivos tienen `aria-label` o texto visible.

## Copy y contenido

- **Idioma**: español de Chile. Tono cercano sin ser informal extremo ("merecido relajo", "schop" están OK).
- **Precios**: formato `$4.500` (punto como separador de miles, sin decimales).
- **Horarios**: guion en-dash (`–`) entre horas (no guion corto `-`).
- **Dirección canónica**: "Av. Italia 1442, Providencia" (siempre con mayúsculas correctas).

## Archivos de referencia

| Archivo | Contenido |
|---|---|
| `design.md` | Especificaciones completas de diseño: paleta, tipografía, componente por componente, accesibilidad, checklist de cambios vs. sitio actual |
| `design_oficial.png` | Screenshot del sitio actual (referencia "antes") |
| `royal bar COLORES Y FUENTES.pdf` | Manual de marca oficial de Royal Guard |
| `Aniversario Royal Bar 03-12-25 091.jpg` | Fotografía de referencia del bar |

## Integraciones pendientes (a definir con el cliente)

- Sistema de reservas (OpenTable / Restorando / form propio)
- Newsletter (Mailchimp / Brevo)
- Instagram feed (API oficial o SnapWidget)
- Analytics: GA4 con tracking de clics en "Reservar", "Carta PDF" y "Cómo llegar"
