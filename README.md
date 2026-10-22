# WebPDF

A browser-based PDF editor built with PDF.js and pdf-lib.

## Current capabilities

- Open and render PDF files in the browser
- Add text, freehand marks, stamps, images, and drawn signatures
- Insert blank pages or pages from another PDF
- Rotate and delete pages
- Undo/redo annotation changes
- Export an edited PDF
- **OCR Studio MVP:** recognize scanned pages locally in the browser and export editable OCR text as TXT

## Local-first OCR Studio

1. Open a PDF in WebPDF.
2. Select the **OCR Studio** scan-text icon in the toolbar.
3. Choose Indonesian + English, Indonesian, or English.
4. Select all pages or the currently active page, then choose render quality.
5. Run OCR, review/correct the recognized text, and export TXT.

### Privacy and connectivity

The PDF is rendered and recognized in the browser; WebPDF does not upload the document to its own server. The Tesseract.js library and language data may be downloaded from their configured CDN on first use, so this MVP is **local document processing, not yet fully offline**. Cloud OCR is not enabled. Do not use this MVP as a guarantee of transcription accuracy for legal, medical, financial, or other high-stakes documents without human review.

### Current OCR scope

- OCR output per page and editable result panel
- Indonesian and English language options
- Progress reporting and cancellation between page tasks
- TXT export with page separators

Searchable-PDF export, persistent OCR project storage, preprocessing, and optional cloud providers remain future work. Do not treat the current TXT export as a searchable-PDF feature.

## Development notes

The application is currently a single-page HTML implementation. New OCR behavior is isolated in a dedicated section of the existing script to limit changes to the original editor. A later refactor can move OCR into separate JavaScript modules once regression tests cover the existing editing workflow.

## Testing checklist

- Open a text-based PDF and a scanned PDF.
- Run OCR on the current page and on all pages.
- Test each language option.
- Cancel OCR during a multi-page document and confirm completed page results remain available.
- Edit recognized text, switch page results, and confirm the edits are retained.
- Export TXT and confirm page separators and edited text are present.
- Re-test existing annotation, signature, image, stamp, page insertion/deletion/rotation, and PDF export features.
- Disable network access after dependencies have loaded: the PDF itself should remain local, but first-time OCR dependency/model loading may fail offline.
