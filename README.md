# CNeuromod Mario: a large-scale longitudinal fMRI dataset of naturalistic videogame play

Source of the *mario* / *mariostars* data descriptor, intended for *Scientific Data*. The
analyses and figures come from [`mario_fmri`](https://github.com/courtois-neuromod/mario_fmri).

The manuscript exists in two forms, kept in the same repository:

| Form | Entry point | Used for |
|---|---|---|
| LaTeX | `main.tex` (repository root) | Journal submission; import this repo into Overleaf |
| MyST Markdown | `myst.yml`, `paper/*.md` | Web version, built with [Jupyter Book v2](https://next.jupyterbook.org), same setup as [`cneuromod.paper`](https://github.com/courtois-neuromod/cneuromod.paper) |

Both read the same `references.bib` and `figures/`. The text is **not** generated from one to the
other: an edit to one must be carried over to the other by hand. Section mapping:

| `main.tex` section | MyST file |
|---|---|
| Title, authors, affiliations | `paper/index.md` (+ `authors` in `myst.yml`) |
| Abstract, Background & Summary | `paper/background.md` |
| Methods (incl. Code availability) | `paper/methods.md` |
| Data Records (Table 1, Figure 1) | `paper/data_records.md` |
| Technical Validation (Figures 2–3) | `paper/technical_validation.md` |
| Usage Notes | `paper/usage_notes.md` |
| Acknowledgements, Author contributions, Competing interests, Data Citations | `paper/acknowledgements.md` |

## Figures

See [`figures/README.md`](figures/README.md): generate them with `mario_fmri` (`invoke paper.*`)
and place the PDF + PNG of each figure in `figures/`.

## LaTeX / Overleaf

On Overleaf, *New Project → Import from GitHub* and pick this repository; `main.tex` is the main
document. It uses the `arxiv.sty` preprint style (MIT, see `arxiv-sty-LICENSE.txt`) with natbib
numbered superscript citations. Locally:

```bash
latexmk -pdf main.tex
```

## MyST web version

Install dependencies with [uv](https://docs.astral.sh/uv/):

```bash
uv sync
```

Preview with live reload:

```bash
uv run jupyter book start
```

Build the static site (`_build/html/`) or the PDF (`exports/`):

```bash
uv run jupyter book build --html
uv run jupyter book build --pdf
```

Pushing to `main` deploys the HTML site to GitHub Pages
(`.github/workflows/deploy.yml`; Pages source must be set to *GitHub Actions*).

## Project structure

| File / Folder | Description |
|---|---|
| `main.tex` | LaTeX manuscript (Scientific Data section order) |
| `arxiv.sty`, `orcid.pdf` | LaTeX style and ORCID logo |
| `references.bib` | BibTeX references, shared by LaTeX and MyST |
| `figures/` | Paper figures produced by `mario_fmri` |
| `myst.yml` | MyST configuration, table of contents and PDF export |
| `paper/` | MyST sections |
| `references.mjs`, `site.css` | Single reference list on the References page (from `cneuromod.paper`) |
