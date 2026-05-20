# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

_Nothing pending._

## [1.3.0] - 2026-05-20

### Added

- **Red Hat Customer Marketing brand profile** — fourth built-in chip applying the Customer Marketing team logo with Red Hat red (`#EE0000`).
- Two new preset logos in the Logo dropdown: **Red Hat Customer Marketing** (color) and **Red Hat Customer Marketing (reverse)** (light, for dark QR codes).
- URL auto-suggestion now recognizes `customer-marketing` keywords and offers the matching logo.

## [1.2.0] - 2026-05-19

### Added

- **Transparent background** toggle in the Appearance section. The canvas, PNG, and SVG outputs all carry true alpha transparency — useful for overlaying QR codes on colored brand artwork. A subtle CSS checkerboard pattern behind the canvas indicates transparency visually in the browser.

### Changed

- `validateScan` now composites transparent canvases onto white in a hidden canvas before decoding, so the ✓ Verified scannable badge still works for transparent codes.

## [1.1.0] - 2026-05-19

### Added

- **Saved custom profiles.** Snapshot the current logo + color as a named profile via the new "+ Save as…" chip. Custom chips appear alongside the built-ins; click to apply, double-click to rename, hover for the × delete, drag to reorder. Backed by `localStorage` (key `qr-custom-profiles-v1`), capped at 20 profiles / 4 MB total.
- **Profile export / import.** Round-trip all custom profiles through a JSON file for sharing between machines or teammates ("Export all" / "Import…" under the chips row).
- **Persisted last-used settings.** Type, style, size, border, transparent flag, color, and logo (when non-custom) are remembered across sessions (`qr-last-settings-v1`).
- **Color scannability warning.** WCAG relative-luminance check on the color picker shows an orange warning for risky colors and a red warning for colors that almost certainly won't scan against white.
- **Drag-and-drop logo upload.** Drop a PNG/JPG/SVG/WebP file anywhere on the card to set it as the custom logo. A dashed red outline marks the drop zone.
- **Brand color swatch picker.** Red Hat (`#EE0000`, `#BE0000`, `#151515`, `#4D4D4D`) and The Open Accelerator (`#151515`, `#F7F5F3`, `#FFC600`, `#B36924`, `#77C5D5`, `#005761`, `#FF6A39`, `#9A3324`, `#FFFFFF`) preset swatches under the color input. Active swatch outlined in Red Hat red.
- **Inline rename of custom profiles.** Double-click any custom chip to edit its name in place — Enter saves, Escape cancels, blur commits.
- **Drag-to-reorder custom profiles.** Drag any custom chip; red insertion-line indicators show where it'll land. The new order persists.
- **Smart batch filename templates.** Tokens `{name}` `{date}` `{host}` `{slug}` `{index}` for batch output filenames. Default `{name}` preserves the original behavior.
- **Recent generations history.** Collapsible panel under the output showing the last 12 generations with one-click restore of the exact settings and a per-item × delete (`qr-recent-v1`, capped at 256 KB).

### Changed

- `inferProfileFromState` now matches custom profiles in addition to the built-in three when deciding which chip to highlight.
- `getBatchItems` applies the active filename template to each derived item rather than emitting `safeFilename(rawName)` directly.

## [1.0.0] - 2026-05-19

### Added

- Initial public release of the **Red Hat EBC QR Code Generator** — a single static HTML page, no build step.
- Six content types: URL/text, WiFi, Email, SMS, Contact (vCard 3.0), Calendar event (iCal).
- Built-in brand profiles: **None**, **Red Hat EBC**, **The Open Accelerator** — each applies a matching logo + brand color in one click.
- Five preset logos (Red Hat, EBC, TOA + reverse variants) and custom uploads up to 2 MB (PNG/JPG/SVG/WebP).
- URL-keyword auto-suggestion for matching logos (`redhat.com`, `openaccelerator`, etc.).
- Two QR styles: classic **square** and **liquid** (rounded modules with circular finder patterns).
- Three export formats: PNG (raster), SVG (vector), and clipboard copy.
- Batch generation: paste a list or upload a CSV, get back a ZIP with PNGs, SVGs, or both — up to 500 codes per batch.
- Post-render scan validation via `jsQR`.
- Red Hat brand styling: Red Hat Display + Red Hat Text fonts, Red Hat red (`#EE0000`) accents, black topbar with EBC logo, branded modal, suggestion banner, and validation badges.
- Fully accessible: skip link, focus management, ARIA roles, live regions, keyboard navigation between tabs and chips, `prefers-reduced-motion` support.
- Companion user guide in Markdown and Red Hat-branded HTML.

[Unreleased]: https://github.com/holzerjm/QRcode-Generator/compare/main...HEAD
[1.3.0]: https://github.com/holzerjm/QRcode-Generator/commits/main
[1.2.0]: https://github.com/holzerjm/QRcode-Generator/commit/3b3f792
[1.1.0]: https://github.com/holzerjm/QRcode-Generator/commit/6040ad6
[1.0.0]: https://github.com/holzerjm/QRcode-Generator/commit/da69a53
