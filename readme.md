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

### Card Types
Cards come in five layouts. The default fast path is unchanged — `+ card` instantly creates a Basic card. Click the `▾` chevron beside it to pick a different type.

- **Basic** — the classic layout: optional image, title, description
- **Newspaper** — image floats left with text wrapping around it, like a news column or Word text-wrap
- **List** — bullet list with inline editing; `Enter` adds a row, `Backspace` on an empty row removes it
- **Table** — editable header row + data rows; add/remove rows and columns in edit mode; horizontal scroll on narrow cards
- **Gallery** — 2-column image grid; each image opens in the lightbox; add or remove images individually

Right-click any card → **Change card type** to convert between types. Compatible fields (title, content) are always preserved. Images are stashed per-type and restored if you switch back — nothing is silently deleted.

### Editing
- **Double-click** any card to enter edit mode — title, description, image
- **Double-click** board header to open board settings — rename, columns, color
- Text wraps naturally, card height adapts to content
- Click outside or `Escape` to save and exit
- Image upload with fullscreen lightbox on click

### Context Menu (right-click)
- **On a card** — Edit, Move to top, Move to bottom, Duplicate, Copy, Cut, Move to board, Change card type, Delete
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
| Add list item | `Enter` (in list card) |
| Remove empty list item | `Backspace` (in list card) |
| Cancel cut / close menus | `Escape` |
| Close lightbox | `Escape` |

---

## Card Types

### Basic
The default. Image on top (optional), title, description below. Exactly like v0.1.

### Newspaper
Image floats left at 68×68px; title and body text wrap around it to the right — the same text-wrap behavior as a newspaper column or Word's "wrap text" layout. Click the image to zoom; in edit mode, click to swap or remove it.

### List
```
• item
• item
• item
```
Stored as an array of strings. `Enter` creates a new row below the current one. `Backspace` on an empty row deletes it. Rows can be individually removed with the `✕` button visible in edit mode.

### Table
```
| Col 1 | Col 2 |
|-------|-------|
|       |       |
```
Fixed simple table — no formulas, no resize. Column headers are editable. Use `+ row` / `+ col` / `- row` / `- col` buttons (visible in edit mode) to reshape. Horizontally scrollable on narrow cards.

### Gallery
A 2-column image grid. Each image is independently zoomable via lightbox. Edit mode reveals per-image delete buttons and an `+` tile to add more images. Reuses the same WebP compression pipeline as all other image types.

---

## Storage

All data is stored in `localStorage`. Images are compressed and stored as base64 WebP data URLs — fully self-contained, no external references.

**Image pipeline:**
```
File → FileReader (data URL) → Canvas resize (max 768px) → WebP (quality 0.75) → base64 → localStorage
```

**Card type data** is stored alongside title and content:
```js
// List
{ type: "list", title: "...", data: { items: ["...", "..."] } }

// Table
{ type: "table", title: "...", data: { columns: ["Col 1"], rows: [["cell"]] } }

// Gallery
{ type: "gallery", title: "...", data: { images: ["data:image/webp;base64,..."] } }
```

Old cards without a `type` field are automatically migrated to `type: "basic"` on load — no data loss.

**Limits:** ~5MB per origin. Text-only boards hold thousands of cards comfortably. With images, roughly 10–20 depending on content. Gallery cards will consume storage faster. The storage meter in Settings gives you a live read.

**Neocities CSP note:** Neocities blocks `blob:` URLs. DasBoard avoids this entirely by using `FileReader.readAsDataURL()` — no `URL.createObjectURL()` is ever called at any stage.

**Export / import:** Settings → Export JSON downloads a complete snapshot of all boards and cards including images and card type data. Import replaces current data after confirmation.

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
| Card types | Renderer map (`CARD_RENDERERS`) + editor map (`CARD_EDITORS`) |
| Fonts | IBM Plex Mono + IBM Plex Sans (Google Fonts) |
| Icons | Icons8 (iOS style) |
| Dependencies | **None** |
| Build step | **None** |
| Bundle size | One HTML file |

---

## Changelog

### v0.2.0 — 2026
- **Card type system** — five layouts: Basic, Newspaper, List, Table, Gallery
- `+ card ▾` split button — instant Basic card on left click, type picker on chevron
- Right-click → Change card type — converts between types, preserves compatible fields
- Image stashing — switching types never silently destroys images; switching back restores them
- Basic → Gallery migration seeds the gallery with the existing image
- Newspaper layout — image floats left with CSS text-wrap (no flexbox)
- List card — Enter to add, Backspace to remove, inline ✕ per row
- Table card — editable headers, add/remove rows and columns, overflow-x scroll
- Gallery card — 2-column grid, per-image delete, lightbox, WebP pipeline reuse
- Search extended to cover list items and table cells
- Duplicate/copy/paste deep-clones `data` field to prevent reference sharing
- Automatic migration: old cards without `type` get `type: "basic"` on load

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
- [x] Card types — Basic, Newspaper, List, Table, Gallery
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