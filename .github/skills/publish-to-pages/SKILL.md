---
name: publish-to-pages
description: 'Publish presentations and web content to GitHub Pages. Converts PPTX, PDF, HTML, or Google Slides to a live GitHub Pages URL. Handles repo creation, file conversion, Pages enablement, and returns the live URL. Use when the user wants to publish, deploy, or share a presentation or HTML file via GitHub Pages.'
---

# publish-to-pages

Publish any presentation or web content to GitHub Pages in one shot.

## 1. Prerequisites Check

Run these silently. Only surface errors:

```bash
command -v gh >/dev/null || echo "MISSING: gh CLI — install from https://cli.github.com"
gh auth status &>/dev/null || echo "MISSING: gh not authenticated — run 'gh auth login'"
```

## 2. Input Detection

Determine input type from what the user provides:

| Input | Detection |
|-------|-----------|
| HTML file | Extension `.html` or `.htm` |
| PPTX file | Extension `.pptx` |
| PDF file | Extension `.pdf` |
| Google Slides URL | URL contains `docs.google.com/presentation` |

Ask the user for a **repo name** if not provided. Default: filename without extension.

## 3. Conversion

### HTML
No conversion needed. Use the file directly as `index.html`.

### PPTX
Run the conversion script:
```bash
python3 SKILL_DIR/scripts/convert-pptx.py INPUT_FILE /tmp/output.html
```
If `python-pptx` is missing, tell the user: `pip install python-pptx`

### PDF
Convert with included script (requires `poppler-utils` for `pdftoppm`):
```bash
python3 SKILL_DIR/scripts/convert-pdf.py INPUT_FILE /tmp/output.html
```

### Google Slides
1. Extract the presentation ID from the URL
2. Download as PPTX:
```bash
curl -L "https://docs.google.com/presentation/d/PRESENTATION_ID/export/pptx" -o /tmp/slides.pptx
```
3. Then convert the PPTX using the convert script above.

## 4. Publishing

### Visibility
Repos are created **public** by default. If the user specifies `private`, use `--private` — but note that GitHub Pages on private repos requires a Pro, Team, or Enterprise plan.

### Publish
```bash
# Create repo
gh repo create REPO_NAME --public --description "Description"

# Clone and add files
gh repo clone USERNAME/REPO_NAME /tmp/repo
cp /path/to/index.html /tmp/repo/index.html
cd /tmp/repo
git add .
git commit -m "Initial publish"
git push

# Enable GitHub Pages
gh api repos/USERNAME/REPO_NAME/pages -X POST -f source.branch=main -f source.path=/
```

## 5. Output

Tell the user:
- **Repository:** `https://github.com/USERNAME/REPO_NAME`
- **Live URL:** `https://USERNAME.github.io/REPO_NAME/`
- **Note:** Pages takes 1-2 minutes to go live.

## Error Handling

- **Repo already exists:** Suggest appending a number (`my-slides-2`) or a date (`my-slides-2026`).
- **Pages enablement fails:** Still return the repo URL. User can enable Pages manually in repo Settings.
- **PPTX conversion fails:** Tell user to run `pip install python-pptx`.
- **PDF conversion fails:** Suggest installing `poppler-utils`.
- **Google Slides download fails:** The presentation may not be publicly accessible.
