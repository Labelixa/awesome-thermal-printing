# Awesome Thermal Printing

A curated list of tools, references and specifications for **thermal label
printing** — ZPL, EPL, TSPL, CPCL, barcodes and the systems that drive them.

Curation rules, so the list stays worth reading:

- Every entry is something a person can open and use today. No "coming soon".
- Vendor documentation is linked to the vendor, not to a mirror.
- Paid products are marked `$`. Nothing is ranked; the list is alphabetical
  inside each section.
- An entry is removed when its link dies or the project is archived.

## Printer languages

| Language | Printers | Where it is specified |
| --- | --- | --- |
| ZPL / ZPL II | Zebra and many compatibles | Zebra Programming Guide (vendor PDF) |
| EPL2 | Older Zebra/Eltron desktop units | Zebra EPL2 Programming Guide |
| TSPL / TSPL2 | TSC and compatibles | TSC TSPL/TSPL2 Programming Manual |
| CPCL | Zebra mobile printers | Zebra CPCL Programming Guide |
| DPL | Honeywell/Datamax | Honeywell DPL Programmer's Manual |
| SBPL | SATO | SATO programming reference |
| IPL | Intermec/Honeywell | Honeywell IPL manual |

Emulation is not native support: many printers can *also* speak a competitor's
language through a vendor emulation mode, and how much of the language that
mode covers is decided by the vendor and can change between firmware versions.

## Viewers, validators and converters

- **Labelixa** — render ZPL/EPL/TSPL/CPCL in the browser, lint it, convert
  between print densities, and call the same engine over an API or MCP:
  <https://labelixa.com>
- **Labelary** — the long-standing ZPL viewer and rendering API.
- **zint** — open-source barcode encoder (library + CLI) covering most 1D and
  2D symbologies.
- **ZXing / zxing-cpp** — barcode decoders; the practical way to read back what
  a printed label actually encodes.

## Barcode standards worth reading before you encode

- **GS1 General Specifications** — Application Identifiers, quiet zones, the
  rules that make a GS1-128 or GS1 Data Matrix valid rather than merely
  scannable.
- **ISO/IEC 15417** (Code 128), **ISO/IEC 15420** (EAN/UPC), **ISO/IEC 16022**
  (Data Matrix), **ISO/IEC 18004** (QR).
- **ISO/IEC 15416 / 15415** — print quality grading for linear and 2D symbols;
  the vocabulary a verifier report uses.

## Sending bytes to a printer

- Raw TCP port 9100 — the lowest common denominator; no acknowledgement, no
  undo.
- CUPS raw queues on macOS/Linux; `lp -o raw`.
- Windows: generic/text-only driver, or writing directly to the share.
- Browsers cannot open TCP sockets: web applications need a backend relay, a
  local helper, or a rendered image printed through the OS driver.

## Label design and data

- Template + merge is the normal architecture: business data from the ERP/WMS,
  layout from a template, ZPL out, printer in.
- Test every variable field with the **longest real value**, not the average
  one — an overflowing product name is the most common production failure.
- Keep a template per print density, or convert deliberately: coordinates are
  printer dots, so a 203 dpi layout prints two-thirds size on a 300 dpi head.

## Contributing

Open a pull request. One entry per PR, with a one-line reason it belongs and a
link that works without a login.
