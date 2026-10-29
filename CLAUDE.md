# mario_fmri.paper

Data descriptor for the CNeuroMod *mario* / *mariostars* datasets (Scientific Data).

- Two hand-synced manuscript sources: `main.tex` (Overleaf/submission) and `paper/*.md` (MyST,
  Jupyter Book v2). Any text change goes into both; the mapping is in `README.md`.
- `references.bib` and `figures/` are shared. Citation keys must exist in `references.bib`.
- Figures and every reported number come from `mario_fmri` (`invoke paper.*`, `invoke paper.stats`);
  do not invent or recompute them here.
- MyST: `uv run jupyter book build --html` (CLI is `jupyter book`, with a space). Use
  `{cite:p}` for citations and `{numref}` with the `fig-*` / `tab-*` labels for cross-references.
- `main.tex` must stay compilable on Overleaf: no shell-escape, no local-only packages.
