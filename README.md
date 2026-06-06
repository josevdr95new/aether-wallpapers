# Aether Wallpapers

Repositorio **oficial** de fondos animados HTML/CSS/JS para la app **Aether**. Se publica vía **GitHub Pages** y la app lo consume como catálogo remoto **fijo** (la URL es `https://josevdr95new.github.io/aether-wallpapers/index.json` y no se puede cambiar desde la UI).

Official animated HTML/CSS/JS wallpapers repository for the **Aether** app. Published via **GitHub Pages** and consumed by the app as a **fixed** remote catalog (URL is `https://josevdr95new.github.io/aether-wallpapers/index.json` and cannot be changed from the UI).

---

## Español

### ¿Qué es esto?

Catálogo comunitario de wallpapers. La app Aether descarga `index.json` desde este repo público y muestra los wallpapers en una galería con filtros por **categoría**, **autor** y **fecha**, además de ordenación (recientes / antiguos / A-Z / autor).

> **URL fija en la app**: a partir de la versión actual, la URL del repositorio está **bloqueada** en el código. El usuario **no puede** cambiarla desde la interfaz. Si quieres proponer un wallpaper, envíalo como **Pull Request** a este repo.

### Estructura del repositorio

```
aether-wallpapers/
├── README.md            ← este archivo
├── index.json           ← catálogo (obligatorio)
├── <id>.html            ← wallpapers como archivos HTML sueltos
└── ...
```

### Esquema `index.json`

```json
{
  "version": 1,
  "wallpapers": [
    {
      "id": "mi-wallpaper",
      "name": "Mi wallpaper",
      "author": "tu-usuario",
      "category": "Abstracto",
      "date": "2026-06-05",
      "description": "Descripción corta, máximo 2 frases.",
      "file": "mi-wallpaper.html",
      "color": "#5eb3ff"
    }
  ]
}
```

**Campos:**

| Campo | Tipo | Descripción |
|---|---|---|
| `id` | string | Slug único (sin espacios). Se usa como nombre de caché local. |
| `name` | string | Nombre a mostrar en la galería. |
| `author` | string | Tu nombre/handle. Filtrable en la app. |
| `category` | string | Categoría libre. Se agrupan automáticamente en chips. |
| `date` | string | Fecha en formato `YYYY-MM-DD`. Para ordenar por "Recientes". |
| `description` | string | Descripción corta. Visible en el popup de metadatos. |
| `file` | string | Nombre del archivo HTML en este repo. |
| `color` | string | Color HEX (`#rrggbb`) para la banda de la tarjeta. |

### Cómo añadir un wallpaper

1. **Haz fork** de este repositorio.

2. **Crea un HTML self-contained**. Un solo archivo, sin assets externos locales. Puedes usar `<canvas>`, CSS animations, WebGL, SVG, `<video>` embebido, etc. La ventana ocupa toda la pantalla.

3. **Test local**: clona tu fork y sirve los archivos:
   ```bash
   python -m http.server 8000
   ```
   Abre `http://localhost:8000/<tu-id>.html` en el navegador para verificar que el wallpaper funciona.

4. **Añade una entrada a `index.json`** con todos los campos rellenados.

5. **Abre un Pull Request** hacia este repo. Tras el merge, GitHub Pages publicará automáticamente y todos los usuarios de Aether verán tu wallpaper.

> **Nota para desarrolladores**: si quieres probar tu fork desde la app Aether, puedes editar `constants.py` → `DEFAULT_REPO_URL` y recompilar. Los usuarios finales no tienen esta opción.

### Reglas

- **Self-contained**: un solo archivo HTML. Sin `<img src="...">` locales, sin CSS externo local. CDN vía HTTPS está permitido (Three.js, GSAP, etc.).
- **Sin interacción de ratón**: el wallpaper está **detrás de los iconos del escritorio** y **no** recibe eventos de mouse/teclado. Solo animaciones automáticas.
- **Ligero**: apunta a <20 KB sin comprimir.
- **Fullscreen**: usa `100vw` / `100vh` (o `position:fixed; inset:0`). El wallpaper se renderiza a pantalla completa.
- **No autoplay de audio**: los wallpapers son silenciosos.

### Convenciones recomendadas

- **`id`** en minúsculas, palabras separadas con guiones (`aurora-borealis`).
- **`category`** intenta reutilizar existentes (`Abstracto`, `Naturaleza`, `Espacio`, `Retro`, `Utility`, `Ciudad`, `Animación`) antes de crear nuevos.
- **`color`** representativo del wallpaper, HEX sin alpha.
- **`date`** formato ISO `YYYY-MM-DD`.

### Contribuir (resumen)

1. **Fork** del repositorio.
2. Rama: `git checkout -b feat/mi-wallpaper`.
3. Añade tu `<id>.html` y la entrada en `index.json`.
4. Verifica el JSON: `python -m json.tool index.json`.
5. Verifica que tu HTML abre sin errores en un navegador.
6. Abre un **Pull Request**.

---

## English

### What is this?

Community wallpaper catalog. The Aether app fetches `index.json` from this repo's public URL and shows the wallpapers in a gallery with filters by **category**, **author** and **date**, plus sort options (recent / oldest / A-Z / author).

> **Fixed URL in the app**: starting from the current version, the repository URL is **hardcoded** in the app. The user **cannot** change it from the UI. If you want to propose a wallpaper, submit a **Pull Request** to this repo.

### Repository structure

```
aether-wallpapers/
├── README.md            ← this file
├── index.json           ← catalog (required)
├── <id>.html            ← wallpapers as standalone HTML files
└── ...
```

### `index.json` schema

```json
{
  "version": 1,
  "wallpapers": [
    {
      "id": "my-wallpaper",
      "name": "My wallpaper",
      "author": "your-handle",
      "category": "Abstract",
      "date": "2026-06-05",
      "description": "Short description, max 2 sentences.",
      "file": "my-wallpaper.html",
      "color": "#5eb3ff"
    }
  ]
}
```

**Fields:**

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique slug (no spaces). Used as local cache filename. |
| `name` | string | Display name in the gallery. |
| `author` | string | Your name/handle. Filterable in the app. |
| `category` | string | Free-form category. Auto-grouped into chips. |
| `date` | string | Date in `YYYY-MM-DD` format. Used for "Recent" sorting. |
| `description` | string | Short description. Shown in the metadata popup. |
| `file` | string | HTML filename in this repo. |
| `color` | string | HEX color (`#rrggbb`) for the card's accent band. |

### How to add a wallpaper

1. **Fork** this repository.

2. **Create a self-contained HTML file**. Single file, no external local assets. You can use `<canvas>`, CSS animations, WebGL, SVG, embedded `<video>`, etc. The window is full-screen.

3. **Test locally**: clone your fork and serve the files:
   ```bash
   python -m http.server 8000
   ```
   Open `http://localhost:8000/<your-id>.html` in the browser to verify the wallpaper works.

4. **Add an entry to `index.json`** with all fields filled in.

5. **Open a Pull Request** to this repo. After merge, GitHub Pages will publish automatically and all Aether users will see your wallpaper.

> **Developer note**: to test your fork from within the Aether app, edit `constants.py` → `DEFAULT_REPO_URL` and rebuild. End users do not have this option.

### Rules

- **Self-contained**: single HTML file. No local `<img src="...">`, no local CSS. CDN via HTTPS is allowed (Three.js, GSAP, etc.).
- **No mouse interaction**: the wallpaper sits **behind the desktop icons** and does **not** receive mouse/keyboard events. Auto-playing animations only.
- **Lightweight**: aim for <20 KB uncompressed.
- **Fullscreen**: use `100vw` / `100vh` (or `position:fixed; inset:0`).
- **No audio autoplay**: wallpapers are silent.

### Recommended conventions

- **`id`** lowercase, dash-separated words (`aurora-borealis`).
- **`category`** reuse existing ones when possible (`Abstract`, `Nature`, `Space`, `Retro`, `Utility`, `City`, `Animation`).
- **`color`** representative of the wallpaper, HEX without alpha.
- **`date`** ISO format `YYYY-MM-DD`.

### Contributing (summary)

1. **Fork** the repository.
2. Create a branch: `git checkout -b feat/my-wallpaper`.
3. Add your `<id>.html` and the entry in `index.json`.
4. Verify JSON is valid: `python -m json.tool index.json`.
5. Verify your HTML opens in a browser without errors.
6. Open a **Pull Request**.
