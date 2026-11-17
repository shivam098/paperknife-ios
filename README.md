# PaperKnife for iPhone and iPad

**An offline, open-source PDF editor for iPhone and iPad.** Part of [PaperKnife](https://github.com/shivam098/paperknife-windows):
your documents never leave your device — no uploads, no account, no telemetry.

> **Status: planning.** No app code yet. Windows is the lead implementation; iOS development
> starts once the editing model and shared test corpus are proven there (Windows milestone M1).
> See the [roadmap](docs/ROADMAP.md) and [architecture plan](docs/ARCHITECTURE.md).

## Planned features

The same promises as every PaperKnife app ([product principles](https://github.com/shivam098/paperknife-windows/blob/main/docs/PRODUCT.md)):

- Edit existing text in place, keeping the original font, size, position and color.
- Verify every change before keeping it, and refuse with a clear reason instead of damaging the
  document.
- Organize pages: rotate, delete, reorder, merge and split.
- Later: Apple Pencil markup, form filling, document scanning and on-device text recognition.

## Planned technology

| Area | Choice |
|---|---|
| Language and UI | Swift, SwiftUI, a document-based app that works with the Files app |
| Viewing | PDFKit (smooth scrolling, zoom and accessibility) |
| Editing and verification | [PDFium](https://pdfium.googlesource.com/pdfium/) from the [pdfium-binaries](https://github.com/bblanchon/pdfium-binaries) iOS builds, packaged as an XCFramework |
| Scanning and OCR (later) | VisionKit and the Vision framework, which run on the device |
| Privacy | No networking code; App Store privacy label "Data Not Collected" |

Building requires a Mac with Xcode.

## Contributing

Ideas and design feedback are welcome in issues. See [CONTRIBUTING.md](CONTRIBUTING.md) and
[SECURITY.md](SECURITY.md).

## License

[Apache License 2.0](LICENSE).
