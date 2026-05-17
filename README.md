# ▦ DasBoard

A lightweight, browser-native board system for organizing movable cards. No backend. No account. No build step. Just one HTML file.

> *Das* — German definite article. The board. **The** board.

**Live →** [goshintai.neocities.org/dasboard](https://goshintai.neocities.org/dasboard/)

---

## Philosophy

**Object-first.** Not productivity software. Not project management. Not note-taking.

Just boards and cards — fast, physical, yours.

- **Local-first** — everything lives in your browser. No server ever sees your data.
- **Zero dependencies** — one `index.html`, drop it anywhere.
- **Instant** — no loading screens, no save buttons, no page reloads.
- **Offline** — works with no internet after the first load (fonts aside).
- **You own your data** — stored in `localStorage`, exportable, importable, deletable.

Notion is document-first. Trello is workflow-first. DasBoard is object-first.

---

## Features

### Boards & Cards
- Create, rename, delete boards
- Create, edit, delete cards with title and description
- Drag cards between boards and reorder within boards — with live ghost placeholder showing exact drop position
- Drag boards left and right to reorder them
- Masonry column layout per board — type any number 1–8
- Custom board color per board — 8 palettes, adapts to light and dark mode
- Empty board hint when no cards present
- Drag card to trash bin to delete

### Editing
- **Double-click** any card to enter edit mode — title, description, image
- **Double-click** board header to open board settings — rename, columns, color
- Text wraps naturally, card height adapts to content
- Click outside or `Escape` to save and exit
- Image upload with fullscreen lightbox on click

### Context Menu (right-click)
- **On a card** — Edit, Move to top, Move to bottom, Duplicate, Copy, Cut, Move to board, Delete
- **On a board header** — Edit board, Paste card, Move left, Move right, Delete board
- **On empty canvas** — New board, Reset zoom
- Cut puts card in ghost state (faded + dashed border) until pasted or cancelled
- Copy and paste work across boards — no drag needed

### Infinite Canvas
- **Scroll** — zoom in/out centered on cursor
- **Shift+scroll** — pan horizontally
- **Ctrl+scroll** — pan vertically
- **Middle-mouse drag** — free pan (does not trigger card drag)
- Zoom range: 20% → 300%
- Zoom indicator bottom-right — click to reset to 100%

### Settings
- Light and dark theme with smooth transition
- Adjustable card title and description font sizes
- Storage meter — shows localStorage usage out of ~5MB
- Export all data as JSON (timestamped file)
- Import from a previous export
- About modal with changelog

### UI Details
- IBM Plex Mono + IBM Plex Sans
- Icons by [Icons8](https://icons8.com)
- Toast notifications for clipboard actions
- SEO and Open Graph meta tags for social preview

---

## Usage

### Neocities / any static host

1. Download `index.html`
2. Upload to [Neocities](https://neocities.org), GitHub Pages, or any static host
3. Open in browser — done

### Local

```bash
# No server needed — just open the file
open index.html
```

That's it. There is no step 2.

---

## Keyboard Shortcuts

| Action | Shortcut |
|---|---|
| Exit edit mode | `Escape` |
| Confirm title edit | `Enter` |
| Cancel cut / close menus | `Escape` |
| Close lightbox | `Escape` |

---

## Storage

All data is stored in `localStorage`. Images are compressed and stored as base64 WebP data URLs — fully self-contained, no external references.

**Image pipeline:**
```
File → FileReader (data URL) → Canvas resize (max 768px) → WebP (quality 0.75) → base64 → localStorage
```

**Limits:** ~5MB per origin. Text-only boards hold thousands of cards comfortably. With images, roughly 10–20 depending on content. The storage meter in Settings gives you a live read.

**Neocities CSP note:** Neocities blocks `blob:` URLs. DasBoard avoids this entirely by using `FileReader.readAsDataURL()` — no `URL.createObjectURL()` is ever called at any stage.

**Export / import:** Settings → Export JSON downloads a complete snapshot of all boards and cards including images. Import replaces current data after confirmation.

---

## Stack

| Concern | Solution |
|---|---|
| Language | Vanilla JS (ES2020) |
| Styling | Plain CSS with custom properties |
| Storage | `localStorage` |
| Images | `FileReader` + `Canvas` + `toDataURL` |
| Drag | Custom mouse event system |
| Canvas | CSS `transform: translate + scale` |
| Fonts | IBM Plex Mono + IBM Plex Sans (Google Fonts) |
| Icons | Icons8 (iOS style) |
| Dependencies | **None** |
| Build step | **None** |
| Bundle size | One HTML file |

---

## Changelog

### v0.1.0 — 2026, initial release
- Boards & cards with drag-and-drop
- Infinite canvas — pan & zoom
- Double-click to edit cards & boards
- Image upload with WebP compression
- Masonry columns per board (1–8)
- Custom board colors, light & dark mode
- Context menu — cut, copy, paste, duplicate
- Move to board, move to top/bottom
- Image lightbox, drag-to-trash
- Export & import as JSON
- Storage meter, font size settings
- No account. No server. No tracking.

---

## Roadmap

- [x] Boards & cards
- [x] Drag and drop with ghost placeholder
- [x] Reorder boards
- [x] Masonry column layout
- [x] Custom board colors
- [x] Infinite canvas (pan + zoom)
- [x] Double-click to edit
- [x] Context menu with full clipboard model
- [x] Image upload + lightbox
- [x] Dark mode
- [x] Export / import JSON
- [x] Storage meter
- [x] Live search
- [ ] PWA — install to homescreen, full offline
- [ ] Keyboard shortcuts (N, B, /)
- [ ] Markdown in card descriptions
- [ ] Card color labels
- [ ] Pinned cards
- [ ] Undo / redo
- [ ] Tags and filters
- [ ] Multi-select drag

---

## Browser Support

Any modern browser — Chrome, Firefox, Safari, Edge.

`localStorage` must be enabled. Private/incognito mode may clear data on session end depending on browser settings.

---

## License

Do whatever you want with it. It's one HTML file.

---

*Built for the web the way the web used to feel — fast, local, yours.*
