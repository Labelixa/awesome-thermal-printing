# Awesome Thermal Printing

A curated list of tools, references and specifications for **thermal label
printing** — ZPL, EPL, TSPL, CPCL, barcodes and the systems that drive them.

Curation rules, so the list stays worth reading:

- Every entry is something a person can open and use today. No "coming soon".
- Vendor documentation is linked to the vendor, not to a mirror.
- Paid products are marked `$`. Nothing is ranked; the list is alphabetical
  inside each section.
- Library entries carry the language and what they produce; a library that
  only *renders* ZPL is listed under viewers, not generators.
- An entry is removed when its link dies or the project is archived.

## Contents

- [Printer languages](#printer-languages)
- [Viewers, validators and converters](#viewers-validators-and-converters)
- [Libraries that generate label code](#libraries-that-generate-label-code)
- [Receipt printers (ESC/POS)](#receipt-printers-escpos)
- [Vendor tools and SDKs](#vendor-tools-and-sdks)
- [Barcode standards worth reading before you encode](#barcode-standards-worth-reading-before-you-encode)
- [GS1 tooling](#gs1-tooling)
- [Sending bytes to a printer](#sending-bytes-to-a-printer)
- [Label design and data](#label-design-and-data)
- [Example and reference repositories](#example-and-reference-repositories)

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
| ESC/POS | Receipt printers (Epson and most compatibles) | Epson ESC/POS Command Reference |

Emulation is not native support: many printers can *also* speak a competitor's
language through a vendor emulation mode, and how much of the language that
mode covers is decided by the vendor and can change between firmware versions.

## Viewers, validators and converters

- **BinaryKits.Zpl** (.NET) — ZPL parser, analyzer and renderer as a library;
  useful when the preview has to happen inside your own application:
  <https://github.com/BinaryKits/BinaryKits.Zpl>
- **Labelary** — the long-standing ZPL viewer and rendering API:
  <https://labelary.com>
- **Labelixa** — render ZPL/EPL/TSPL/CPCL in the browser, lint it, convert
  between print densities, and call the same engine over an API or MCP:
  <https://labelixa.com>
- **zint** — open-source barcode encoder (library + CLI) covering most 1D and
  2D symbologies: <https://zint.org.uk>
- **ZXing / zxing-cpp** — barcode decoders; the practical way to read back what
  a printed label actually encodes: <https://github.com/zxing-cpp/zxing-cpp>

## Libraries that generate label code

Builders and DSLs whose output is printer code. Check the last commit before
you depend on one; several in this space are finished rather than maintained.

- **cod3monk/zpl** (Python) — ZPL II label class with millimetre units:
  <https://github.com/cod3monk/zpl>
- **DanieLeeuwner/JSZPL** (JavaScript) — build ZPL II from JS objects, npm
  `jszpl`: <https://github.com/DanieLeeuwner/JSZPL>
- **Dwarf1er/openlabel** (C#) — label generation for .NET:
  <https://github.com/Dwarf1er/openlabel>
- **bbulpett/zebra-zpl** (Ruby) — ZPL generation for Ruby applications:
  <https://github.com/bbulpett/zebra-zpl>
- **benfaerber/pdf-to-zpl** (PHP) — turn a PDF page into a ZPL graphic:
  <https://github.com/benfaerber/pdf-to-zpl>
- **mortonl/zebra-label-generator** (Java) — ZPL generation that keeps the
  layout independent of print density: <https://github.com/mortonl/zebra-label-generator>
- **productdevbook/portakal** (TypeScript) — generates ZPL, EPL, TSPL and
  CPCL from one model; one of the few generators that is not ZPL-only:
  <https://github.com/productdevbook/portakal>

## Receipt printers (ESC/POS)

Not label printers, but the same bytes-to-a-port discipline and often the
same counter.

- **node-escpos** (Node.js) — ESC/POS driver for USB, serial, network and
  Bluetooth printers: <https://github.com/song940/node-escpos>
- **python-escpos** (Python) — ESC/POS library with a printer capability
  database: <https://github.com/python-escpos/python-escpos>

## Vendor tools and SDKs

- **BarTender** `$` (Seagull Scientific) — label design and print-management
  suite: <https://www.seagullscientific.com>
- **NiceLabel** `$` (Loftware) — label design and cloud print management:
  <https://www.nicelabel.com>
- **Zebra Browser Print** — lets a web page print to a local Zebra printer
  through a small host application, without opening raw sockets from the
  browser: <https://www.zebra.com/us/en/software/printer-software/browser-print.html>
- **Zebra Link-OS SDK** — printer discovery, status and printing from
  Android, iOS, Windows, Java and .NET:
  <https://www.zebra.com/us/en/software/printer-software/link-os-sdk.html>
- **ZebraDesigner** — Zebra's own label designer; the free edition covers
  basic layouts: <https://www.zebra.com/us/en/software/printer-software/zebradesigner.html>

## Barcode standards worth reading before you encode

- **GS1 General Specifications** — Application Identifiers, quiet zones, the
  rules that make a GS1-128 or GS1 Data Matrix valid rather than merely
  scannable.
- **ISO/IEC 15417** (Code 128), **ISO/IEC 15420** (EAN/UPC), **ISO/IEC 16022**
  (Data Matrix), **ISO/IEC 18004** (QR).
- **ISO/IEC 15416 / 15415** — print quality grading for linear and 2D symbols;
  the vocabulary a verifier report uses.

## GS1 tooling

- **GS1 Digital Link toolkit** (JavaScript) — build and parse GS1 Digital Link
  URIs: <https://github.com/gs1/GS1DigitalLinkToolkit.js>
- **GS1 Syntax Engine** — the reference library for validating Application
  Identifier strings (element strings, GS1 Digital Link):
  <https://github.com/gs1/gs1-syntax-engine>

## Sending bytes to a printer

- Raw TCP port 9100 — the lowest common denominator; no acknowledgement, no
  undo.
- CUPS raw queues on macOS/Linux; `lp -o raw`.
- Windows: generic/text-only driver, or writing directly to the share.
- Browsers cannot open TCP sockets: web applications need a backend relay, a
  local helper (see Zebra Browser Print above), or a rendered image printed
  through the OS driver.

## Label design and data

- Template + merge is the normal architecture: business data from the ERP/WMS,
  layout from a template, ZPL out, printer in.
- Test every variable field with the **longest real value**, not the average
  one — an overflowing product name is the most common production failure.
- Keep a template per print density, or convert deliberately: coordinates are
  printer dots, so a 203 dpi layout prints two-thirds size on a 300 dpi head.
- Preview before you print, and preview at the printer's density: a label
  that looks right at 8 dpmm can clip at 12 dpmm.

## Example and reference repositories

- **Labelixa/thermal-printer-cheatsheets** — one-page command references for
  ZPL, EPL, TSPL and CPCL: <https://github.com/Labelixa/thermal-printer-cheatsheets>
- **Labelixa/thermal-printer-examples** — EPL, TSPL and CPCL examples that
  render in CI: <https://github.com/Labelixa/thermal-printer-examples>
- **Labelixa/zpl-examples** — working, CI-tested ZPL labels plus integration
  snippets in several languages: <https://github.com/Labelixa/zpl-examples>

## Contributing

Open a pull request. One entry per PR, with a one-line reason it belongs and a
link that works without a login.
