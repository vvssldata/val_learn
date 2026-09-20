# Study Trail (Val) — Project Notes

Live app: https://vvssldata.github.io/val_learn/
Repo: https://github.com/vvssldata/val_learn
Progress sheet (manual backup only, not yet auto-wired): https://docs.google.com/spreadsheets/d/1DW9Y2Ch7PPSZMKlaWDj_LEFoPTlo4EPWaHs973LYOXo/edit

Same engine as Victoria's Study Trail (`vvssldata/victoria_learn`), a single
self-contained `index.html`, retargeted for Val: 8th-grade **Language Arts**
and **Math** covering **Geometry** and **Algebra 2** (she's advanced —
normally a 9th/10th-grade math sequence).

Progress is stored in the browser's `localStorage` under its own key
(`studyTrailData_val_v1`, distinct from Victoria's site) — the two sites
share the `vvssldata.github.io` origin, so a shared/generic key would have
let their progress collide in the same browser.

## Curriculum (20 topics, 200 questions, all hand-verified)

**Language Arts** — Vocabulary, Reading Comprehension, Writing (4 topics
each), hand-authored at 8th-grade level: advanced context clues, Greek/Latin
roots, connotation/tone, figurative language, nonfiction analysis, rhetorical
appeals (ethos/pathos/logos), literary elements, synthesizing multiple
texts, thesis/argument structure, evidence & counterarguments, MLA citation
basics, style revision.

**Math** — Geometry (4 topics, hand-authored: angle relationships, triangle
congruence/similarity, Pythagorean theorem, circles) and Algebra 2 (4
topics, sourced from Kumon Level I/J worksheets in
`H:\my drive\kids_education_lower school\Math\Kumon\`: factoring quadratics,
solving quadratics, quadratic functions/graphing, exponent rules &
polynomial operations).

Kumon level mapping (confirmed by sampling the PDFs, which are scanned
images with no extractable text):
- G = pre-algebra (Victoria's level)
- H = Algebra 1
- **I = Algebra 2 core** (factoring, quadratic functions/graphs)
- J = Algebra 2 advanced / early pre-calc (polynomial/exponent operations,
  later exponential & log functions)
- K = Pre-calculus

Kumon has no dedicated proof-based Geometry course (only computational
area/volume, in G) — that's why Geometry here is hand-authored rather than
Kumon-sourced.

## Not yet done

- No `SHEET_PROGRESS_SEED` (no history exists yet — nothing to reconstruct).
- No "Writing Task" long-form topic yet (Victoria's site has one under
  Writing); can add the same way if wanted.

## Auto-save (2026-09-21)

`SAVE_URL` is wired to an Apps Script web app bound to the Val_LearnTracker
sheet:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([data.date, data.subject, data.area, data.topic, data.mode, data.score, data.minutes, data.status, data.notes]);
  return ContentService.createTextOutput(JSON.stringify({ok:true})).setMimeType(ContentService.MimeType.JSON);
}
```

Verified end-to-end with a labeled test POST (3 rows marked `TEST` /
"safe to delete this row" were left in the sheet during verification —
delete them next time you're in there).

## Commit history

- Initial commit: full 20-topic site (retargeted from victoria_learn)
- Wired up auto-save to the Google Sheet via Apps Script
