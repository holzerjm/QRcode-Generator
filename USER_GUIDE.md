# Red Hat EBC QR Code Generator — User Guide

A web-based tool for creating branded QR codes for URLs, WiFi networks, email, SMS, contact cards, calendar events, and bulk batches. Built for the Red Hat Executive Briefing Center team.

---

## Contents

1. [Getting started](#1-getting-started)
2. [Quick start: Brand profiles](#2-quick-start-brand-profiles)
3. [Saved profiles](#3-saved-profiles)
4. [Single QR code generation](#4-single-qr-code-generation)
5. [Logo selection](#5-logo-selection)
6. [Appearance: style, border, transparency, size, color](#6-appearance-style-border-transparency-size-color)
7. [Output, downloads, and validation](#7-output-downloads-and-validation)
8. [Recent generations](#8-recent-generations)
9. [Batch generation](#9-batch-generation)
10. [Keyboard and accessibility](#10-keyboard-and-accessibility)
11. [Troubleshooting](#11-troubleshooting)
12. [Files in this project](#12-files-in-this-project)

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

- **Top bar** — Red Hat EBC logo plus a "User guide →" link.
- **Card** — generation mode, brand profile, content fields, logo, appearance, and the generate button.
- **Output panel** — appears after generation with download/copy buttons.
- **Recent generations** — collapsible list of your last few codes, restored with one click.

Your last-used settings (type, style, size, border, transparent flag, color, and logo) are remembered between sessions in your browser's local storage.

---

## 2. Quick start: Brand profiles

The fastest way to create a branded QR code:

1. Pick a **Brand profile** chip at the top of the card:
   - **None** — no logo, black QR code (the default).
   - **Red Hat EBC** — applies the Red Hat EBC logo with Red Hat red (`#EE0000`).
   - **The Open Accelerator** — applies the TOA logo with TOA yellow (`#FFC600`).
   - **Customer Marketing** — applies the Red Hat Customer Marketing logo with Red Hat red (`#EE0000`).
2. Enter your URL in the **URL or text** field.
3. Click **Generate QR code**.

The selected chip stays highlighted in its brand color. If you later change the logo, color, or upload a custom file, the chip auto-deselects to show you've gone off-preset; click the chip again to snap back.

---

## 3. Saved profiles

In addition to the three built-in chips you can save any logo + color combination as a **custom profile** and apply it later with one click.

### Save the current settings

1. Configure the logo and color you want.
2. Click the dashed **+ Save as…** chip.
3. Enter a name (e.g. *AnsibleFest 2026*) in the modal and click **Save profile**.

A new chip with your chosen color appears alongside the built-ins. Up to 20 custom profiles can be saved.

### Apply, rename, reorder, delete

- **Apply** — single-click the chip.
- **Rename** — double-click the chip; type the new name; Enter to save, Escape to cancel.
- **Reorder** — drag the chip left/right. A red insertion line shows where it'll land.
- **Delete** — hover or focus the chip, then click the **×** in the corner (a confirmation is shown).

### Export and import

Use the **Export all** and **Import…** links beneath the chips row:

- **Export all** downloads `qr-profiles-YYYY-MM-DD.json` containing all of your custom profiles (including any embedded custom logo data).
- **Import…** loads a JSON file and merges its profiles into your existing list. Profiles with conflicting IDs get fresh IDs so duplicates can coexist.

Profile data is stored in your browser only. Use Export / Import to share profiles between machines or with teammates.

---

## 4. Single QR code generation

The **Single** tab (selected by default) creates one QR code at a time. Use the **QR code type** dropdown to pick what you're encoding.

| Type | What it produces | Typical use |
|---|---|---|
| URL / text | Opens a URL or shows free-form text | Websites, landing pages, plain text |
| WiFi | One-tap connection to a WiFi network | Guest WiFi cards, EBC reception posters |
| Email | Opens an email composer with optional subject and body | Contact cards, feedback links |
| SMS | Opens an SMS composer with optional message | Opt-in numbers, quick contact |
| Contact (vCard) | Adds a contact to the user's address book | Business cards, name badges |
| Calendar event | Adds an event to the user's calendar | Event posters, save-the-date materials |

### 4.1 URL / text

Enter a URL or any text in the single field. When the URL contains keywords like `redhat.com`, `ebc.redhat.com`, or `openaccelerator`, a banner appears suggesting the matching brand logo — click **Apply** to add it, or **Dismiss** to keep your current selection.

### 4.2 WiFi

Fields:
- **Network name (SSID)** — required.
- **Password** — click *Show* to reveal while typing.
- **Security** — WPA/WPA2/WPA3 covers virtually every modern network. WEP is legacy. *None* is for open networks.
- **Hidden** — check if the SSID is not broadcast.

### 4.3 Email

- **Recipient email** — required.
- **Subject** — optional; pre-fills the email subject line.
- **Body** — optional; pre-fills the email body.

The QR code uses the standard `mailto:` URL with proper encoding.

### 4.4 SMS

- **Phone number** — required. International format (`+1234567890`) gives the best scanner compatibility.
- **Message** — optional; pre-fills the SMS body.

If a message is provided, the `SMSTO:` format is used (broadest compatibility). Otherwise the standard `sms:` URL is used.

### 4.5 Contact (vCard)

Provide at least a name or organization. All other fields are optional:

- **Name** — first and last.
- **Work** — organization, title.
- **Contact** — phone, mobile, email, website.

The output is a vCard 3.0 payload that imports cleanly into iOS Contacts, Android Contacts, Outlook, and most other address books.

### 4.6 Calendar event

- **Event title** — required.
- **Starts** — required, your local timezone.
- **Ends** — optional.
- **Location**, **Description** — optional.

Times are converted to UTC and packaged as a `VCALENDAR/VEVENT` payload, compatible with Google Calendar, Apple Calendar, and Outlook.

---

## 5. Logo selection

A logo embedded in the center of the QR code reinforces your brand. The generator automatically raises error correction to the highest level (~30% recovery) whenever a logo is present, so the code remains scannable.

### Preset logos

Available from the **Logo** dropdown:

- **Red Hat EBC** — the team logo (color).
- **Red Hat** — standard Red Hat fedora + wordmark.
- **Red Hat (reverse)** — light version, intended for dark QR codes.
- **The Open Accelerator** — black wordmark version.
- **The Open Accelerator (reverse)** — light version for dark backgrounds.
- **Red Hat Customer Marketing** — the Customer Marketing team logo (color).
- **Red Hat Customer Marketing (reverse)** — light version for dark backgrounds.

### Custom upload

There are two ways to apply a custom logo:

1. **File picker:** select **Upload custom…** from the Logo dropdown, then click **Choose image…** and pick a PNG, JPG, SVG, or WebP file (up to 2 MB).
2. **Drag-and-drop:** drag an image file from your desktop and drop it anywhere on the card. A dashed red outline highlights the drop zone while the file is hovering.

Either path embeds the image immediately and regenerates the QR.

### Auto-suggestion

When the URL/text field contains a recognized keyword (e.g. `redhat.com`, `ebc.redhat.com`, `openaccelerator`), a red-bordered banner appears suggesting the matching logo. This is purely a convenience — clicking **Dismiss** keeps your current setting.

---

## 6. Appearance: style, border, transparency, size, color

### Style

- **Square** — classic, sharp QR modules. Highest scanner compatibility.
- **Liquid** — rounded modules with circular finder patterns. More modern look; uses high error correction automatically.

### Border

Toggle a thin rounded border around the QR code. Useful for print contexts where you want a defined edge.

### Transparent background

When **Transparent** is on, the QR code is generated with no background fill — only the dark modules are drawn. Use this when you want to overlay the code on a colored brand background, a photo, or printed artwork.

- The PNG and SVG exports both preserve alpha transparency.
- A subtle checkerboard appears behind the canvas in the browser as a visual reminder that the background is see-through.
- The small white pad behind the embedded logo is preserved for scannability; if you want a fully transparent code, set Logo to **None**.
- Scan validation still works — the validator composites onto white internally before decoding.

### Size

- **Small** — 240 px.
- **Medium** — 360 px (default).
- **Large** — 520 px.
- **Extra large** — 720 px.

For print, choose Extra large or download as SVG (resolution-independent).

### Color

Click the color swatch to pick any color for the dark modules. Two rows of preset swatches sit underneath:

- **Red Hat** — `#EE0000`, `#BE0000`, `#151515`, `#4D4D4D`.
- **TOA** — the nine-color Open Accelerator palette (black, off-white, yellow, brown, light blue, dark teal, orange, maroon, white).

The active swatch (matching the current color) is outlined in Red Hat red.

### Color scannability warning

A WCAG luminance check runs on every color change:

- **No warning** — color is dark enough to scan reliably.
- **Orange warning** — color is borderline; may not scan against bright backgrounds.
- **Red warning** — color is too light against white; the code likely won't scan.

The warnings are advisory. You can ignore them if the code will sit on a darker background, but the validator may also fail.

---

## 7. Output, downloads, and validation

After generation, the QR code appears below the card with three actions.

### Download options

- **Download PNG** — raster image with the logo baked in. Best for digital use (web pages, email signatures, screen-share decks). Honors transparency.
- **Download SVG** — vector format with the logo embedded. Best for print at any size — scales without quality loss. Honors transparency.
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

## 8. Recent generations

Each successful generation is stored in a **Recent generations** panel that appears under the output card. The panel keeps the last 12 codes, each showing:

- A color swatch matching the QR color used.
- The label (URL, "WiFi: …", "Email: …", etc.).
- A relative timestamp ("just now", "5m ago", etc.).

Click any entry to restore that exact configuration — logo, color, style, size, border, transparent flag — and re-render the same QR. Hover an entry to reveal a **×** delete button. The **Clear all** link at the bottom empties the history.

The history is stored locally in your browser (capped at 256 KB total).

---

## 9. Batch generation

For dozens or hundreds of QR codes at once, click the **Batch** tab.

### Source: pasted list

1. Set **Source** to *Paste list*.
2. Paste your URLs into the textarea — one per line.
3. Filenames are derived from each URL's host and last path segment (e.g. `redhat.com-customer-a`) by default; see *Filename template* below to customize.

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

### Filename template

The **Filename template** field controls how each output file is named. Default is `{name}`. Available tokens:

| Token | Replaced with |
|---|---|
| `{name}` | The derived filename from paste-list URL, or the first CSV column |
| `{date}` | Today's date in `YYYY-MM-DD` format |
| `{host}` | Host part of the URL (with leading `www.` stripped), e.g. `redhat.com` |
| `{slug}` | Last path segment of the URL, e.g. `customer-a` |
| `{index}` | The 1-based row number, zero-padded to 3 digits (e.g. `001`) |

Examples:
- `{date}-{name}` → `2026-05-19-customer-a.png`
- `qr-{index}-{slug}` → `qr-001-customer-a.png`
- `{host}-{slug}` → `redhat.com-customer-a.png`

Disallowed characters are replaced with `_`.

### Generating

Click **Generate ZIP** (the primary button changes label in Batch mode). A progress bar shows how many codes have been processed. When complete, a ZIP file named `qrcodes-YYYY-MM-DD.zip` downloads automatically.

The current **Logo** and **Appearance** settings (including transparent background) apply to every code in the batch.

> **Limits:** 500 items maximum per batch. For larger jobs, split into multiple ZIPs.

---

## 10. Keyboard and accessibility

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

## 11. Troubleshooting

### My QR code won't scan from a phone

- Increase contrast — switch to a darker module color. The color scannability warning under the picker will help.
- Try a larger size (Extra large) and avoid pixelation when reprinting.
- Reduce or remove the logo.
- Shorten the encoded text — long URLs produce denser, harder-to-scan codes. Consider a URL shortener for very long links.

### The validation badge says "Could not decode"

The logo + content combination is too aggressive. Try, in order:
1. Reduce the size of your custom logo before uploading.
2. Switch from **Liquid** to **Square** style.
3. Increase the size to Extra large.
4. Shorten the URL or text.

### My transparent QR code looks weird

The checkerboard pattern behind the canvas only appears in the browser — it's a visual indicator that the background is transparent. The downloaded PNG/SVG won't include it. Place the file on the colored background where you intend to use it to see the final result.

### Logos don't embed when I download SVG

This happens when the page is opened via `file://` because browsers taint the canvas for security. The SVG still downloads, but the logo `<image>` references the original filename rather than embedding the bytes — so the logo only shows when the SVG sits alongside the original logo file.

Fix: serve the project over `http://` (see [Getting started](#1-getting-started)).

### "Copy image" doesn't work

Your browser may not implement the Clipboard `write()` API. Use **Download PNG** and paste the file directly into your destination.

### The Brand profile chip stays deselected

This is expected after any manual change to the logo dropdown, file upload, or color picker. Click the desired profile chip again to re-apply its preset.

### My saved profiles disappeared

Profiles are stored in `localStorage`, which is per-browser, per-origin, and can be cleared by:
- Clearing browser site data for the origin.
- Opening the site in a different browser or incognito window.
- Switching to a different machine.

Use **Export all** regularly to keep a JSON backup that you can re-import.

### Batch generation seems frozen

A 500-item batch can take 30+ seconds, depending on QR size and your CPU. The progress bar updates roughly every four items — if the bar is moving, give it another moment. If it's truly stuck, refresh the page and try a smaller batch.

### A recent-history entry restores the wrong logo

If the entry used an uploaded custom logo, the image data is stored alongside the entry. Very large custom logos may have been dropped during storage compaction. Re-upload the logo, then re-save the profile if needed.

---

## 12. Files in this project

| File | Purpose |
|---|---|
| `index.html` | The QR code generator app — open this in a browser |
| `USER_GUIDE.md` | This guide |
| `user-guide.html` | Branded HTML user guide |
| `README.md` | Project overview |
| `CHANGELOG.md` | Release history |
| `LICENSE` | MIT license for the source code |
| `Logo-Red_Hat-Team-Executive_Briefing_Center_Team-A-Standard-RGB.png` | Red Hat EBC team logo |
| `Logo-Red_Hat-A-RGB.Small-logo-transparent.png` | Red Hat standard logo |
| `Logo-Red_Hat-A-Reverse-RGB.Small-logo-transparent.png` | Red Hat reverse (for dark backgrounds) |
| `Logo-OpenAccelerator-A-Standard-RGB.png` | The Open Accelerator standard logo |
| `Logo-OpenAccelerator-A-Reverse-RGB.png` | The Open Accelerator reverse logo |
| `Logo-Red_Hat-Customer_Marketing_Team-A-Standard-RGB_Small_logo_transparent.png` | Red Hat Customer Marketing logo |
| `Logo-Red_Hat-Customer_Marketing_Team-A-Reverse-RGB_Small_logo_transparent.png` | Red Hat Customer Marketing reverse logo |

### Distribution

To share the tool with colleagues, copy the entire folder (or zip it). All assets are local — no internet connection is required at runtime except for the Google Fonts and the three CDN libraries (qrcode-generator, jsQR, JSZip).

For an internal deployment, drop the folder on any static web host (S3, GitHub Pages, an internal Apache/nginx, etc.) and share the URL.

### Local storage keys

The app stores a few things locally in your browser:

| Key | Purpose | Cap |
|---|---|---|
| `qr-custom-profiles-v1` | Saved custom profiles (name, color, logo) | 20 profiles / 4 MB |
| `qr-last-settings-v1` | Last-used type, style, size, color, logo, transparent flag | ~1 KB |
| `qr-recent-v1` | Recent generations history | 12 items / 256 KB |

---

*Red Hat · Executive Briefing Center Team*
