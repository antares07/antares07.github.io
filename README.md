# Personal academic website

A one-page research homepage with a downloadable CV. The CV is written in
LaTeX (`cv/cv.tex`) and compiled automatically by GitHub Actions on every
push, so the PDF on the site always matches the source.

```
index.html                    the homepage
assets/style.css              colours, fonts and layout
assets/favicon.svg            browser tab icon (edit the initials)
cv/cv.tex                     your CV in LaTeX
.github/workflows/deploy.yml  builds cv.pdf and publishes the site
```

## Publish it

1. Create a new **public** repository on GitHub named
   `<your-username>.github.io`. With that exact name the site lives at
   `https://<your-username>.github.io`. Any other name works too, but the
   address becomes `https://<your-username>.github.io/<repo-name>`.
2. Upload these files, keeping the folder structure (including the hidden
   `.github` folder), to the `main` branch. From a terminal:

   ```bash
   cd academic-site
   git init -b main
   git add .
   git commit -m "First version of my site"
   git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
   git push -u origin main
   ```

3. In the repository, go to **Settings → Pages** and set **Source** to
   **GitHub Actions**.
4. Open the **Actions** tab. The "Build CV and deploy site" run takes a couple
   of minutes. If it ran before you changed the setting and failed, use
   **Run workflow** to start it again.

## Update it

- **Your details:** edit the text in `index.html` (name, bio, links,
  publications, news) and `cv/cv.tex`. Search for "Jane Doe", "example" and
  "janedoe" to find every placeholder.
- **A new paper:** copy one `<li class="pub">` block into the right year in
  `index.html`. Set `data-type` to `conference`, `journal` or `preprint` so the
  filter buttons pick it up.
- **A photo:** add `assets/portrait.jpg` and uncomment the `<img>` line near
  the top of `index.html`.
- **The CV:** edit `cv/cv.tex` and push. The workflow rebuilds `cv.pdf`.

## Preview locally

Run `python3 -m http.server` in this folder and open http://localhost:8000.
The **Download CV** link works locally only after you compile the CV and copy
it next to `index.html`:

```bash
cd cv && pdflatex cv.tex && cp cv.pdf ../cv.pdf
```

(`cv.pdf` in the top folder is only for local previews. The live site uses the
one the workflow builds.)
