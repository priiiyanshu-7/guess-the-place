# guess the spot

A five-question quiz about places that recently opened in Bangalore. You get a photo and a written clue for each one, pick from four options, and see a short write-up of the real place either way.

Built as a shareable link for [glide](https://justglide.ai).

**Play it: <https://priiiyanshu-7.github.io/guess-the-place/>**

## Running it

It's a single self-contained HTML file — no build step, no dependencies.

```
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

Opening the file directly with `file://` mostly works too, but serving it over HTTP is closer to production for the `history.pushState` navigation between questions.

## Structure

Everything lives in `index.html`:

- **`SPOTS`** — the question data. One object per place: `img` (base64 JPEG), `emoji`, `clue`, `options`, `answer` (index into `options`), `name`, `blurb`, `get` and `where`. Add or reorder entries and the rest of the UI follows.
- **`LINKS`** — App Store and Play Store URLs for the download buttons. Both are currently empty, so every tap falls back to the website; fill them in to deep-link per platform.
- The quiz state is three variables (`picked`, `i`, `ended`) driven through `history.pushState`, so the browser back button steps back through questions.

The photos are inlined as base64, which keeps the file portable at the cost of size — it's around 715 KB.
