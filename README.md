# Paper_cave

**A private, in-browser utility suite.** Every tool runs entirely on your device — no uploads, no servers, no accounts. Your files never leave your browser.

> 🔒 **100% client-side.** All processing happens in your browser's memory using the Web Speech API, Web Audio, Canvas, `pdf-lib`, `pdf.js` and `JSZip`.

---

## ✨ Tools

| Tool | What it does |
| --- | --- |
| 🎙️ **Voice Transcriber** | Live speech-to-text dictation with 12 languages, live word/char counts, copy & save as `.txt`. |
| ✂️ **Media Trimmer** | Trim audio & video with an interactive dual-handle timeline, playhead scrubbing and range preview. |
| 📄 **PDF Tools** | 11 client-side PDF utilities (see below). |
| 🖼️ **Image Compressor** | Compress & convert PNG / JPG / WebP with quality, format and dimension controls. |

### 📄 The 11 PDF tools

1. **Merge PDF** — combine multiple PDFs with drag-to-reorder.
2. **Split PDF** — extract page ranges, or split into multiple files (ZIP).
3. **Organise pages** — live thumbnails, rotate ±90°, delete, drag-to-reorder.
4. **Page numbers** — 6 positions, 3 formats, start-at, font size, margin, skip first page.
5. **Watermark** — diagonal / tiled / horizontal, 4 colours, size & opacity.
6. **Compress PDF** — page rasterisation with resolution + quality controls and a before/after size report.
7. **PDF → JPG** — export pages as JPG/PNG, with resolution, page range and ZIP download.
8. **JPG → PDF** — build a PDF from images (A4 / Letter / fit, auto-orientation, contain/cover, margin).
9. **Extract images** — pull embedded images out of a PDF (falls back to full-page renders).
10. **Protect PDF** — AES encryption with granular print / copy / modify / annotate permissions.
11. **Unlock PDF** — remove owner restrictions and verify the output is readable.

---

## 📈 Analytics & Ads

### Vercel Web Analytics

Added with the **framework-agnostic** approach, which is the correct one for a plain static HTML page:

```html
<script>
  window.va = window.va || function () { (window.vaq = window.vaq || []).push(arguments); };
</script>
<script defer src="/_vercel/insights/script.js"></script>
```

The Next.js import (`import { Analytics } from "@vercel/analytics/next"`) does **not** work in a static HTML file.

> **To start collecting data:** deploy on Vercel, then open the project in the Vercel dashboard and enable **Web Analytics**. Vercel then serves `/_vercel/insights/script.js` automatically. Off Vercel that path simply 404s, which is harmless.

### Adsterra

Two ad units sit in labelled, non-intrusive slots:

| Slot | Placement | Unit |
| --- | --- | --- |
| A | Below the header | 468×60 iframe banner |
| B | After the tool content | Native banner container |

Layout safety: each slot reserves its own space and is **hidden until it actually contains an ad**, so a blocked or unsold slot never leaves a blank hole in the page. The fixed-width 468×60 banner is also scaled down in place on narrow screens instead of overflowing the layout.

---

## 🚀 Deploy on Vercel (no build step)

This is a **static single-page site** — `index.html` at the repo root is the whole app. There is nothing to build.

### Option A — Import from GitHub (recommended)

1. Go to **[vercel.com/new](https://vercel.com/new)**.
2. Click **Import Git Repository** and pick **`AbhiSunday55/paper-cave`**.
3. Vercel auto-detects it as a static site. Leave everything at the defaults:
   - **Framework Preset:** `Other`
   - **Build Command:** *(empty)*
   - **Output Directory:** *(empty / `.`)*
   - **Install Command:** *(empty)*
4. Click **Deploy**. Done — you get a live `*.vercel.app` URL.

### Option B — Vercel CLI

```bash
npm i -g vercel
vercel          # preview deploy
vercel --prod   # production deploy
```

---

## 🌐 GitHub Pages

A workflow at `.github/workflows/deploy-pages.yml` publishes the site to GitHub Pages on every push to `main`.

Live URL: **https://abhisunday55.github.io/paper-cave/**

---

## 🛠️ Run locally

No tooling required — just open the file:

```bash
# simplest
open index.html          # macOS
xdg-open index.html      # Linux

# or serve it (recommended, so the Web Speech API has a secure origin)
python3 -m http.server 8000
# → http://localhost:8000
```

> **Note:** the Voice Transcriber needs a **secure context** (`https://` or `localhost`) and microphone permission. It works in Chrome, Edge and Brave; Firefox and Safari have limited/no Web Speech support.

---

## 🧱 Tech

- **Zero dependencies to install** — everything is loaded from CDNs at runtime.
- [`pdf-lib`](https://pdf-lib.js.org/) — PDF creation & editing
- [`pdf.js`](https://mozilla.github.io/pdf.js/) — PDF rendering & thumbnails
- [`JSZip`](https://stuk.github.io/jszip/) — ZIP packaging
- [Tailwind CSS](https://tailwindcss.com/) (Play CDN) — styling
- [Font Awesome](https://fontawesome.com/) — icons
- Web Speech API · Web Audio API · Canvas · MediaRecorder

---

## 📁 Project structure

```
paper-cave/
├── index.html                          # the entire app (single page)
├── vercel.json                         # Vercel static-site config
├── .nojekyll                           # tells GitHub Pages to skip Jekyll
├── .github/workflows/deploy-pages.yml  # GitHub Pages deploy workflow
└── README.md
```

---

## 🔐 Privacy

Paper_cave has **no backend of its own** — your files are never uploaded. Everything you drop in is processed locally in browser memory and discarded when you close the tab.

Two third-party services do load alongside the page, and **neither ever receives your files**:

| Service | What it receives | Notes |
| --- | --- | --- |
| **Vercel Web Analytics** | Aggregate page views (URL, referrer, country, device) | Cookieless and privacy-focused; active only when the site is hosted on Vercel. |
| **Adsterra** | Ad impressions and clicks through its own scripts and iframes | A third-party ad network that may set its own cookies. Ads appear only in the clearly-labelled slots. |

**Your documents, audio, images and transcripts are never part of that traffic.**
