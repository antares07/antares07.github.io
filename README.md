# Personal academic website

A one-page research homepage with a downloadable CV. The CV is written in
LaTeX (`cv/cv.tex`) and compiled automatically by GitHub Actions on every
push, so the PDF on the site always matches the source.

```
index.html                    the homepage (all styles are inside this file)
assets/background.jpg         the hero background image
assets/photo.jpg              your photo (add it yourself, see below)
assets/favicon.svg            browser tab icon
cv/cv.tex                     your CV in LaTeX
.github/workflows/deploy.yml  builds cv.pdf and publishes the site
.nojekyll                     tells GitHub not to process the site with Jekyll
```

## Publish it

1. Create a **public** repository named `<your-username>.github.io`.
2. Push this folder's **contents** (not the folder itself) to the `main`
   branch, so `index.html` sits at the top of the repository:

   ```bash
   cd academic-site
   git init -b main
   git add .
   git commit -m "First version of my site"
   git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
   git push -u origin main
   ```

   If you upload through the GitHub website instead, drag the folders in
   rather than selecting files one by one; selecting files flattens the
   folders and the images stop loading. Hidden items (`.github`, `.nojekyll`)
   are easy to miss this way, so the command line is safer.
3. **Settings → Pages → Source: GitHub Actions.** This is required for the
   CV to be built. With "Deploy from a branch" the page shows but `cv.pdf`
   does not exist.
4. Open the **Actions** tab and wait for "Build CV and deploy site" to turn
   green (a couple of minutes). If it failed earlier, click **Run workflow**.

## Personalise it

- **Photo:** save a square photo (at least 400 × 400 px) as `assets/photo.jpg`.
  Until that file exists, your initial is shown in the circle.
- **Background:** replace `assets/background.jpg` with any wide image
  (about 2400 × 1400 px). Keep the main subject on the right; the left side
  is darkened for the text. If you use a NASA/ESA/ESO image, add the credit
  in the footer of `index.html`.
- **Text:** edit `index.html`. Search for "Laro", "Author", "Title of" and
  "conference name" to find the placeholders.
- **A new paper:** copy one `<li class="pub">` block into the right year and
  set `data-type` to `journal`, `conference` or `preprint`.
- **The CV:** edit `cv/cv.tex` and push. The workflow rebuilds `cv.pdf`.

## If something looks wrong

- **No styling at all:** the styles are inside `index.html`, so this means
  the browser is showing an old version. Wait for the Actions run to finish,
  then hard-refresh (Ctrl+Shift+R, or Cmd+Shift+R on a Mac).
- **No background image or photo:** check that `assets/` exists in the
  repository with exactly these lowercase names. GitHub Pages is
  case-sensitive, so `Photo.JPG` will not match `photo.jpg`.
- **The README shows instead of the site:** `index.html` is inside a
  subfolder. Move the contents up to the top of the repository.

## Preview locally

Run `python3 -m http.server` in this folder and open http://localhost:8000.
To test the CV link locally, compile the CV and copy it next to `index.html`:

```bash
cd cv && pdflatex cv.tex && cp cv.pdf ../cv.pdf
```
