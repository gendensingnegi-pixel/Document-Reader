# Document Reader

An offline-first Android document reader with text-to-speech narration, on-device OCR, and audio export, built for screen-reader users. Written in Kotlin with Jetpack Compose.

**Download (public testing):** get the latest APK from [Releases](../../releases). Current version: 1.0.0 (version code 4). Requires Android 8.0 (API 26) or newer. The current build is a debug build published for testing.

## Features

### Reading
- Opens TXT, HTML, EPUB, DOCX, RTF, XLSX, CSV, PPTX and PDF files, via the system file picker or "Open with" / Share from another app
- Document-aware pagination: EPUB chapters, PPTX slides and PDF pages keep their original boundaries
- Legacy binary Office formats (.doc, .xls, .ppt) are not supported

### Text-to-speech narration
- Choice of installed TTS engines, plus speech-rate and pitch controls
- Word-by-word highlighting that follows the narration on screen, on TTS engines that report the currently spoken text range; on engines without that support, playback is unaffected and highlighting doesn't appear
- Custom pronunciation rules (plain text or regular expressions, individually toggleable) applied only to the text handed to the speech engine - the on-screen text is never altered
- Sleep timer (5, 15, 30 or 60 minutes) that stops narration automatically, with an on-screen countdown

### On-device OCR for scanned PDFs
- Scanned pages are detected and can be recognized locally with Tesseract - recognition itself works fully offline
- Downloadable OCR language packs: English, Hindi, Spanish, French, German, Arabic, Chinese (Simplified) and Russian; internet is needed only for the one-time download
- Results are cached per document, page and language, so recognized pages don't have to be processed again when cached results are available

### Reading comfort
- In-document search with page numbers and context snippets, with jump-to-result
- Bookmarks and a recent-documents list with reading progress
- Optional content filters that strip running headers, footers and page-number lines
- Ambient background audio from your own files (nothing bundled) that ducks under the narration and restores afterwards
- Optional sound cues for page turns, bookmarks, OCR completion and sleep-timer end

### Audio export
- Export the current page or a whole document as an MP3 file, using the same content filters and pronunciation rules as live narration
- Runs as a cancellable background job with a progress notification, even if the reader screen is closed; share the result from the app

### Accessibility
- Built for TalkBack use: interactive controls carry content descriptions, decorative icons are silenced, and live regions announce page changes, search results, and OCR, export and sleep-timer progress
- Light and dark themes with explicit high-contrast colors

## Privacy

Based on inspection of the app's source code:
- No accounts, no ads, no analytics or tracking SDKs
- Works offline; the only network use in the app itself is downloading OCR language packs. (The TTS engine installed on your phone is a separate component and may use the network on its own.)
- Android permissions: Internet (OCR language downloads), Notifications and Foreground Service (audio export progress)

## Known limitations

- OCR runs one page at a time, on demand; batch OCR of a whole scanned document in one pass is not currently provided
- Content-filter changes apply to the next document opened, not the one currently open
- Word highlighting is skipped on pages where pronunciation rules changed the spoken text's length, because engine offsets would land on the wrong words
