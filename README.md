# How the data files work 

Your website reads book info from 4 files in this `data` folder instead of
the HTML itself. Every book has a reference code (like "AP-01") that links
its entry across all 4 files — always use the same code in each file for
the same book.

## 1. books.json
Core info: title (bn/en), type/genre (bn/en), price, and a WhatsApp number
for that specific book's Buy button (leave "whatsapp": "" to use the site's
default number instead).

`"order"` controls the position when sorting by "Author's order".

## 2. dates.json
Published / started / ended / edited dates, format "DD-MM-YYYY".
Leave any value as "" if you don't know it yet — it just won't be shown.

## 3. descriptions.json
- `short` — the blurb shown in the book list
- `full` — the longer description shown when someone taps the book/cover
- `pages`, `chapters` — shown in the full view (0 = hidden)
- `sold` — copies sold, shown as "Sold copies: X"

## 4. covers.json
Maps a reference code to an image path, e.g.:
```json
{
  "AP-01": "covers/AP-01.jpg"
}
```
To add a cover:
1. Create a `covers` folder in your repo (same level as `data`)
2. Upload your image there, e.g. `covers/AP-01.jpg`
3. Add the line above to `covers.json` with the matching reference code
4. Books with no entry in this file automatically show a placeholder

## Adding a brand new book
1. Pick the next reference code, e.g. `"AP-04"`
2. Add one block to `books.json`
3. Add one block to `dates.json` (or leave dates blank)
4. Add one block to `descriptions.json`
5. Optionally add a line to `covers.json`

That's it — the website rebuilds the list automatically from these files.

## Note on previewing
These files only load correctly when served from a real web address
(like GitHub Pages) because the site fetches them as separate files.
Opening `index.html` directly on your phone without uploading everything
together won't load the book data — always test on the live GitHub Pages
link.
