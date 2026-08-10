# jacoblefler.github.io

Personal site at <https://jacoblefler.github.io>. Plain HTML and CSS — no Hugo, no
Jekyll, no theme, no build step.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The entire site. Edit this to change any text. |
| `style.css` | All styling. Colors live in the `:root` block at the top. |
| `cv.tex` | CV source. |
| `cv.pdf` | Built CV, served at `/cv.pdf`. Commit it after rebuilding. |
| `assets/` | Profile photo and favicon. |

## Editing the site

Open `index.html`, change the text, save. To preview before pushing, just open
`index.html` in a browser — double-click it, or:

```bash
start index.html
```

The site is entirely static with relative paths, so opening the file directly renders
exactly what gets published. If you'd rather serve it over HTTP (closer to the real
thing, and needed if you ever add anything that fetches):

```bash
npx --yes serve .
```

## Rebuilding the CV

Edit `cv.tex`, then:

```bash
latexmk -pdf cv.tex
```

Each section is one `\cvsection{Label}{Body}` call. To add a section, copy an existing
block. Inside a body, `\dated{what}{when}` puts a date flush against the right margin.
A few extra sections (grants, talks, refereeing, languages) are commented out at the
bottom of the file, ready to uncomment.

Build artifacts (`.aux`, `.log`, `.fls`, …) are gitignored — only `cv.tex` and `cv.pdf`
get committed.

## Publishing

Push to `master`. A GitHub Action (`.github/workflows/deploy.yml`) uploads the repo and
publishes it; the site is live in under a minute.

```bash
git add -A
git commit -m "describe the change"
git push origin master
```

Note the branch is `master`, not `main`.

## Adding a paper

Drop the PDF in the repo root and wrap the title in `index.html`:

```html
<a href="the-paper.pdf" target="_blank">Freight in the Time of Covid: A Model of US Trucking</a>
```

Anything committed here is publicly downloadable once pushed, whether or not the site
links to it.
