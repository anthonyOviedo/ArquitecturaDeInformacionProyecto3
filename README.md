# EIF511 Project - Manejo de Datos (Nuxt)

Aplicación creada con Nuxt 4 y `@nuxt/content` para gestionar un catálogo estático de pinturas, artistas y museos. El sitio se genera de forma estática mediante la prerenderización de las rutas, lo que facilita su despliegue como sitio estático.

Puedes ver la versión desplegada en Netlify: https://museos.netlify.app/

## Requisitos

- Node.js >= 20.19.0
- npm (incluido con Node)

## Configuración inicial

```bash
npm install
```

## Comandos disponibles

- `npm run dev` – Levanta el entorno de desarrollo con recarga en caliente.
- `npm run build` – Compila la aplicación para producción.
- `npm run generate` – Genera los archivos estáticos listos para desplegar.

## Estructura básica

- `content/` – Entradas en formato Markdown para pinturas, artistas y museos.
- `pages/` – Vistas principales del sitio, incluidas las páginas índice y detalle.
- `components/` – Componentes reutilizables como encabezados y pies de página.
- `public/css/main.css` – Hoja de estilos consolidada del proyecto.
- `nuxt.config.ts` – Configuración de Nuxt, incluyendo la prerenderización y recursos globales.

## Generación estática

El proyecto usa Nitro en modo `static` con rastreo de enlaces (`crawlLinks: true`), por lo que `npm run generate` produce un sitio completamente estático dentro de la carpeta `dist/`.

## Notas

- El contenido se gestiona mediante archivos Markdown en `content/`, lo que permite editar la información sin modificar el código.
- Asegúrate de mantener la hoja de estilos global (`public/css/main.css`) como la única fuente de estilos compartidos.
