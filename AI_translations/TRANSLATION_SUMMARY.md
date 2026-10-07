# Translation Summary – manual.pdf → manual_translated.md

## Source
- `manual.pdf` – 97 pages, Mooney M20G "Statesman" (S/N 680001 and
  subsequent, D‑LCP), German "Flughandbuch" Edition 1 (Ausgabe 1)
  translated by AGRO, plus four English FAA/EASA/DAEC/JPI supplement
  appendices.
- Scan‑only PDF (no embedded text).

## Method
1. Rendered every page with PyMuPDF at 1.8× zoom → `imgs/page_001.png` …
   (dark scan on page 2 and some low‑quality pages re‑rendered at 2.2×).
2. OCR with the Tesseract 5.5.3 AppImage (`deu+eng` combined language
   model), one page at a time, output in `ocr_output/`.
3. Read all 97 OCR results, classified each page German/English by
   keyword frequency, translated every German page into English, kept the
   four English appendix pages (77–79, 93–97) as OCR'd text.
4. Assembled `manual_translated.md` with one `## Page N` section per PDF
   page; German headings/tables reconstructed as markdown lists.

Main technical trade-offs:
- Tesseract `deu+eng` mis‑separates umlauts and capitalization
  (`iort` instead of *gehört*, etc.); translations are based on reading
  the intended German, not a strictly literal word‑by‑word render.
- Charts / figures cannot be OCR'd as text: values inside charts are
  noted but flagged where confidence is low.
- Page 2 (dark scan) produced only the title line; annotated accordingly.

## Pages with poor / incomplete OCR
| PDF page | Reason |
|----------|--------|
| 2        | Dark/blank scan – only the title line (*Flughandbuch Mooney M20G, S/N 680001…*) recovered. |
| 8        | Full‑page dimension drawing (ABMESSUNGEN); only the heading and a few dimension numbers (2.44 m, 1.81 m) legible. |
| 15        | Almost entirely a diagram; only a table fragment ("3‑6 bis 3‑8") recovered. |
| 25        | Pre‑flight‑control diagram page; no legible body text found. |
| 26        | Full‑page diagram "Diagram: Vorflugkontrolle"; only the heading legible. |
| 43–46     | Chart pages (takeoff/landing distance, climb, AIRSPEED CORRECTION, STALL SPEEDS). Charts/numbers mostly lost; only titles and a handful of numbers recovered. |
| 49–53     | Performance tables at 0/2500/5000/7500/10000 ft – only a few numeric cells legible; the rest of the tables are not reproducible. Page 49 has a few legible rows (27.06/164 …), page 53 likewise. |
| 58        | Form page with mostly handwritten entries; only the header rows ("Benzin (voll)", "Gewichtige… / Abzüge" etc.) legible. |
| 60–62     | Weight & balance forms, some physically rotated 90° in the scan; values are stored upside‑down and only partially recoverable. Tables reconstructed approximately, flagged. |
| 63–67     | Handwritten weight‑report forms (billed to D‑LCP / S/N 680070, 28.09.17 install of EDM, 24.05.18 weight report). Most numeric entries are handwritten in a small calligraphy that OCR cannot read reliably; the printed‑form headings are preserved. |
| 75        | Full‑page drawing of the control‑yoke lever assembly. Only engraving labels (Autopilot / Trimknopf / GEAR HANDLE / SAFETY LATCH RELEASE LEVER / WING FLAP) recovered from the scan. |
| 88        | Two small line‑drawings (jacking eye; tank dump valve); only the captions legible. |

Everything else was extracted and translated.

## Output files
- `manual_translated.md` – the full English/annotated edition
  (97 page‑numbered sections, ~2,450 lines).
- `ocr_output/page_NNN.txt` – raw OCR results, kept for cross‑checking.
- `imgs/page_NNN.png` – rendered page images (1.8×), kept for re‑OCR or
  visual inspection of the flagged pages.
