# Red Hat EBC QR Code Generator — User Guide

A web-based tool for creating branded QR codes for URLs, WiFi networks, email, SMS, contact cards, calendar events, and bulk batches. Built for the Red Hat Executive Briefing Center team.

---

## Contents

1. [Getting started](#1-getting-started)
2. [Quick start: Brand profiles](#2-quick-start-brand-profiles)
3. [Single QR code generation](#3-single-qr-code-generation)
4. [Logo selection](#4-logo-selection)
5. [Appearance: style, border, size, color](#5-appearance-style-border-size-color)
6. [Output, downloads, and validation](#6-output-downloads-and-validation)
7. [Batch generation](#7-batch-generation)
8. [Keyboard and accessibility](#8-keyboard-and-accessibility)
9. [Troubleshooting](#9-troubleshooting)
10. [Files in this project](#10-files-in-this-project)

---

## 1. Getting started

Open `index.html` in any modern browser (Chrome, Safari, Firefox, or Edge). All processing happens in your browser — nothing is uploaded to a server.

> **Tip:** For best results, serve the folder from a simple local web server rather than opening the file directly. This unlocks logo embedding in SVG exports, scan validation, and clipboard copy. From the project directory:
>
> ```bash
> python3 -m http.server 8000
> # then open http://localhost:8000 in your browser
> ```

The page is laid out top-to-bottom:

- **Top bar** — Red Hat EBC logo (always visible).
- **Card** — content type, brand profile, content fields, logo, appearance, and the generate button.
- **Output panel** — appears after generation with download/copy options.

---

## 2. Quick start: Brand profiles

The fastest way to create a branded QR code:

1. Pick a **Brand profile** chip at the top of the card:
   - **None** — no logo, black QR code (the default).
   - **Red Hat EBC** — applies the Red Hat EBC logo with Red Hat red (`#EE0000`).
   - **The Open Accelerator** — applies the TOA logo with TOA yellow (`#FFC600`).
2. Enter your URL in the **URL or text** field.
3. Click **Generate QR code**.

The selected chip stays highlighted in its brand color. If you later change the logo, color, or upload a custom file, the chip auto-deselects to show you've gone off-preset; click the chip again to snap back.

---

## 3. Single QR code generation

The **Single** tab (selected by default) creates one QR code at a time. Use the **QR code type** dropdown to pick what you're encoding.

| Type | What it produces | Typical use |
|---|---|---|
| URL / text | Opens a URL or shows free-form text | Websites, landing pages, plain text |
| WiFi | One-tap connection to a WiFi network | Guest WiFi cards, EBC reception posters |
| Email | Opens an email composer with optional subject and body | Contact cards, feedback links |
| SMS | Opens an SMS composer with optional message | Opt-in numbers, quick contact |
| Contact (vCard) | Adds a contact to the user's address book | Business cards, name badges |
| Calendar event | Adds an event to the user's calendar | Event posters, save-the-date materials |

### 3.1 URL / text

Enter a URL or any text in the single field. When the URL contains keywords like `redhat.com`, `ebc.redhat.com`, or `openaccelerator`, a banner appears suggesting the matching brand logo — click **Apply** to add it, or **Dismiss** to keep your current selection.

### 3.2 WiFi

Fields:
- **Network name (SSID)** — required.
- **Password** — click *Show* to reveal while typing.
- **Security** — WPA/WPA2/WPA3 covers virtually every modern network. WEP is legacy. *None* is for open networks.
- **Hidden** — check if the SSID is not broadcast.

### 3.3 Email

- **Recipient email** — required.
- **Subject** — optional; pre-fills the email subject line.
- **Body** — optional; pre-fills the email body.

The QR code uses the standard `mailto:` URL with proper encoding.

### 3.4 SMS

- **Phone number** — required. International format (`+1234567890`) gives the best scanner compatibility.
- **Message** — optional; pre-fills the SMS body.

If a message is provided, the `SMSTO:` format is used (broadest compatibility). Otherwise the standard `sms:` URL is used.

### 3.5 Contact (vCard)

Provide at least a name or organization. All other fields are optional:

- **Name** — first and last.
- **Work** — organization, title.
- **Contact** — phone, mobile, email, website.

The output is a vCard 3.0 payload that imports cleanly into iOS Contacts, Android Contacts, Outlook, and most other address books.

### 3.6 Calendar event

- **Event title** — required.
- **Starts** — required, your local timezone.
- **Ends** — optional.
- **Location**, **Description** — optional.

Times are converted to UTC and packaged as a `VCALENDAR/VEVENT` payload, compatible with Google Calendar, Apple Calendar, and Outlook.

---

## 4. Logo selection

A logo embedded in the center of the QR code reinforces your brand. The generator automatically raises error correction to the highest level (~30% recovery) whenever a logo is present, so the code remains scannable.

### Preset logos

Available from the **Logo** dropdown:

- **Red Hat EBC** — the team logo (color).
- **Red Hat** — standard Red Hat fedora + wordmark.
- **Red Hat (reverse)** — light version, intended for dark QR codes.
- **The Open Accelerator** — black wordmark version.
- **The Open Accelerator (reverse)** — light version for dark backgrounds.

### Custom upload

1. Select **Upload custom…** from the Logo dropdown.
2. Click **Choose image…** and pick a PNG, JPG, SVG, or WebP file (up to 2 MB).
3. The logo is embedded and the QR regenerates automatically.

### Auto-suggestion

When the URL/text field contains a recognized keyword (e.g. `redhat.com`, `ebc.redhat.com`, `openaccelerator`), a red-bordered banner appears suggesting the matching logo. This is purely a convenience — clicking **Dismiss** keeps your current setting.

---

## 5. Appearance: style, border, size, color

### Style

- **Square** — classic, sharp QR modules. Highest scanner compatibility.
- **Liquid** — rounded modules with circular finder patterns. More modern look; uses high error correction automatically.

### Border

Toggle a thin rounded border around the QR code. Useful for print contexts where you want a defined edge.

### Size

- **Small** — 240 px.
- **Medium** — 360 px (default).
- **Large** — 520 px.
- **Extra large** — 720 px.

For print, choose Extra large or download as SVG (resolution-independent).

### Color

Click the color swatch to pick any color for the dark modules. For best scannability:

- Use dark, high-contrast colors against a white background.
- Avoid yellows, light blues, and muted tones — scanners may fail to detect the modules.
- The Brand profile chips set scannable colors automatically (Red Hat red is the lightest tested-good color in the palette).

---

## 6. Output, downloads, and validation

After generation, the QR code appears below the card with three actions.

### Download options

- **Download PNG** — raster image with the logo baked in. Best for digital use (web pages, email signatures, screen-share decks).
- **Download SVG** — vector format with the logo embedded. Best for print at any size — scales without quality loss.
- **Copy image** — copies the PNG to your clipboard for pasting into Slack, decks, documents, etc.

Filenames include the logo key, e.g. `qrcode-ebc.png` or `qrcode-toa.svg`.

### Validation badge

Immediately under the QR code, one of three statuses appears:

| Badge | Meaning |
|---|---|
| ✓ **Verified scannable** | The generated image was decoded successfully — what you see is what scanners will read. |
| ⚠ **Could not decode** | The logo + content combination has damaged the code beyond what error correction can recover. Try a smaller logo, simpler content, or larger size. |
| ⚠ **Decoded content differs** | Rare. The decoder returned something different from your input. Regenerate; if it persists, file a bug. |

If the page is opened via `file://`, the browser may block reading the canvas and validation is silently skipped (the badge won't appear). Serving the page via `http://` resolves this.

---

## 7. Batch generation

For dozens or hundreds of QR codes at once, click the **Batch** tab.

### Source: pasted list

1. Set **Source** to *Paste list*.
2. Paste your URLs into the textarea — one per line.
3. Filenames are auto-generated from each URL's host and last path segment (e.g. `redhat.com-customer-a`).

### Source: CSV upload

1. Set **Source** to *Upload CSV*.
2. Click **Choose CSV…** and pick a `.csv` file.
3. Each row should have two columns: `filename,url`. A header row is optional.

Example:

```csv
filename,url
customer-a,https://www.redhat.com/briefings/customer-a
customer-b,https://www.redhat.com/briefings/customer-b
customer-c,https://www.redhat.com/briefings/customer-c
```

### Output format

- **PNG** — one PNG per row.
- **SVG** — one SVG per row.
- **PNG + SVG** — both for every row.

### Generating

Click **Generate ZIP** (the primary button changes label in Batch mode). A progress bar shows how many codes have been processed. When complete, a ZIP file named `qrcodes-YYYY-MM-DD.zip` downloads automatically.

The current **Logo** and **Appearance** settings apply to every code in the batch.

> **Limits:** 500 items maximum per batch. For larger jobs, split into multiple ZIPs.

---

## 8. Keyboard and accessibility

The interface is fully keyboard-navigable.

- **Tab / Shift+Tab** — move between fields.
- **Enter** — generate the QR code when focused on a single-line input.
- **Arrow Left / Arrow Right** — switch between the *Single* and *Batch* tabs when one is focused.
- **Space / Enter** — toggle checkboxes and click buttons.

Accessibility features:

- Skip link to main content (visible on first Tab press).
- Visible focus outlines in Red Hat red.
- ARIA `radiogroup` for Brand profile chips and `tablist` for mode tabs.
- Live regions announce errors, suggestions, validation status, and batch progress.
- The QR `<canvas>` and exported SVG carry descriptive labels for screen readers.
- Honors `prefers-reduced-motion`.

---

## 9. Troubleshooting

### My QR code won't scan from a phone

- Increase contrast — switch to a darker module color.
- Try a larger size (Extra large) and avoid pixelation when reprinting.
- Reduce or remove the logo.
- Shorten the encoded text — long URLs produce denser, harder-to-scan codes. Consider a URL shortener for very long links.

### The validation badge says "Could not decode"

The logo + content combination is too aggressive. Try, in order:
1. Reduce the size of your custom logo before uploading.
2. Switch from **Liquid** to **Square** style.
3. Increase the size to Extra large.
4. Shorten the URL or text.

### Logos don't embed when I download SVG

This happens when the page is opened via `file://` because browsers taint the canvas for security. The SVG still downloads, but the logo `<image>` references the original filename rather than embedding the bytes — so the logo only shows when the SVG sits alongside the original logo file.

Fix: serve the project over `http://` (see [Getting started](#1-getting-started)).

### "Copy image" doesn't work

Your browser may not implement the Clipboard `write()` API. Use **Download PNG** and paste the file directly into your destination.

### The Brand profile chip stays deselected

This is expected after any manual change to the logo dropdown, file upload, or color picker. Click the desired profile chip again to re-apply its preset.

### Batch generation seems frozen

A 500-item batch can take 30+ seconds, depending on QR size and your CPU. The progress bar updates roughly every four items — if the bar is moving, give it another moment. If it's truly stuck, refresh the page and try a smaller batch.

---

## 10. Files in this project

| File | Purpose |
|---|---|
| `index.html` | The QR code generator app — open this in a browser |
| `USER_GUIDE.md` | This guide |
| `Logo-Red_Hat-Team-Executive_Briefing_Center_Team-A-Standard-RGB.png` | Red Hat EBC team logo |
| `Logo-Red_Hat-A-RGB.Small-logo-transparent.png` | Red Hat standard logo |
| `Logo-Red_Hat-A-Reverse-RGB.Small-logo-transparent.png` | Red Hat reverse (for dark backgrounds) |
| `Logo-OpenAccelerator-A-Standard-RGB.png` | The Open Accelerator standard logo |
| `Logo-OpenAccelerator-A-Reverse-RGB.png` | The Open Accelerator reverse logo |

### Distribution

To share the tool with colleagues, copy the entire folder (or zip it). All assets are local — no internet connection is required at runtime except for the Google Fonts and the three CDN libraries (qrcode-generator, jsQR, JSZip).

For an internal deployment, drop the folder on any static web host (S3, GitHub Pages, an internal Apache/nginx, etc.) and share the URL.

---

*Red Hat · Executive Briefing Center Team*
