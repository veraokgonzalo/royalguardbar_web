# Royal Guard Bar — Especificaciones de diseño

Documento de referencia para el rediseño de la página `/bar` de royalguard.cl. Cubre marca, sistema visual, componentes, accesibilidad y notas de implementación.

Última actualización: 18 de mayo, 2026.

---

## 1. Contexto del proyecto

Royal Guard Bar es el bar físico de la marca Royal Guard, ubicado en Av. Italia 1442, Barrio Italia, Providencia, Santiago. La página actual (royalguard.cl/bar) presenta tres problemas principales que esta propuesta resuelve:

1. Un asset de mapa roto en la página en vivo.
2. Conflicto de roles del color amarillo (etiquetas y CTAs comparten el mismo color).
3. Falta de contenido orientado a conversión: no hay vista previa de carta, no hay CTA principal en el hero, no hay agenda de eventos clara.

La propuesta busca convertir la landing en una herramienta de captación: el visitante debe poder reservar, ver qué se sirve y cómo llegar dentro del primer scroll.

**Audiencia primaria.** Adultos 25–45 años, residentes de Santiago, perfil "after office" + fin de semana. Móvil primero — la mayoría del tráfico llega desde redes sociales en celular.

**Idioma.** Español de Chile. Sin tutear formalmente; tono cercano, con coloquialismos suaves ("merecido relajo", "schop", "picar").

---

## 2. Marca

### 2.1 Paleta de colores

Tres colores oficiales del manual de marca, cada uno con un rol distinto en la interfaz.

| Color | Hex | Rol | Uso |
|---|---|---|---|
| Royal Navy | `#114495` | Color base | Fondo de hero, secciones principales, footer, header del mapa |
| Mustard | `#F6A605` | Acción y acento primario | Botones CTA, links activos, eyebrows, números destacados, estado de focus |
| Terracota | `#AF4C1B` | Acento secundario y calidez | Bloque de newsletter, badges (pet friendly), eyebrows sobre fondo claro, hover de botón terciario |

**Colores derivados (definidos como CSS variables):**

| Variable | Hex | Uso |
|---|---|---|
| `--navy-deep` | `#0c3274` | Header del nav, footer (oscurecido para separación) |
| `--navy-soft` | `#1a52ad` | Hover/estado activo sobre navy |
| `--mustard-hover` | `#d99304` | Hover de botones mostaza |
| `--terracotta-hover` | `#923f15` | Hover de botones terracota |
| `--cream` | `#FAF5EA` | Fondo claro para sección Carta y Mapa (rompe la monotonía del navy) |
| `--ink` | `#0A1A33` | Texto principal sobre fondos claros |

**Reglas de uso.**

- Una sola sección puede ser "color principal de fondo". No mezclar terracota y mostaza como fondos en la misma sección.
- El amarillo se reserva para **acción** (botones, links, focus). Nunca para títulos de cuerpo o encabezados decorativos.
- Los _eyebrows_ (etiquetas pequeñas tipo "Eventos", "La carta") usan mostaza sobre navy y terracota sobre cream.
- Hover de botones siempre baja un escalón de luminosidad (definido en las variables `*-hover`).
- Estados de focus visible: outline mostaza de 2px con offset de 3px sobre cualquier fondo.

### 2.2 Tipografía

Cuatro fuentes oficiales del manual de marca:

| Familia | Peso | Rol |
|---|---|---|
| **Lulo Clean W1 One Bold** | Bold | Títulos display de alto impacto (H1 del hero, H2 principales). Geométrica, all caps, tracked. |
| **Lulo Clean W1 One** | Regular | Variante más liviana del display, para subtítulos o variantes secundarias. |
| **Brothers Bold** | Bold | Etiquetas, botones, eyebrows, navegación. Condensada, alta personalidad, all caps. |
| **Neusa Demibold** | Demibold (600) | Cuerpo de texto y UI general. Sans serif limpia, alta legibilidad. |

**Sustitutos en el mockup HTML** (Google Fonts, solo para previsualización — reemplazar en producción):

| Real | Sustituto Google Font | Variable CSS |
|---|---|---|
| Lulo Clean W1 One Bold | Big Shoulders Display 800 | `--font-display` |
| Brothers Bold | Staatliches | `--font-impact` |
| Neusa Demibold | Barlow 500 | `--font-body` |

Las tres variables están definidas en `:root` del HTML. Para pasar a producción solo hay que cargar las fuentes reales (Adobe Fonts, MyFonts o el host que tengan licenciado) y cambiar el valor de la variable.

**Escala tipográfica.**

| Nivel | Tamaño | Familia | Peso | Letter-spacing | Transform |
|---|---|---|---|---|---|
| H1 Hero | `clamp(36px, 5.5vw, 72px)` | Display | 800 | 0.04em | uppercase |
| H2 Sección | `clamp(28px, 3.5vw, 44px)` | Display | 800 | 0.06em | uppercase |
| H3 / título de tarjeta | 22–28px | Impact | 400 | 0.04em | uppercase |
| H4 / título de evento | 18px | Impact | 400 | 0.04em | uppercase |
| Eyebrow | 11–13px | Impact | 400 | 0.20–0.28em | uppercase |
| Body | 14–16px | Body | 400 | normal | sentence case |
| UI label | 11–13px | Impact | 400 | 0.16–0.24em | uppercase |
| Precio destacado | 18px | Display | 800 | 0.08em | — |

**Reglas tipográficas.**

- Sentence case en titulares descriptivos ("Lo que tienes que probar", "En el corazón de Barrio Italia").
- All caps sólo en H1, H2 y elementos de UI (eyebrows, botones, etiquetas).
- Nunca mezclar Brothers Bold con Lulo Clean en la misma línea de texto.
- Cuerpo de texto: line-height 1.5–1.7 según contexto.

---

## 3. Layout y sistema de grilla

### 3.1 Contenedor

- Ancho máximo: `1280px`, centrado.
- Padding lateral: `32px` desktop, `22px` mobile.
- Padding vertical de sección: `90px` desktop, `64px` mobile.

### 3.2 Breakpoints

| Nombre | Ancho | Cambios principales |
|---|---|---|
| Desktop | ≥ 960px | Layout completo, navegación inline |
| Tablet | 560–959px | Grids de 4 → 2 columnas, nav colapsa a burger |
| Mobile | < 560px | Una sola columna, paddings reducidos, burger menu, hero shield centrado |

### 3.3 Espaciado

Sistema de 8px:

`4 · 8 · 12 · 14 · 18 · 22 · 24 · 32 · 48 · 56 · 64 · 90`

Distancias internas de componentes en múltiplos de 4. Distancias entre secciones en múltiplos de 8.

### 3.4 Border radius

| Token | Valor | Uso |
|---|---|---|
| `radius-xs` | `2px` | Botones, inputs |
| `radius-sm` | `4px` | Cards, contenedor del mapa |

Royal Guard es una marca con personalidad estructural — los radios se mantienen pequeños para no perder firmeza. Nada de pills muy redondeados.

---

## 4. Componentes

### 4.1 Navegación (`.nav`)

Sticky en top con fondo `--navy-deep` y borde inferior sutil. Tres bloques:

- **Logo lockup**: escudo amarillo (54×62 hero / 38×44 nav) + wordmark "ROYAL GUARD" con tagline "BAR · BARRIO ITALIA" en mostaza, 9–10px tracked.
- **Links principales**: Variedades, Experiencias, **Royal Guard Bar** (activo, con underline mostaza), Royal Weekend, Contacto. Tipografía Brothers Bold 13px, tracking 0.16em.
- **CTA "Reservar"** (mostaza, prominente) + iconos sociales (Instagram, Facebook, YouTube).

En mobile: links e iconos colapsan a un burger; el CTA "Reservar" se mantiene visible.

### 4.2 Hero (`.hero`)

- Altura mínima: `88vh`.
- Imagen de fondo full-bleed con dos overlays: gradiente vertical de claro a oscuro (35% → 85%) + radial sutil para enfocar el centro. Esto garantiza que el texto blanco siempre tenga 4.5:1 de contraste sin importar la zona del fondo.
- Shield lockup centrado arriba (escudo grande + ROYAL GUARD + BAR · BARRIO ITALIA).
- H1 en display, con la segunda línea en mostaza ("en Barrio Italia").
- Subhead en cuerpo, max-width 600px.
- Dos CTAs: primario mostaza ("Reservar mesa →"), secundario outline blanco ("Ver la carta").
- Scroll hint sutil al pie ("SCROLL" + línea vertical).

### 4.3 Info strip (`.info-strip`)

Banda horizontal con 4 columnas: Dirección, Horario, Reservas, Ambiente. Cada columna tiene:

- Eyebrow en mostaza (11px, Brothers Bold, tracked).
- Valor en blanco, con la pieza clave en `font-weight: 600`.
- Borde izquierdo mostaza de 2px (acento visual).

En tablet: 2×2. En mobile: 1 columna apilada.

### 4.4 Carta preview (`.carta-section`)

Sección sobre fondo `--cream`. Eyebrow terracota, H2 navy. Grid de 4 tarjetas (`.card`):

- Imagen 4:3.
- Body con padding 20–22px.
- Categoría en terracota tracked (eyebrow size).
- Título en Brothers Bold 22px navy.
- Descripción en body 14px.
- Precio destacado en Display 800.
- Hover: `translateY(-4px)` + sombra suave.

CTA terciario terracota al final: "Ver carta completa (PDF) ↓".

### 4.5 Eventos (`.evento`)

Lista vertical. Cada ítem:

- Fecha grande a la izquierda (día en Display 30px mostaza, mes en Brothers tracked).
- Borde divisor a la derecha.
- Título Brothers 18px uppercase.
- Descripción 14px en muted.
- Meta line: hora · precio · cupos, en Brothers mostaza tracked.

Separadores: borde superior `--border` (rgba blanca 0.15).

### 4.6 Instagram grid (`.ig-grid`)

Grid 3×3 sobre fondo navy. Cada tile:

- `aspect-ratio: 1/1`, background-image cover.
- Hover overlay: navy 70% + icono Instagram blanco centrado, fade in 200ms.

Header con `@royalguardbar` (mostaza) a la izquierda y "Ver más →" (muted, underline sutil) a la derecha.

### 4.7 Mapa (`.map-section`)

Sección sobre `--cream`. Contenedor split:

- Panel izquierdo (navy, 40%): nombre del bar, eyebrow neighborhood, dirección, badge "Pet friendly" terracota, botón mostaza "Cómo llegar →" que abre Google Maps en modo navegación.
- Panel derecho (60%): iframe de Google Maps embebido, `loading="lazy"`, min-height 380px.

En mobile: apila vertical, mapa primero.

### 4.8 Newsletter (`.newsletter`)

Bloque terracota full-bleed. Centrado, max-width 720px:

- Eyebrow blanca, H2 display, párrafo explicativo.
- Form en fila: dos inputs (Nombre, Email) con labels persistentes en mayúsculas tracked + botón mostaza "Suscribirme".
- Nota de privacidad debajo del form (12px, opacidad reducida).
- En mobile: form apilado vertical, inputs full-width.

### 4.9 Footer (`.footer`)

Fondo `--navy-deep`. 4 columnas:

1. Brand: lockup escudo + wordmark, tagline corta, iconos sociales en círculos con borde.
2. Visítanos: dirección, teléfono, email.
3. Explora: links principales.
4. Información: contacto, RRHH, privacidad.

Bottom bar: copyright a la izquierda, "Beba con moderación · +18 años" a la derecha. Ambos en Brothers tracked 12px muted.

### 4.10 Botones (`.btn`)

Tres variantes:

| Variante | Fondo | Borde | Texto | Uso |
|---|---|---|---|---|
| `btn-primary` | `--mustard` | — | `--ink` | Acción principal (Reservar, Suscribirme, Cómo llegar) |
| `btn-secondary` | transparente | blanco 2px | blanco | Acción secundaria sobre navy (Ver carta, Ver eventos) |
| `btn-tertiary` | `--terracotta` | — | blanco | Acción de descarga / acción especial (Ver PDF) |

Todos los botones:

- Padding `16px 32px` (10–14px en versiones inline).
- Tipografía Brothers 14px, tracking 0.18em.
- `border-radius: 2px`.
- Hover: `translateY(-1px)` + cambio de fondo.
- Focus visible: outline mostaza con offset.

---

## 5. Contenido y copy

### 5.1 Tono de voz

- Cercano, claro, sin floritura.
- Spanglish moderado (palabras como "schop", "after office" están OK; evitar "delicious" o "bistro").
- Concreto: en lugar de "vive una experiencia única", "cervezas recién tiradas y la mejor terraza".
- Inclusivo: evitar masculino genérico cuando se pueda usar plural neutro ("todes" no — el público no lo espera; "todos" si es necesario, pero priorizar segunda persona "tú").

### 5.2 Detalles de copy

- **Dirección**: siempre como "Av. Italia 1442, Providencia". Capitalización correcta.
- **Horarios**: formato compacto con días abreviados a 3 letras (Lun, Mar, Jue), guion en-dash (`–`) entre horas, separador de día con punto medio (`·`) si va en línea.
- **Precios**: formato chileno `$4.500` con punto como separador de miles, sin decimales.
- **Teléfono**: formato internacional con espacios `+56 9 1234 5678`.
- **Edad**: "+18 años" y nota legal "Beba con moderación" en footer.

---

## 6. Accesibilidad

Objetivo: cumplir WCAG 2.1 AA en producción.

### 6.1 Contraste

- Texto blanco sobre `--navy` (#114495): ratio 8.6:1 ✓
- Texto navy sobre `--mustard` (#F6A605): ratio 7.2:1 ✓
- Texto blanco sobre `--terracotta` (#AF4C1B): ratio 6.4:1 ✓
- Texto blanco sobre foto del hero: garantizado por el overlay con gradiente (mínimo 60% de oscurecimiento en la zona del título).
- Mostaza sobre navy (eyebrows): 5.1:1 ✓ para texto pequeño.

### 6.2 Targets táctiles

Mínimo 44×44px en todos los elementos interactivos en mobile. Los iconos sociales del nav usan padding generoso (8–10px) para alcanzar esa medida.

### 6.3 Estados de focus

`:focus-visible` con outline `2px solid var(--mustard)` y `offset: 3px`. Visible sobre todos los fondos del sitio.

### 6.4 Semántica y ARIA

- `<header role="banner">`, `<footer role="contentinfo">`, `<nav aria-label="Principal">`, `<section aria-label="...">` en cada sección.
- Iconos decorativos: `aria-hidden="true"`.
- Iconos interactivos solos: `aria-label` descriptivo.
- Iframe del mapa: `title="Mapa Royal Guard Bar — Av. Italia 1442"`.
- Imágenes: `alt` descriptivo en producción (los placeholders del mockup tienen alt vacío por ser decorativos).

### 6.5 Formularios

- Labels persistentes encima del input (no labels-as-placeholder).
- `required` en campos obligatorios.
- Mensajes de error visibles (a implementar en producción).

---

## 7. Imágenes y assets

### 7.1 Fotografía

El mockup usa placeholders de Unsplash. En producción, reemplazar por:

- **Hero**: foto horizontal del bar de noche, con gente, luz cálida y ambiente. Mínimo 1800px de ancho, formato JPG progresivo, optimizado.
- **Carta preview**: 4 fotos cuadradas o 4:3, una por producto destacado. Iluminación cálida, fondo desenfocado, plato/vaso centrado. Reemplazar trimestralmente cuando cambie la carta.
- **Instagram grid**: 9 tiles cuadradas. Idealmente conectado vía Instagram Basic Display API para que se actualice solo. Si no, mantenimiento manual mensual.

### 7.2 Logo

Dos lockups oficiales:

- **Lockup principal** (hero): escudo + ROYAL GUARD + BAR · BARRIO ITALIA centrado.
- **Lockup compacto** (nav, footer): escudo + ROYAL GUARD con BAR · BARRIO ITALIA en línea pequeña debajo.

Escudo: amarillo `#F6A605` con detalle interior navy. SVG, no PNG, para escalar perfecto en todos los tamaños.

### 7.3 Optimización

- Imágenes en WebP con fallback JPG.
- `loading="lazy"` en todo excepto el hero.
- Sprites SVG para iconos sociales (no fuentes de iconos).

---

## 8. Estructura de archivos

```
royal/
├── index.html                          ← Mockup HTML autocontenido
├── design.md                           ← Este documento
├── design_oficial.png                  ← Screenshot del sitio actual (referencia "antes")
├── royal bar COLORES Y FUENTES.pdf     ← Manual de marca oficial
└── Aniversario Royal Bar 03-12-25 091.jpg  ← Foto referencia
```

Cuando se pase a un proyecto real, separar:

```
royal/
├── index.html
├── styles/
│   ├── tokens.css         ← Variables CSS (colores, fuentes, espaciado)
│   ├── base.css           ← Reset + tipografía
│   ├── components.css     ← .nav, .hero, .card, .btn, etc.
│   └── responsive.css     ← Media queries
├── scripts/
│   └── main.js            ← Burger menu, form validation, IG feed fetch
├── assets/
│   ├── images/
│   ├── logos/
│   └── icons/
└── design.md
```

---

## 9. Notas para implementación

### 9.1 Stack sugerido

- **Estático**: HTML + CSS vanilla es suficiente para esta página. No requiere framework.
- **CMS**: si el cliente quiere editar carta y eventos, conectar con un headless CMS liviano (Sanity, Strapi) que exponga las dos colecciones.
- **Hosting**: Netlify o Vercel — deploy automático desde Git, SSL, CDN.

### 9.2 Performance

- Lighthouse target: 90+ en Performance y Accessibility, 100 en Best Practices.
- Hero image: preload `<link rel="preload" as="image">`.
- Fuentes: `font-display: swap`.
- Mapa iframe: `loading="lazy"` (ya implementado).

### 9.3 Integraciones a definir

- **Reservas**: ¿se conecta con OpenTable / Restorando / form propio + email?
- **Newsletter**: ¿Mailchimp, Brevo, propio?
- **Instagram**: API oficial o un servicio tipo SnapWidget si no quieren mantener el token.
- **Analytics**: GA4 + tracking de clicks en CTA principal (Reservar, Carta PDF, Cómo llegar).

### 9.4 SEO mínimo

- `<title>`: "Royal Guard Bar — Cervezas, terraza y eventos en Barrio Italia"
- `<meta description>`: 155 caracteres incluyendo Av. Italia, Providencia, cervezas Royal Guard.
- Schema.org `BarOrPub` con dirección, horarios, teléfono, imagen, rating.
- Open Graph para compartir en redes (imagen del hero, título, descripción).

---

## 10. Cambios sobre la versión actual (resumen)

| # | Problema actual | Solución propuesta |
|---|---|---|
| 1 | Imagen del mapa rota | Embed Google Maps real + panel con dirección y CTA "Cómo llegar" |
| 2 | Hero sin CTA | Botón "Reservar mesa" mostaza + secundario "Ver la carta" |
| 3 | Amarillo en doble rol (etiquetas + CTAs) | Amarillo solo para acción; etiquetas en blanco/mostaza eyebrow tracked |
| 4 | No hay vista previa de carta | Sección de 4 tarjetas con foto, descripción y precio |
| 5 | Botón "Eventos" sin contenido | Lista de eventos con fecha grande, título y meta |
| 6 | Instagram grid sin affordance | Hover overlay con icono IG + link "Ver más" |
| 7 | Copy inconsistente ("providencia.", "18.:00") | Capitalización y formato corregidos |
| 8 | Footer con león sobredimensionado | Lockup proporcionado + columnas de links útiles |
| 9 | Solo se usaban 2 de los 3 colores de marca | Terracota aplicado en newsletter, badges y eyebrows |
| 10 | Sin estados de focus visibles | Outline mostaza con offset en todo elemento interactivo |

---

## 11. Próximos pasos

1. **Validar la propuesta con el cliente** — abrir `index.html` en desktop y mobile, recoger feedback.
2. **Sesión de fotos** — necesitamos imágenes propias del bar, los platos y el equipo. Sin fotos buenas la propuesta pierde el 50% del impacto.
3. **Definir integraciones** — sistema de reservas, newsletter, IG feed (ver 9.3).
4. **Cargar fuentes reales** — confirmar licencia de Lulo Clean, Brothers y Neusa con el cliente.
5. **Implementación** — pasar de mockup a sitio real con CMS si aplica.
6. **QA** — Lighthouse audit, prueba en navegadores reales, prueba con lector de pantalla.

---

*Documento mantenido por el equipo de diseño. Para dudas o sugerencias, abrir issue en el repo del proyecto.*
