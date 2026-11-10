# Master thesis

This repository contains the TU Delft LaTeX source for the master thesis.
`report.tex` is the only build entry point; all content is organised below it
by document role.

## Repository structure

```text
report.tex                 Main document and chapter order
frontmatter/               Cover, title page, and preface
chapters/                  Numbered thesis chapters
appendices/                Appendices
references/                BibLaTeX databases
figures/                   Generated figures, grouped by chapter
plotting/                  Plot scripts and shared Matplotlib defaults
latex/                     Project-local LaTeX packages
-texmf/                    TU Delft report class and template dependencies
```

Keep plot sources in `plotting/scripts/<chapter>/` and save their output
directly into the corresponding `figures/<chapter>/` directory. See
[`plotting/README.md`](plotting/README.md) for a complete example.

## Building

From the repository root, build with:

```sh
latexmk report.tex
```

The existing [`latexmkrc`](latexmkrc) keeps the project compatible with both
LuaLaTeX and pdfLaTeX, and configures Biber for the bibliography. The TU Delft
class is provided locally through `-texmf/`, so the project does not depend on
a globally installed copy of that class.

Before submitting, replace the template metadata in
[`frontmatter/cover.tex`](frontmatter/cover.tex) and
[`frontmatter/title.tex`](frontmatter/title.tex), remove placeholder chapter
content, and update the chapter list in [`report.tex`](report.tex).

## Visual consistency

The colour names in [`latex/thesis-colors.sty`](latex/thesis-colors.sty) and
the hex values in [`plotting/styles/thesis.mplstyle`](plotting/styles/thesis.mplstyle)
are intentionally kept in sync. Use the Matplotlib style in every plotting
script so figure dimensions, line widths, colours, and text sizes remain
consistent with the document.
