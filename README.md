# ENA-LS (Location-based Services)

Course repository for ENA-LS course

## Build the Project Proposal Doc

Requires XeLaTeX and `latexmk`, plus the LaTeX packages used by the source and the Latin Modern fonts. These can be provided by a TeX Live installation.

From the repository root:

```sh
cd proj/proposal
latexmk -xelatex -interaction=nonstopmode -halt-on-error -file-line-error -outdir=build main.tex
```

The PDF is generated at `proj/proposal/build/main.pdf`. Build outputs are ignored by Git and must be generated locally.
