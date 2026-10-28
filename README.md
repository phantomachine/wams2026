# WAMS2026 — workshop program

**GitHub Pages:** serve from branch `main`, folder **`/docs`** (Settings → Pages).
`docs/` holds the public web build (HTML as `index.html`, PDF, ePUB) **without participants' e-mail addresses**.
Everything outside `docs/` is the full working version (includes e-mails) and is not served by Pages.
Public build: `cd build && python3 build.py ../../data --no-emails` (run on a copy, then copy the three outputs into `docs/`).

## Generated outputs

| File | What it is |
|---|---|
| `WAMS2026-program.pdf` | Program booklet (compiled from `latex/`) |
| `WAMS2026-program.html` | Self-contained HTML version (built from `markdown/`) |
| `WAMS2026-program.epub` | ePUB version (built from `markdown/`) |
| `latex/WAMS2026-program.tex` | Main LaTeX file; section files in `latex/sections/`, figures in `latex/figures/` |
| `markdown/WAMS2026-program.md` | Markdown source (+ `style.css`, `figures/`) |
| `build/` | Generator: `wams_data.py` (data fixes, metadata, session allocation), `build.py`, `schedule-checks.txt` |

Rebuild everything (needs python3 + openpyxl, matplotlib, geopandas; xelatex/latexmk; pandoc ≥ 3):

    cd build && python3 build.py ../../data

Recompile only the PDF:  `cd latex && latexmk -xelatex WAMS2026-program.tex`
Only HTML/ePUB from the Markdown (pandoc 2.x: replace `--embed-resources` with `--self-contained`):

    cd markdown
    pandoc WAMS2026-program.md -s --toc --toc-depth=2 --mathml --css style.css --embed-resources -o ../WAMS2026-program.html
    pandoc WAMS2026-program.md --toc --toc-depth=2 --mathml --css style.css -o ../WAMS2026-program.epub

To move a paper, edit `SESSIONS` in `build/wams_data.py` and rebuild — the scheduling restrictions
(Okada not 21 Nov, Chowdhury not 20 Nov, Mantovani/Ptashkina on different days, no person needed in two rooms at once)
are re-checked automatically and the build stops if one is violated.
