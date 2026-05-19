# QRcode-Generator

A web-based, branded QR code generator built for the Red Hat Executive Briefing Center team. Creates QR codes for URLs, WiFi networks, email, SMS, vCards, calendar events, and bulk batches — with optional Red Hat / EBC / The Open Accelerator / custom logo embedding.

The entire app is a single static HTML file with no build step.

## Features

**Content**
- **Six content types** — URL/text, WiFi, Email, SMS, Contact (vCard 3.0), Calendar event (iCal)
- **Batch generation** — paste a URL list or upload a CSV, get back a ZIP of PNGs/SVGs (up to 500 per batch)
- **Filename templates** — tokens `{name}` `{date}` `{host}` `{slug}` `{index}` for batch output

**Branding**
- **Brand profiles** — one-click presets for *Red Hat EBC* (`#EE0000`) and *The Open Accelerator* (`#FFC600`)
- **Saved custom profiles** — name, save, rename, reorder, and delete your own logo + color combinations (persisted in `localStorage`)
- **Profile export / import** — round-trip profiles as JSON for sharing across machines or teammates
- **Logo embedding** — preset logos for Red Hat, EBC, and TOA (plus reverse variants), or upload your own (PNG / JPG / SVG / WebP up to 2 MB)
- **Drag-and-drop logo** — drop an image file directly on the card to set it as the logo
- **URL auto-suggestion** — paste a `redhat.com` or `openaccelerator` URL and the matching logo is offered
- **Brand color swatches** — Red Hat (4) and TOA (9) brand-safe color presets alongside a freeform picker

**Output**
- **Three export formats** — PNG (raster), SVG (vector), and clipboard copy
- **Transparent background** — toggle for codes intended to overlay on colored brand artwork
- **Two styles** — square modules or liquid (rounded modules with circular finder patterns)
- **Scan validation** — generated codes are decoded via `jsQR` and verified before display (works for transparent codes too)
- **Color scannability warning** — WCAG-luminance check warns before you generate an unscannable code

**Quality of life**
- **Persisted last-used settings** — type, style, size, color, logo, transparent flag remembered across sessions
- **Recent generations history** — restore the exact settings of any of the last 12 generations with one click
- **Red Hat brand styling** — Red Hat Display + Red Hat Text fonts, Red Hat red accents
- **Fully accessible** — keyboard navigation, ARIA roles, focus management, live regions, reduced-motion support

## Quick start

```bash
git clone https://github.com/holzerjm/QRcode-Generator.git
cd QRcode-Generator

# Option 1: open the file directly in your browser
open index.html

# Option 2: serve over HTTP (recommended — unlocks SVG logo embedding,
# scan validation, and clipboard copy)
python3 -m http.server 8000
# then open http://localhost:8000
```

## Documentation

A user guide is included in two formats:

- [`USER_GUIDE.md`](USER_GUIDE.md) — Markdown, renders directly on GitHub
- [`user-guide.html`](user-guide.html) — Red Hat-branded HTML version with sticky TOC, scroll-spy, and print styles

Both are reachable from the **"User guide →"** link in the app's top bar.

Release history is in [`CHANGELOG.md`](CHANGELOG.md).

## Project structure

| File | Purpose |
|---|---|
| `index.html` | The QR code generator app |
| `user-guide.html` | Branded HTML user guide |
| `USER_GUIDE.md` | Markdown user guide |
| `README.md` | This file |
| `CHANGELOG.md` | Release history |
| `LICENSE` | MIT license for the source code |
| `Logo-Red_Hat-Team-Executive_Briefing_Center_Team-A-Standard-RGB.png` | Red Hat EBC team logo |
| `Logo-Red_Hat-A-RGB.Small-logo-transparent.png` | Red Hat standard logo |
| `Logo-Red_Hat-A-Reverse-RGB.Small-logo-transparent.png` | Red Hat reverse logo |
| `Logo-OpenAccelerator-A-Standard-RGB.png` | The Open Accelerator standard logo |
| `Logo-OpenAccelerator-A-Reverse-RGB.png` | The Open Accelerator reverse logo |

## Dependencies

Loaded from cdnjs at runtime — no build step required:

- [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) — QR matrix generation
- [jsQR](https://github.com/cozmo/jsQR) — post-render scan validation
- [JSZip](https://stuk.github.io/jszip/) — batch ZIP packaging

Fonts: **Red Hat Display** and **Red Hat Text** from Google Fonts.

## Deployment

To share with colleagues, copy the folder (or zip it) and host on any static web host — S3, GitHub Pages, an internal Apache/nginx, etc. No server-side code, no environment variables, no secrets.

## License

The application source code is released under the [MIT License](LICENSE).

## Trademarks

The Red Hat logo, the Red Hat fedora design, the **Red Hat Executive Briefing Center** logo, and **The Open Accelerator** logo are trademarks of Red Hat, Inc. The MIT license applied to the source code does **not** grant any rights to these trademarks or logo files. If you fork or reuse this project outside of Red Hat, replace the bundled logo PNG files with your own assets.
