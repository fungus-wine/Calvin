# Calvin Documentation Website – CLAUDE.md

## Project Overview
Static multi-page documentation site for the Calvin self-balancing robot project.
Hosted on GitHub Pages. No build step required.

## Tech Stack
- **HTML5** – plain, human-editable HTML files
- **Tailwind CSS** – loaded via CDN play script (no npm, no PostCSS, no build)
- **custom.css** – minimal hand-written overrides in `assets/css/custom.css`

## Tailwind CDN Approach
Every page includes this in `<head>`:
```html
<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="assets/css/custom.css">
```
The CDN script compiles Tailwind on the fly in the browser. This means:
- No `tailwind.config.js` needed
- No build commands
- Works with `file://` locally and GitHub Pages without any CI

## File Structure
```
calvin/
├── CLAUDE.md
├── .gitignore
├── .claudeignore
├── index.html          ← Home / hero
├── hardware.html       ← Hardware deep-dive
├── software.html       ← Software architecture
├── gallery.html        ← Photos + YouTube embeds
├── build-log.html      ← Chronological build log
└── assets/
    ├── images/         ← Local photos (ignored by Claude)
    └── css/
        └── custom.css
```

## Related GitHub Repositories
| Repo | Description |
|------|-------------|
| `github.com/fungus-wine/calvin_instinctus` | Arduino GIGA R1 real-time balance firmware |
| `github.com/fungus-wine/calvin_cogitator` | Jetson Orin Nano AI / vision / LLM layer |
| `github.com/fungus-wine/calvin_explorator` | Electron + Vue 3 desktop monitoring app |
| `github.com/fungus-wine/librarius` | Shared Arduino library (InstinctusKit) |

## Navigation Pattern
Each page contains the full `<nav>` block copied verbatim. The current page's link
gets the `.nav-active` class (defined in `custom.css`) added to its `<a>` tag.

Example – on `hardware.html`, the Hardware link should be:
```html
<a href="hardware.html" class="nav-active">Hardware</a>
```
All other links are plain:
```html
<a href="index.html" class="hover:text-orange-400 transition-colors">Home</a>
```

## How to Add a Gallery Image
1. Drop the image into `assets/images/`
2. Open `gallery.html`
3. Copy an existing `<figure>` block in the grid and update:
   - `src="assets/images/YOUR_PHOTO.jpg"`
   - `alt="..."` description
   - `<figcaption>` text

## How to Add a YouTube Embed
In `gallery.html`, find the `<!-- YouTube Embeds -->` section and copy an existing
`<div class="aspect-video ...">` block. Replace the `src` URL:
```html
<iframe src="https://www.youtube.com/embed/VIDEO_ID" ...></iframe>
```

## How to Add a Build Log Entry
In `build-log.html`, entries are newest-first. Copy the topmost `<article>` block
and paste it above the others. Update:
- `<h2>` date heading
- `<p>` description text
- Optionally add an `<img>` element inside the article

## GitHub Pages Deployment
Push the `main` branch to GitHub. In repo Settings → Pages, set source to
**main branch / root**. The site will be available at:
`https://fungus-wine.github.io/<repo-name>/`

No build action required — GitHub Pages serves static HTML directly.

## Local Development
```bash
python3 -m http.server 8080
# then open http://localhost:8080
```
Or just open any `.html` file directly in a browser (`file://` path).
