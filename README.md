# AI Ecosystem · SDLC

Un sitio estático que documenta, de forma incremental, cómo la inteligencia artificial se integra en cada etapa del ciclo de vida de desarrollo de software (SDLC): herramientas, modelos y tutoriales prácticos.

No usa framework ni build step — es HTML, CSS y JS planos, pensado para crecer con el tiempo y desplegarse fácilmente en GitHub Pages.

## Estructura

```
.
├── index.html              Landing page
├── about.html               Sobre mí
├── sdlc.html                 Mapa de las 10 etapas del SDLC con IA integrada
├── tools.html                 Catálogo de AI Tools & Models
├── tutorials.html             Índice de tutoriales
├── tutorials/
│   └── git-github.html        Tutorial: Git & GitHub — guía de referencia diaria
└── assets/
    ├── css/style.css          Sistema de diseño compartido
    └── js/main.js              Menú móvil / interacciones de navegación
```

## Desarrollo local

No requiere instalación de dependencias. Para previsualizar el sitio:

```bash
python3 -m http.server 8080
# abrir http://localhost:8080
```

## Cómo agregar contenido

- **Nueva etapa o herramienta en el mapa del SDLC** → edita el arreglo `stages` en `sdlc.html`.
- **Nueva herramienta o modelo de IA** → agrega una tarjeta en `tools.html`.
- **Nuevo tutorial** → crea un archivo en `tutorials/`, siguiendo la estructura de `tutorials/git-github.html`, y agrega su tarjeta en `tutorials.html`.

## Despliegue

Pensado para GitHub Pages: al activarlo sobre la rama `main` (carpeta raíz), el sitio queda disponible sin pasos adicionales.
