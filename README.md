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

## Abbreviations and symbols

Define each abbreviation or symbol in
[`frontmatter/abbreviations.tex`](frontmatter/abbreviations.tex), for example:

```latex
\acro{PEM}{Proton Exchange Membrane}
\acro{speed}[v]{Velocity}
```

Use the acronym commands in chapter text:

```latex
\ac{PEM}  % writes "Proton Exchange Membrane (PEM)" on first use
\acs{PEM} % writes only the short form: PEM
\acl{PEM} % writes only the long form: Proton Exchange Membrane
```

Only abbreviations or symbols used with `\ac`, `\acs`, `\acf`, or `\acl` are
expanded according to the acronym package rules. The list is printed in the
front matter even when an entry has not yet been used.

## Figures and tables

Every standard LaTeX `figure` or `table` environment with a `\caption` is
added automatically to the List of Figures or List of Tables. A short example
is:

```latex
\begin{figure}[htbp]
  \centering
  \includegraphics[width=.8\textwidth]{figures/chapter-02/example.pdf}
  \caption{An informative figure caption.}
  \label{fig:example}
\end{figure}

\begin{table}[htbp]
  \centering
  \caption{An informative table caption.}
  \label{tab:example}
  \begin{tabular}{ll}
    \toprule
    Parameter & Value \\
    \midrule
    Example & 1 \\
    \bottomrule
  \end{tabular}
\end{table}
```

Place the `\label` after the `\caption` for both environments. Refer to them
with `Figure~\ref{fig:example}` or `Table~\ref{tab:example}`. Use the
project-wide Matplotlib style for generated plots and keep source assets under
`plotting/scripts/<chapter>/` and output assets under `figures/<chapter>/`.

## Visual consistency

The colour names in [`latex/thesis-colors.sty`](latex/thesis-colors.sty) and
the hex values in [`plotting/styles/thesis.mplstyle`](plotting/styles/thesis.mplstyle)
are intentionally kept in sync. Use the Matplotlib style in every plotting
script so figure dimensions, line widths, colours, and text sizes remain
consistent with the document.
