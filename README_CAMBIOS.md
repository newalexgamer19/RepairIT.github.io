# README - Mejoras de Accesibilidad y Usabilidad · Repair IT

## Resumen de cambios aplicados

Todos los cambios afectan a los archivos: `index.html`, `consolas.html`, `movil.html`, `ordenadores.html`.
Los archivos CSS (`Estils_bootstrap.css`, `estils_serveis_general.css`) y los demás recursos (imágenes, vídeo, audio) **no se han modificado**.

---

## ✅ Accesibilidad (WCAG 2.1 AA)

### 1. Skip link (enlace de salto)
- Añadido `<a href="#main-content" class="skip-link">Saltar al contenido principal</a>` al inicio de cada página.
- Permite a usuarios de teclado y lectores de pantalla saltar directamente al contenido sin pasar por la navegación.
- El enlace es invisible hasta recibir foco (`:focus { top: 0 }`).

### 2. Texto alternativo descriptivo en todas las imágenes
- **Antes:** `alt="PC"`, `alt="Consolas"`, `alt="Móviles"`, `alt="reparación"`, `alt="Logo"`, `alt="Reseña 1"` — textos genéricos o vacíos de significado.
- **Después:** textos descriptivos del contenido real de la imagen. Ejemplos:
  - `alt="Técnico reparando pantalla rota de un móvil iPhone y Android"`
  - `alt="Consola PlayStation desmontada para reparación de lector Blu-ray"`
  - `alt="Portátil reparado por Repair IT, pantalla y componentes nuevos"`
  - `alt="Logotipo de Repair IT"` (en lugar de `alt="Logo"`)

### 3. Formularios accesibles con `<label>` y `aria-label`
- **Antes:** todos los campos del formulario usaban solo `placeholder`, sin `<label>` asociado. Los `<input>`, `<select>` y `<textarea>` no tenían `id` ni `name`.
- **Después:**
  - Cada campo tiene `<label for="id">` vinculado mediante `id` en el control.
  - Añadido `aria-required="true"` en campos obligatorios.
  - `aria-describedby` en campos con texto de ayuda adicional.
  - El formulario tiene `aria-label` descriptivo.
  - El `<form>` lleva atributo `novalidate` para controlar la validación.

### 4. Navegación por teclado
- **Skip link:** primer elemento focusable de cada página.
- **Botón hamburguesa del navbar:** ya tenía `aria-label`; añadido `aria-controls` y `aria-expanded` donde faltaban.
- **Carrusel (index.html):**
  - Los puntos de navegación cambiados de `<div>` a `<button>` (elementos focusables por defecto).
  - Añadida navegación con flechas de teclado (`ArrowLeft`/`ArrowRight`).
  - Pausa automática al recibir foco (`focusin`/`focusout`).
  - Respeto a `prefers-reduced-motion`: si el usuario prefiere movimiento reducido, el carrusel no avanza automáticamente.
- **`:focus-visible`** añadido globalmente con `outline: 3px solid #00ccff` para visibilidad clara del foco.

### 5. Roles ARIA y semántica HTML
- `<header role="banner">`, `<footer role="contentinfo">`, `<main id="main-content">`.
- `<nav role="navigation" aria-label="Navegación principal">`.
- `<nav aria-label="Redes sociales">` en el footer (separado del nav principal).
- Carrusel: `aria-label`, `aria-live="polite"`, `role="group"`, `aria-roledescription="carrusel"/"diapositiva"`, `aria-label="Diapositiva N de 3"`.
- Dots del carrusel: `role="tablist"` + `role="tab"` + `aria-selected`.
- Listas de marcas en footer: `role="list"` + `role="listitem"`.
- Secciones de contenido con `aria-label` descriptivo.

### 6. Iframes accesibles
- Añadido `title` y `aria-label` descriptivos al iframe de Canva y al mapa de Google Maps.
- Los iframes sin título son invisibles para lectores de pantalla.

### 7. Elementos multimedia
- `<video>` y `<audio>`: añadido `aria-label` descriptivo. Fallback con enlace de descarga cuando el navegador no soporta el formato.
- Los iconos decorativos de Bootstrap Icons tienen `aria-hidden="true"`.

### 8. Links externos
- Todos los enlaces que abren en `_blank` tienen `rel="noopener noreferrer"` (seguridad) y un `<span class="visually-hidden">(abre en nueva pestaña)</span>` para avisar a usuarios de lector de pantalla.

### 9. Headings jerárquicos
- **Antes:** en las páginas de servicio, `<h3>` se usaba para secciones principales y `<h5>` para títulos del footer.
- **Después:** jerarquía corregida. `<h1>` para el título principal de la página, `<h2>` para las secciones (formulario, garantías, footer), `<h2 class="h5">` en el footer (estilo visual de h5, semántica de h2). Los artículos de servicio usan `<article>` + `<h2>`.
- Carrusel: los títulos de las slides cambiados de `<h3>` a `<h2>` (no hay h2 previo en esa sección).

### 10. Página actual marcada en nav
- En cada página de servicio, el enlace activo en el navbar lleva `aria-current="page"`.

### 11. Dirección postal semántica
- El bloque de dirección en el footer envuelto en `<address>` en todas las páginas.

---

## ✅ Usabilidad

### 1. Títulos de página únicos y descriptivos
- **Antes:** todas las páginas tenían `<title>Repair IT - Servicio Técnico Profesional</title>`.
- **Después:**
  - `index.html` → `Repair IT - Servicio Técnico Profesional`
  - `consolas.html` → `Reparación de Consolas - Repair IT`
  - `movil.html` → `Reparación de Móviles - Repair IT`
  - `ordenadores.html` → `Reparación de Ordenadores - Repair IT`

### 2. H1 visibles en páginas de servicio
- **Antes:** el título de la página de servicio era un `<span class="btn-active">` (sin semántica de heading).
- **Después:** `<h1 class="btn-active">` para que el título sea el encabezado principal de la página.

### 3. Estructura semántica clara
- Uso de `<article>` para cada tarjeta de servicio y cada reseña.
- Uso de `<section>` con `aria-label` para agrupar contenidos relacionados.
- `<address>` para los datos de contacto del footer.

### 4. Responsive
- No se han modificado los CSS; Bootstrap 5 ya garantiza la responsividad. Se ha verificado que todos los cambios HTML son compatibles con el sistema de grids existente.

---

## ✅ Verificación y test

### Herramientas recomendadas para pasar las pruebas

| Herramienta | Qué comprueba | Cómo usarla |
|---|---|---|
| **Lighthouse** | Performance, Accessibility, Best Practices, SEO | Chrome DevTools > Lighthouse > Generate report |
| **WAVE** | Errores WCAG, contraste, formularios | Extensión WAVE o wave.webaim.org |
| **axe DevTools** | Reglas WCAG 2.1 AA | Extensión axe DevTools > Analyze |

### Checklist de navegación por teclado
- [ ] `Tab` navega por todos los elementos interactivos en orden lógico.
- [ ] El skip link aparece al primer `Tab` y funciona.
- [ ] El menú hamburguesa se abre con `Enter`/`Space`.
- [ ] El carrusel se controla con `ArrowLeft`/`ArrowRight`.
- [ ] Los puntos del carrusel son focusables y activables.
- [ ] Todos los campos del formulario son accesibles desde teclado.
- [ ] El foco siempre es visible (outline azul claro).

### Compatibilidad de navegadores
- Chrome, Firefox y Edge: compatibles. Bootstrap 5 y el JS del carrusel no usan APIs exclusivas de ningún motor.

---

## Archivos modificados

```
RepairIT.github.io-main/
├── index.html          ← MODIFICADO
├── consolas.html       ← MODIFICADO
├── movil.html          ← MODIFICADO
├── ordenadores.html    ← MODIFICADO
├── Estils_bootstrap.css        (sin cambios)
├── estils_serveis_general.css  (sin cambios)
├── terminos-condiciones.html   (sin cambios)
├── fitxer.php                  (sin cambios)
└── Imagenes/                   (sin cambios)
```
