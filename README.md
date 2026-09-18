# Dath Reader

A fast, glass-styled PDF viewer that runs entirely in the browser — no backend, no upload, nothing leaves the visitor's device. Built as a single static `index.html`, so it deploys to GitHub Pages with zero build step.

**Live demo (after you deploy):** `https://<your-username>.github.io/<repo-name>/`

![theme](https://img.shields.io/badge/theme-red%20glass-c81730) ![deps](https://img.shields.io/badge/build%20step-none-3fbf6f)

## Features

- **True PDF rendering** via [pdf.js](https://mozilla.github.io/pdf.js/) — sharp at any zoom, real selectable/searchable text (not an image)
- **Zoom & fit** — fit width, fit page, manual zoom, keyboard shortcuts
- **Continuous scroll** with lazy rendering (only renders pages near the viewport, so large PDFs stay smooth)
- **Thumbnail sidebar** for quick navigation
- **In-document search** with match highlighting and next/previous navigation
- **Rotate**, **print**, and **download** the original file
- **Annotation tools** — pen, highlighter, sticky notes, eraser (kept in-session, drawn as an overlay — see [Limitations](#limitations))
- **Drag-and-drop** to open a file, or the Open button / `Ctrl+O`
- **Red glassmorphism UI** with light/dark variants that follow the visitor's system theme
- Fully responsive, keyboard accessible, works offline once loaded (except for the CDN-hosted pdf.js library and Google Fonts)

## Deploying to GitHub Pages

1. Create a new repository on GitHub (or use an existing one).
2. Add these two files to the repository root:
   - `index.html`
   - `README.md` (this file — optional but recommended)
3. Commit and push:
   ```bash
   git init
   git add index.html README.md
   git commit -m "Add Dath Reader"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
4. On GitHub, open your repo → **Settings** → **Pages**.
5. Under **Build and deployment → Source**, choose **Deploy from a branch**.
6. Under **Branch**, choose `main` and folder `/ (root)`, then **Save**.
7. GitHub will publish the site within a minute or two at:
   ```
   https://<your-username>.github.io/<repo-name>/
   ```
   (If the repo is named `<your-username>.github.io`, the site is served at the root of that URL instead.)

No build tools, no `npm install`, no config file needed — it's a single HTML file that GitHub Pages serves as-is.

## Running locally

Just open `index.html` in a browser, or serve the folder so relative behavior matches production:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Project structure

```
.
├── index.html   # the entire app — markup, styles, and logic
└── README.md
```

Everything is intentionally kept in one file so the project stays copy-paste-deployable with no bundler.

## Customizing

- **App name / branding:** search `index.html` for `Dath Reader` and `dath` — both the toolbar wordmark and the About panel.
- **Color theme:** the red palette is defined as CSS custom properties at the top of the `<style>` block (`--red-500`, `--red-600`, `--red-700`, `--gold-400`, etc.) — change these to retheme the whole app.
- **Logo:** the logo is inline SVG (search for `logoGrad`) so it can be edited directly without an image asset.
- **pdf.js version:** pinned to `3.11.174` via cdnjs in the `<head>` and in the worker `src` inside the script — update both together if you upgrade.

## Limitations

- Annotations (pen, highlighter, sticky notes) are **view-time only**: they live in the page's memory for the current session and are **not saved back into the PDF file** or persisted between visits. Treat them as an on-screen markup layer for review, not a permanent edit.
- Password-protected PDFs are not supported — the viewer will show an error toast if one is opened.
- Very large PDFs (hundreds of MB) may be slow to open since the whole file is read into memory client-side.

## Credits

Crafted by **dath**. PDF rendering powered by [pdf.js](https://mozilla.github.io/pdf.js/) (Mozilla, Apache-2.0). Fonts: [Inter](https://fonts.google.com/specimen/Inter) and [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) via Google Fonts.

## License

MIT — do whatever you like with it.
