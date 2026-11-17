# PaperKnife for iPhone and iPad — architecture plan

This is a plan, not a description of existing code. It follows the design proven in
[PaperKnife for Windows](https://github.com/shivam098/paperknife-windows/blob/main/docs/ARCHITECTURE.md).

## Structure

| Part | Responsibility |
|---|---|
| `PaperKnifeCore` (Swift package) | Snapshots, the document session, verification rules and undo history, on top of a small Swift wrapper around the PDFium C API. No UI code. |
| `PaperKnife` (app target) | SwiftUI document-based app, PDFKit viewer, editing panel. |
| `third_party/pdfium` | Script that downloads the pinned PDFium release and builds an XCFramework. Binaries aren't committed. |

## PDF engines

- **PDFKit** displays documents: it provides smooth scrolling, zoom, text selection and
  VoiceOver support. After each committed edit the viewer reloads the new snapshot.
- **PDFium** (from [pdfium-binaries](https://github.com/bblanchon/pdfium-binaries), the build
  without V8) performs edits and renders the pages used for verification. PDFKit can add
  annotations but can't change the text drawn on a page.
- All PDFium calls go through one Swift `actor`, which serializes them because PDFium isn't
  thread-safe.

Because PDFKit and PDFium can render the same page slightly differently, verification always
compares PDFium renderings with each other, never with what PDFKit shows.

## Editing model

The same transaction as on Windows: apply the change to a scratch copy, save it, reload it,
verify it (character support, text round trip, object counts per type, pixel comparison of the page with
the edited text hidden), then commit or discard. iOS-specific points:

- **Memory.** iOS ends apps that use too much memory, so the undo history has a smaller budget
  and older snapshots are written to the app's caches folder.
- **Saving.** The document architecture (`DocumentGroup` and file coordination) writes files
  atomically and works with iCloud Drive and other file providers. Exporting a copy is the
  default.

## Privacy

- No networking code, analytics, crash-reporting or advertising SDKs.
- App Store privacy label: "Data Not Collected".

## Testing

- Unit tests for `PaperKnifeCore` run in the simulator on CI.
- The shared corpus runs in the simulator, and results are compared with the Windows app.

## Open questions

- Minimum iOS version (proposal: the two most recent major versions at launch).
- Whether `PaperKnifeCore` should live in its own repository so the macOS app can use the same
  Swift package, instead of each app keeping its own copy.
