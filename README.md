# CV

LaTeX CV with automated build and GitHub Pages hosting.

**Live PDF**: [https://gfgf96.github.io/cv/resume.pdf](https://gfgf96.github.io/cv/resume.pdf)

## How it works

Edit `cv/resume.tex`, push to `main` -- GitHub Actions compiles the PDF and deploys it to GitHub Pages automatically. The link above always points to the latest version.

## Local build

Requires MiKTeX or TeX Live:

```bash
cd cv
pdflatex resume.tex
```

Or just save in VS Code with LaTeX Workshop installed.

## Structure

- `cv/resume.tex` -- source file
- `.github/workflows/build.yml` -- auto-compile + deploy
