# HAL report — SENG 4130 (Fall 2026)

`main.tex` follows `ignored/report-template.docx`, with prompts tailored to the
smart-home project in `ignored/project.pdf`. The original university logo and
LaTeX formatting are retained. Italic grey text and framed diagrams are placeholders.

For deliverable one (October 6), fill in Introduction, Problem Definition and
Scope, Design Requirements, and the initial UML design under Solution. The
remaining chapters support later deliverables; they are not claims of completed work.
Replace the two team-member placeholders and submission date before submission.

The Word template includes Solution 3 in its body but omits it from its sample
table of contents. This template includes it as an optional section.

## Build

From this directory, run:

```bash
latexmk -pdf main.tex
```

The PDF is written to `build/main.pdf`. The table of contents and lists of figures
and tables update automatically. In VS Code, use LaTeX Workshop with the existing
workspace settings, which also direct output to `report/build/`.

## References

Add project sources to `references.bib`, cite them with `\cite{key}`, and change
`\reportreferencesfalse` to `\reportreferencestrue` in the preamble. Then rebuild
with latexmk to generate the numbered References chapter in IEEE style. Until
sources are cited, the report displays an instructional placeholder.

## Requirements

A LaTeX distribution with the packages used in `main.tex`, BibTeX, and latexmk.
On Ubuntu, `texlive-latex-extra`, `texlive-fonts-recommended`, and `latexmk`
provide the required tools and fonts.
