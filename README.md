# CV

LaTeX CV with automated build and GitHub Pages hosting.

**Share this**: <https://alex-krasnoshtanov.github.io/CV/> — landing page, with a preview card for LinkedIn/Slack
**Direct PDF**: <https://alex-krasnoshtanov.github.io/CV/resume.pdf> — unchanged, still the raw file

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
- `site/index.html` -- landing page served at `/CV/`; `BUILD_DATE` is substituted at build time
- `.github/workflows/build.yml` -- auto-compile + deploy

## Why there is a landing page and not just the PDF

Link a bare `.pdf` on LinkedIn and it renders as a plain text link: a PDF carries
no Open Graph metadata, so there is no title, description or thumbnail to show.
The landing page supplies those, and its `og:image` is regenerated from page 1 of
the PDF on every build, so the preview never drifts from the actual CV.

The embedded viewer is deliberately desktop-only. Mobile browsers -- iOS Safari,
and the in-app browser LinkedIn opens links in -- will not render a PDF inside an
`<iframe>` or `<object>`; they paint an empty box. On small screens the page shows
the buttons instead, which work everywhere.

Nothing about this changes `resume.pdf`. It stays at the same URL and anyone who
already links straight to it is unaffected.
