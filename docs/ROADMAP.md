# PaperKnife for iPhone and iPad — roadmap

iOS development starts after Windows milestone M1, so it can reuse a proven editing model and the
shared test corpus. Each milestone ends with an app that can be installed through TestFlight.

## I0 — Foundation

- Xcode project for a SwiftUI document-based app, Apache-2.0 notices and an acknowledgements
  screen, CI on macOS that builds the app and runs tests in the simulator.
- A script that downloads the pinned PDFium release, checks its checksum and assembles an
  XCFramework (device arm64, simulator arm64 and x86_64).
- Open PDFs from the Files app (including password-protected files); view them with PDFKit.

## I1 — Verified text editing

- Port the Windows editing model: immutable snapshots, transactional edits, verification
  (character support, round trip, object counts, pixel comparison), undo and redo.
- Tap text to select it, edit it, see a clear explanation when an edit is refused.
- Run the shared corpus in the simulator and compare results with Windows.

## I2 — Pages

- Thumbnail grid with drag to reorder, rotate, delete, extract, merge and split.
- Share sheet and drag and drop between apps on iPad.

## I3 — Markup and forms

- Apple Pencil drawing (PencilKit), highlights, notes and form filling.

## I4 — Toolbox

- Scan documents with the camera (VisionKit, on the device).
- Compress, images to PDF and PDF to images.

## I5 — Text recognition

- Make scanned pages searchable with the Vision framework, on the device.

## Distribution

- App Store and TestFlight. Apache-2.0 and PDFium's licenses are compatible with App Store
  distribution; their notices are shown in the app.
