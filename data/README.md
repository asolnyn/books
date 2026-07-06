# How the data files work

Every book now has its own file, so editing one book can never break
another — if you make a mistake in one book's file, the website just
skips that book and keeps showing everyone else normally.

## The structure
```
data/
  manifest.json          <- list of which books exist
  books/
    AP-01.json            <- everything about book AP-01
    AP-02.json            <- everything about book AP-02
    AP-03.json            <- everything about book AP-03
```

## manifest.json
A simple list of reference codes, in the order you want them checked:
```json
[
  "AP-01",
  "AP-02",
  "AP-03"
]
```

## Each book file (e.g. data/books/AP-01.json)
Contains everything about that one book:
- `title`, `type` (genre — also powers the filter chips), `price`
- `whatsapp` — a book-specific WhatsApp number for its Buy button
  (leave `""` to use the site's default number instead)
- `cover` — path to the cover image, e.g. `"covers/AP-01.jpg"`
  (leave `""` to show the placeholder instead)
- `dates` — published / started / ended / edited, format `"DD-MM-YYYY"`
  (leave any of these as `""` if unknown — it just won't be shown)
- `description.short` — the blurb shown in the book list
- `description.full` — the longer text shown in the preview/details view
- `description.excerpt` — the sample text shown on the "আংশিক পড়ুন"
  (Read excerpt) screen
- `description.pages`, `description.chapters` — shown in the details
  view (`0` hides them)
- `description.sold` — copies sold, shown as "Sold copies: X"
- `description.continuous` — `true` for an ongoing/continuing series,
  `false` for a complete standalone book

## Adding a brand new book
1. Pick the next reference code, e.g. `"AP-04"`
2. Add `"AP-04"` to the list in `manifest.json`
3. Create a new file `data/books/AP-04.json` — easiest way is to copy
   an existing book's file's content, paste it into the new file, then
   edit the text inside
4. Optionally upload a cover to `covers/AP-04.jpg` and set `"cover"`
   to match

## Adding a cover
1. Upload the image to a `covers` folder in your repo (same level as
   `data`), e.g. `covers/AP-04.jpg`
2. Set `"cover": "covers/AP-04.jpg"` inside that book's own file

## Genre filter chips (গল্প, কবিতা, উপন্যাস, etc.)
The chips above the book list are generated automatically from each
book's `"type"` field — you don't edit the chips directly. Reuse the
exact same `type.bn` value across books that share a genre so they
group under the same chip. For example:
```json
"type": { "bn": "কবিতা", "en": "Poetry" }
```

## If something looks wrong
Open your browser's developer tools / console (or ask Claude to check
the live JSON files) — if one book's file has a typo (like a missing
comma), the console will show exactly which reference code failed to
load, while every other book keeps working normally.

## Note on previewing
These files only load correctly when served from a real web address
(like GitHub Pages), since the site fetches them as separate files.
Opening `index.html` directly on your phone without uploading
everything together won't load any book data — always test on the
live GitHub Pages link.
