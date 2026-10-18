# Résumé — Alex Deluar Husen Sayidi

A single-page, print-ready A4 résumé rendered as a static website. No build step, no
dependencies, no external webfonts — it renders and prints correctly fully offline.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The résumé document (all 8 sections) |
| `styles.css` | Screen styling + the entire print stylesheet |
| `README.md` | This file |

## Export to PDF

1. Open `index.html` in any modern browser (Chrome, Edge, Safari, Firefox).
2. Click the **Download PDF** button in the toolbar at the top of the page.
3. In the browser print dialog choose **Save as PDF** as the destination, then set:
   - **Paper size:** A4
   - **Margins:** Default (the document supplies its own `@page` margin of 14mm/15mm)
   - **Headers and footers:** **OFF** — uncheck both. They are the main cause of stray
     page numbers and the file-URL banner.
   - **Background graphics:** **ON** — keeps the indigo accents, tags and rules in colour.
     If your browser shows grey boxes instead of colour, this setting is the cause.
4. Save. The result is a clean A4 PDF with no browser header or footer. The section layout is
   tuned to fit one page, but confirm page count in the print preview and adjust `@page`
   margins or the print font sizes at the end of `styles.css` if your build spills to two.

### Browser menu alternative
`File ▸ Print…` (macOS: `⌘P`) and select **Save as PDF** — identical result.

### Headless export (for scripting or CI)

```bash
# Chrome / Edge — disables the header/footer by default
google-chrome --headless --disable-gpu --no-pdf-header-footer \
  --print-to-pdf=alex-delsyarus-sayidi.pdf \
  "file://$PWD/index.html"

# macOS
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu --no-pdf-header-footer \
  --print-to-pdf=alex-delsyarus-sayidi.pdf \
  "file://$PWD/index.html"
```

Firefox: `about:config` → set `print.print_header_footer` / `print.print_footer_timestamp`
to `false`, or use File ▸ Print ▸ Save as PDF with header/footer unchecked.

## Why the print output is safe

| Concern | How it is handled |
| --- | --- |
| Page size & clipping | `@page { size: A4; margin: 14mm 15mm; }` |
| Sections splitting across pages | `page-break-inside: avoid` on every `.block` (plus `break-inside: avoid`) |
| Toolbar leaking into the PDF | `@media print { .toolbar { display: none !important; } }` |
| Offline rendering | System font stack only — no Google Fonts, no webfont requests |
| Broken images offline | Avatar is a CSS circle with the initials "AH" — no image files |
| Repeating print artefacts | No `position: fixed` / `sticky` elements inside `.page` |
| Print-engine quirks | No `backdrop-filter`, no exotic properties; body print type steps down to 11px (10.5px floor) |
| Accent colour stripped | `print-color-adjust: exact` on `body` |

## Editing

Content lives in plain HTML — edit the text directly and reload. Design tokens
(accent, ink, body, rule colours, font stack) are CSS custom properties at the top
of `styles.css` under `:root`.

## Note on details

The GitHub handle is `onelpawarai`, derived from the repository owner and the builder
name given in the brief. Email, phone and links beyond GitHub were not provided and have
been left out rather than invented.
