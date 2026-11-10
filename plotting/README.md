# Plotting

This directory contains plotting code and the shared Matplotlib style for the
thesis. Generated figures belong in the matching folder under [`../figures/`](../figures/):

```text
plotting/scripts/01-introduction/   -> figures/introduction/
plotting/scripts/02-chapter-name/   -> figures/chapter-02/
plotting/scripts/appendix-a/        -> figures/appendix-a/
```

The output folders are deliberately separate from plotting code, so figures can
be included directly from the LaTeX sources without copying them manually.

## Defaults

Use the style file at the start of every plotting script:

```python
from pathlib import Path
import matplotlib.pyplot as plt

ROOT = Path(__file__).resolve().parents[2]
FIGURES = ROOT / "figures" / "introduction"

plt.style.use(ROOT / "plotting" / "styles" / "thesis.mplstyle")

# ... create the plot ...
fig.savefig(FIGURES / "example.pdf")
fig.savefig(FIGURES / "example.png")
```

The default canvas is 6.69 x 3.5 inches at 400 dpi. Plot labels use 11 pt,
matching the thesis body text; tick labels use 9.5 pt for readability. Use the
same palette in plot-specific styling: TU Delft blue `#00A6D6`, dark blue
`#003082`, cyan `#00B5E2`, and black `#000000`.

Prefer PDF for vector figures in the thesis and PNG for quick previews. Keep
one plot per file and use descriptive, stable filenames so LaTeX references do
not break when scripts are rerun.
