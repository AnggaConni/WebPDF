# WebPDF OCR Overhaul Roadmap

## Phase 1 — Local OCR MVP (implemented on this branch)
- Add OCR Studio modal to the existing editor.
- Use PDF.js to render selected PDF pages to canvas.
- Use Tesseract.js in the browser for Indonesian/English recognition.
- Show page-level text results, progress, cancellation, and TXT export.
- Keep cloud OCR disabled.

## Phase 2 — Searchable PDF
- Preserve OCR word/line bounding boxes and map them to original PDF coordinates.
- Add a genuine invisible text layer to each scanned page. (MVP export now implemented using Tesseract word boxes and PDF.js coordinate conversion.)
- Validate text selection/search in at least two independent PDF readers.
- Preserve original visual scan and existing annotations.
- Do not claim redaction or editing of underlying scanned pixels.

## Phase 3 — Scan quality and scale
- Add page rotation detection and optional grayscale/contrast/threshold preprocessing.
- Add page-range selection and safe queue limits.
- Reuse OCR worker where appropriate; release canvas and image buffers after each page.
- Add resumable project state only after privacy and storage behavior are documented.

## Phase 4 — Optional cloud provider
- Add a provider adapter interface, but do not enable a provider by default.
- Explain which file/pages will be sent, what provider receives them, and any retention implications.
- Require explicit confirmation before upload.
- Keep the local workflow available without an account.

## Regression risks
- OCR coordinates may drift on rotated or non-standard-size pages.
- High-resolution rendering can consume substantial memory.
- OCR accuracy varies with scan quality, fonts, tables, and languages.
- Changes to PDF.js or Tesseract.js CDN versions can affect compatibility.
- Existing annotation/page operations must be regression-tested after export changes.

## Acceptance tests
1. Digital PDF, scanned PDF, and mixed PDF are processed without uploading document bytes to a WebPDF backend.
2. Current-page and all-page modes produce correct page labels.
3. OCR output can be edited and exported as UTF-8 TXT.
4. Searchable PDF export retains the original page appearance and adds an invisible text layer; verify search/selection in external readers.
5. Cancellation retains results for completed pages.
6. UI remains usable during OCR and temporary canvases are released.
7. Existing editor workflows remain functional.
8. Searchable-PDF support is not considered production-ready until text search/selection is verified in external PDF readers.
