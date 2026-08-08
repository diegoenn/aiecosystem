# CLAUDE.md

Guía para Claude Code (u otro agente) al trabajar en este repositorio.

## Propósito del proyecto

Este proyecto es un sitio centralizado de información y ayuda para tener acceso fácil al ecosistema moderno de SDLC (Software Development Life Cycle): un mapa de referencia con todas las herramientas necesarias para desarrollar software de manera profesional, incluyendo las herramientas de IA que hoy se integran a lo largo de todo el ciclo (planeación, diseño, desarrollo, testing, despliegue, monitoreo, etc.).

Es un proyecto personal de Diego Enn, pensado para crecer de forma incremental: nuevas etapas del SDLC, nuevas herramientas/modelos de IA y nuevos tutoriales prácticos se agregan con el tiempo, no de una sola vez.

## Stack

Sitio estático, sin framework ni build step: HTML, CSS y JS planos.

```
.
├── index.html                       Landing page
├── about.html                       Sobre mí
├── sdlc.html                        Mapa de las 10 etapas del SDLC con IA integrada
│                                     (incluye la franja "customer journey" con anclas por etapa)
├── tools.html                       Catálogo de AI Tools & Models
├── tutorials.html                   Índice de tutoriales
├── tutorials/
│   ├── git-github.html              Tutorial: Git & GitHub
│   └── claude-code-glosario.html    Tutorial: Glosario de Claude Code
└── assets/
    ├── css/style.css                Sistema de diseño compartido (design system v2)
    └── js/main.js                   Menú móvil, scroll-spy, interacciones
```

No hay `package.json`, gestor de paquetes ni pipeline de build. Cualquier cambio se ve reflejado abriendo los `.html` directamente o sirviéndolos con un servidor estático.

## Desarrollo local

```bash
python3 -m http.server 8080
# abrir http://localhost:8080
```

Para QA visual (responsive, estados hover/scroll-spy, menú móvil), usar Playwright con el Chromium ya instalado en el entorno en vez de intentar descargar uno nuevo.

## Sistema de diseño

Definido en `assets/css/style.css` (tokens en `:root`):

- **Colores**: `--bg`, `--navy`, `--amber` / `--amber-deep`, `--coral`, `--violet`, `--teal`, `--slateblue`, cada uno con su variante `-bg` para fondos suaves.
- **Tipografía**: Sora para títulos/display, Manrope para cuerpo de texto, JetBrains Mono solo para código. Se usan stacks de fuentes del sistema como fallback (importante si el contenido se reutiliza en un Artifact, donde `@import` de Google Fonts no funciona por CSP).
- **Componentes reutilizables**: `.hero` / `.hero-sm`, botones pill (`.btn-primary`, `.btn-secondary`), `.tag` por categoría (`ai`, `dev`, `qa`, `pm`, `infra`, `design`), `.tut-card` / `.soon-card` para tarjetas de tutoriales, `.ref-table` y `.callout` (`.good` / `.warn`) para contenido de tutoriales, `.journey-*` para la franja tipo customer journey de `sdlc.html`.

Al agregar contenido nuevo, reutilizar estas clases en vez de crear estilos ad-hoc; si hace falta un color nuevo, agregarlo como token en `:root` siguiendo el mismo patrón `--nombre` / `--nombre-bg`.

## Cómo agregar contenido

- **Nueva etapa o herramienta en el mapa del SDLC** → editar el arreglo `stages` en `sdlc.html` (incluye `icon` por etapa y las herramientas agrupadas; la franja de journey y el scroll-spy se generan automáticamente a partir de ese arreglo).
- **Nueva herramienta o modelo de IA** → agregar una tarjeta en `tools.html`.
- **Nuevo tutorial** → crear un archivo en `tutorials/`, siguiendo la estructura de `tutorials/git-github.html` o `tutorials/claude-code-glosario.html` (hero + TOC con anclas + secciones numeradas `.tut-section` con `.ref-table` y `.callout` donde aplique), y agregar su tarjeta correspondiente en `tutorials.html`.

### Contenido de terceros

Si una fuente (PDF, curso, artículo) sirve de inspiración para un tutorial, escribir el contenido con palabras y organización propias — no copiar texto, numeración de módulos, branding ni enlaces promocionales de la fuente original.

## Flujo de Git

- **Rama de trabajo**: `claude/landing-page-ai-sdlc-xbcoom`. Nunca hacer push directo a `main`.
- Todo cambio se desarrolla en esa rama, se commitea con mensajes claros y se abre un Pull Request hacia `main` para que el usuario lo revise antes de mergear.
- Merge a `main` y despliegue son pasos que el usuario pide explícitamente y por separado — no asumir que abrir el PR implica mergear ni desplegar.
- Si el PR de esa rama ya fue mergeado y hay trabajo nuevo, recrear la rama desde el último `main` (no apilar commits sobre historial ya mergeado):
  ```bash
  git fetch origin main && git checkout -B claude/landing-page-ai-sdlc-xbcoom origin/main
  ```

## Despliegue

- **GitHub Pages**: pensado para activarse sobre la rama `main` (carpeta raíz), sin pasos adicionales.
- **Vercel**: proyecto `aiecosystem` bajo el equipo `condomedia`. El deploy a producción debe incluir siempre el árbol completo del sitio (todas las páginas, `assets/css/style.css` y `assets/js/main.js`) — un deploy parcial deja el sitio roto (sin estilos o con páginas faltantes).
