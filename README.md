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
- `site/index.html` -- the page served at `/CV/`; copied verbatim at build time
- `.github/workflows/build.yml` -- auto-compile + deploy

## Why there is a page at `/CV/` and not just the PDF

Link a bare `.pdf` on LinkedIn and it renders as a plain text link: a PDF carries
no Open Graph metadata, so there is no title, description or thumbnail to show.

The page exists only to supply that metadata. All of it sits in `<head>`, which a
reader never sees, so the page has no visible chrome at all -- the resume is the
entire content. `og:image` is regenerated from page 1 on every build and cannot
drift from the actual CV.

## What each viewport gets

Desktop (`min-width: 60rem` and a fine pointer) gets `resume.pdf` in an iframe
filling the viewport: real selectable text, and the browser's own download and
print controls rather than any of ours.

Phones get `page1.png` instead, full width. This is not a preference -- iOS
Safari and the in-app browsers LinkedIn opens links in refuse to render a PDF
inside an `<iframe>` or `<object>` and paint an empty box, so a viewer there would
be a blank screen. A rendered image always works and looks identical to the
document. A small pill in the bottom corner opens the real PDF; it is the only
element on the page that is not the resume, and it is hidden on desktop.

Both images are produced by `pdftoppm` during the build, and the build fails if
either comes out at unexpected dimensions -- which is what would happen if the
paper size in `resume.tex` ever changed without `index.html` being updated to
match.

The build also fails if `resume.pdf` is more than one page. Only page 1 is ever
rendered to an image, so on a phone a second page would simply not exist, with
nothing on screen to say so. Better to break the build than to publish half a
CV.

Nothing about this changes `resume.pdf`. It stays at the same URL and anyone who
already links straight to it is unaffected.
