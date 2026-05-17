# ▦ DasBoard

I made this because I wanted a simple board tool that doesn't require an account, doesn't phone home, and doesn't make me install Node just to look at a sticky note. Vibecoded with Claude. Hosted on Neocities because that's still a thing and I love it.

**Live →** [goshintai.neocities.org/dasboard](https://goshintai.neocities.org/dasboard/)

---

## What it is

Boards and cards. That's it. You can drag them around, put images on them, zoom out to see everything at once, zoom in to read stuff. It lives entirely in your browser — no server, no account, no tracking. Close the tab and your data is still there next time.

It's not Notion. It's not Trello. Those are great but they're also a lot. This is just the boards-and-cards part.

---

## What it does

**Boards**
- Create, rename, delete
- Set how many columns of cards you want (1 to 8)
- Pick a color — different palettes for light and dark mode
- Drag to reorder
- Double-click the header to edit settings

**Cards**
- Title and description, both auto-resize to content
- Attach an image — it gets compressed and stored locally
- Click the image to open it fullscreen
- Double-click to edit, click outside to save
- Drag between boards, drag to reorder within a board
- Ghost placeholder shows exactly where the card will land

**Right-click menu**
- On a card: edit, move to top/bottom, duplicate, copy, cut, move to another board, delete
- On a board: edit, paste, move left/right, delete
- On empty canvas: new board, reset zoom
- Cut leaves a ghost card in place until you paste it somewhere

**Canvas**
- Scroll to zoom (centered on cursor)
- Shift+scroll to pan sideways
- Ctrl+scroll to pan up/down
- Middle-mouse drag to pan freely
- 20% to 300% zoom range

**Settings**
- Dark/light mode
- Card font size controls
- Storage meter (localStorage, ~5MB limit)
- Export everything as JSON, import it back

---

## Using it

Download `index.html`. Open it. Done. No npm, no build step, no nothing.

If you want it online, upload it to Neocities or GitHub Pages or literally any static host. It's one file.

---

## Storage

Everything goes into `localStorage` — boards, cards, images. Images are resized to max 768px, compressed to WebP at 0.75 quality, and stored as base64 strings. That's why the storage limit exists (~5MB per origin). The meter in Settings shows you how much you've used.

Export your data regularly if you care about it. The browser can wipe localStorage if you clear your cache. You've been warned, I've been warned, we've all been warned.

**Neocities CSP:** Neocities blocks `blob:` URLs so all image handling goes through `FileReader.readAsDataURL()` instead — no blob URLs ever created.

---

## Stack

Vanilla JS. Plain CSS. No frameworks, no bundler, no package.json. `localStorage` for persistence. Custom mouse event system for drag. CSS `transform` for the infinite canvas. Icons from [Icons8](https://icons8.com). Fonts from Google Fonts (IBM Plex Mono + IBM Plex Sans).

One file. Currently ~2500 lines. Readable by a human.

---

## Changelog

**v0.1.0 — 2026**
First release. Boards, cards, drag and drop, infinite canvas, double-click editing, masonry columns, board colors, context menu with clipboard, image upload and lightbox, export/import, storage meter, dark mode.

**Coming next**
PWA support — install to homescreen, works fully offline after first load.

---

## Roadmap

- [x] Boards & cards
- [x] Drag and drop with ghost placeholder
- [x] Reorder boards
- [x] Masonry column layout
- [x] Custom board colors
- [x] Infinite canvas (pan + zoom)
- [x] Double-click to edit
- [x] Context menu with clipboard (cut/copy/paste)
- [x] Image upload + lightbox
- [x] Dark mode
- [x] Export / import JSON
- [x] Storage meter
- [x] Live search
- [ ] PWA — install to homescreen, full offline
- [ ] Keyboard shortcuts
- [ ] Markdown in descriptions
- [ ] Card color labels
- [ ] Undo / redo
- [ ] Tags and filters

---

## License

Do whatever you want.
