# Artemis · Web de poesía

Una página web pensada como un poema en sí misma. Estética de cristal líquido sobre fondo negro, tipografía Instrument Serif, navegación por migas de pan y buscador integrado para recorrer toda la obra de Artemis.

## Estructura

```
.
├── index.html          # única página (SPA con router por hash)
├── media/
│   ├── avatar.mp4      # vídeo del hero
│   ├── featured.mp4    # vídeo de la sección destacada
│   ├── philosophy.mp4  # vídeo de la sección Cuerpo × Verso
│   ├── card-1.mp4      # vídeo del poemario "La mujer que no se calla"
│   └── card-2.mp4      # vídeo del poemario "El silencio fértil"
├── .nojekyll           # evita que GitHub Pages procese con Jekyll
└── README.md
```

Todo el contenido (poemas, biografía, descripciones) está dentro de `index.html`. Los datos de los poemarios viven en el array `POEMARIOS` al inicio del `<script>` — fácil de editar sin tocar el resto del código.

## Rutas (SPA con hash routing)

| URL | Vista |
|---|---|
| `#/` | Inicio (hero + sobre + featured + cuerpo×verso + poemarios) |
| `#/poemarios` | Índice completo de los tres libros |
| `#/poemarios/{id}` | Ficha del libro + lista de poemas |
| `#/poemarios/{id}/{poema-id}` | Poema individual centrado |

Las migas de pan (`Inicio › Poemarios › El libro › Poema`) se actualizan solas en cada vista. Cada segmento es clickable.

## Buscador

- Lupa en la nav, **`Cmd+K`** / **`Ctrl+K`**, o tecla **`/`** abre el modal
- Indexa títulos, descripciones y versos completos
- Resaltado de coincidencias con `<mark>`
- **`Esc`** cierra

## Deploy en GitHub Pages

1. Crea un repositorio nuevo en GitHub (público o privado con plan).
2. Sube todos estos archivos a la raíz del repositorio:
   ```bash
   git init
   git add .
   git commit -m "Web de Artemis"
   git branch -M main
   git remote add origin git@github.com:TU-USUARIO/TU-REPO.git
   git push -u origin main
   ```
3. En GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root)**.
4. Espera 1-2 minutos. La web estará en `https://TU-USUARIO.github.io/TU-REPO/`.

> No hace falta build ni dependencias. Es HTML/CSS/JS plano. El archivo `.nojekyll` evita que GitHub procese subdirectorios que empiezan por `_`.

### Dominio propio (opcional)

En **Settings → Pages → Custom domain** pones tu dominio y creas un registro `CNAME` apuntando a `TU-USUARIO.github.io` en tu DNS.

## Probar en local

Cualquier servidor estático sirve. El más rápido:

```bash
cd Artemis2
python3 -m http.server 4321
# abre http://localhost:4321
```

> Abrir `index.html` con doble clic **NO funciona** porque el navegador bloquea los `fetch`/`<source>` con protocolo `file://`. Hay que servirlo por HTTP.

## Personalizar

- **Cambiar el nombre de la poeta**: busca y sustituye `Artemis` en `index.html` y en el `<title>`.
- **Editar poemas**: modifica el array `POEMARIOS` en el script. Las cursivas dentro de los versos se marcan con `_palabra_`.
- **Añadir un libro nuevo**: copia el último objeto del array y cambia `id`, `title`, `year`, `tag`, `desc`, `epigraph`, `video` y la lista de `poems`.
- **Cambiar vídeos**: sustituye los archivos en `media/` manteniendo los nombres, o cambia las rutas en el HTML.

## Tecnologías

- HTML/CSS/JS vanilla, sin build, sin dependencias npm
- Google Fonts: **Instrument Serif** + **JetBrains Mono**
- Cristal líquido CSS: `backdrop-filter: blur(4px)` + bordes con gradiente enmascarado
- Cursor personalizado, fade del hero, parallax sutil, IntersectionObserver para revelar al scroll
- Hash routing (sin React, sin Vue)
- Buscador client-side sobre los datos en memoria
- Respeta `prefers-reduced-motion`

## Licencia

Todos los versos pertenecen a Artemis. El código del sitio: tuyo, haz lo que quieras.
