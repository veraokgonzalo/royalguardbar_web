# PROGRESS.md — Royal Guard Bar

Registro de desarrollos del rediseño de royalguard.cl/bar.

---

## Estado actual

**Fase**: Mockup / propuesta de diseño  
**Última actualización**: 2026-05-18

---

## Completado

### 2026-05-18
- Mockup HTML autocontenido (`index.html`) con todas las secciones: nav, hero, info strip, carta preview, eventos, Instagram grid, mapa, newsletter, footer.
- Sistema de diseño documentado en `design.md`: paleta, tipografía, grilla, componentes, accesibilidad, copy guidelines.
- `CLAUDE.md` con guía de arquitectura para el repositorio.

---

## Pendiente

### Validación con cliente
- [ ] Revisar mockup en desktop y mobile con el cliente
- [ ] Confirmar copy (dirección, horarios, teléfono, email reales)
- [ ] Confirmar precios reales de la carta

### Assets
- [ ] Sesión de fotos: bar, platos destacados, terraza, equipo
- [ ] Reemplazar placeholders de Unsplash por fotos propias
- [ ] Confirmar licencia de fuentes reales (Lulo Clean, Brothers Bold, Neusa Demibold)
- [ ] Cargar fuentes reales y actualizar variables CSS en `:root`
- [ ] Logo SVG oficial (el actual es un placeholder construido a mano)

### Funcionalidad
- [ ] Burger menu (mobile) — toggle de visibilidad de `.nav-links`
- [ ] Validación del formulario de newsletter con mensaje de error visible
- [ ] Definir e integrar sistema de reservas
- [ ] Definir e integrar plataforma de newsletter
- [ ] Instagram feed: API oficial o servicio externo (SnapWidget u otro)

### Producción
- [ ] Separar CSS en archivos (`tokens.css`, `base.css`, `components.css`, `responsive.css`)
- [ ] Hero image con `<link rel="preload">` y `font-display: swap` en fuentes
- [ ] Convertir imágenes a WebP con fallback JPG
- [ ] SEO: `<title>`, `<meta description>`, Schema.org `BarOrPub`, Open Graph
- [ ] Configurar hosting (Netlify / Vercel) con deploy desde Git
- [ ] Lighthouse audit: target 90+ Performance, 90+ Accessibility
- [ ] QA en navegadores reales y lector de pantalla
- [ ] Integrar GA4 con tracking de clics en "Reservar", "Carta PDF" y "Cómo llegar"

---

## Log de sesiones

| Fecha | Descripción |
|---|---|
| 2026-05-18 | Creación del mockup inicial y documentación base |
