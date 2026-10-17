# Sowing Discord — project website

Static website for the IEEE S&P 2027 paper
**"Sowing Discord: Exploiting the Lack of Key Commitment in E2EE Group RTC"**.

Plain HTML / CSS / a little JS. No build step, no external CDN, no analytics.

## Local preview

```sh
python3 -m http.server 8000
# open http://localhost:8000/
```

## Structure

```
index.html            single-page site; sections are delimited by
                      <!-- ===== SECTION: name ===== --> comments
assets/css/style.css  colors / fonts / spacing via :root variables (dark mode included)
assets/js/main.js     nav toggle, nav highlight, BibTeX copy
assets/img/           logo.svg, favicon.svg, og-image.png, phase1.svg / phase2.svg (redrawn from phase1.pdf / phase2.pdf)
assets/video/         PoC.mp4 (web version) + PoC-poster.jpg
.nojekyll             disables Jekyll on GitHub Pages
```

## Content rules

- Facts must come from the paper only. Do not write that Discord or Linphone have "fixed" the issue.
- Do not use Discord's logo, mascot, Blurple (#5865F2) or wordmark. The site uses a black + cyan-leaning blue base instead. No non-affiliation notice in the footer (author decision).
- Do not embed attack code; link to the artifact only.
- The site covers the Discord (DAVE) attack (plus Linphone where relevant). Other surveyed apps are not mentioned.

## Before the S&P publication

`paper.pdf` is published (Paper button in the hero, PDF link in `#paper`). BibTeX and the DOI are
**not** published yet; the BibTeX part of `#paper` is a placeholder.

## Common updates


- **Update the paper**: overwrite `paper.pdf`.
- **Add BibTeX / DOI**: update `CITATION.bib` and the `<pre>` in `#paper` so both match.
- **Add news**: add an item at the top of the `#news` section.
- **Update vendor status**: edit the timeline / status list in `#ethics` (Disclosure timeline) and update "Last updated".
- **Edit the FAQ**: each question is a `<details>` block in `#faq`. Keep answers to 1–3 sentences.
- **Add author homepage**: in `#authors`, wrap the name: `<p class="author-name"><a href="https://...">Name</a></p>`.
- **Change the public URL** (e.g., when moving to a custom domain): in `<head>` update the `canonical` link, `og:url`,
  `og:image` and `twitter:image` (all absolute URLs). For a custom domain, set up DNS **first**, then add a `CNAME`
  file and the domain in Settings → Pages — otherwise the github.io URL redirects to a domain that does not work.
- **Replace the video**: overwrite `assets/video/PoC.mp4` (keep < 50 MB) and regenerate the poster:
  `ffmpeg -ss 2 -i assets/video/PoC.mp4 -frames:v 1 -q:v 3 assets/video/PoC-poster.jpg`

- **Update the Discord user number**: edit the sentence in `#discord` and the source note in the HTML comment above it (the number is not from the paper; the source is kept only in the comment).
- **Edit a phase figure**: `assets/img/phase1.svg` / `phase2.svg` are hand-written SVGs (640×280, dark background `#12161e`) redrawn from the authors' PDFs; edit the text/coordinates directly. Note: XML comments must not contain `--`. After editing, bump the `?v=` number on both the `<img src>` and the `<a href>` in index.html so browsers reload the figure.

## Deployment

GitHub Pages (repository `HayatoYamashita/sowing-discord`): Settings → Pages → Deploy from a branch → `main` / `(root)`.
Public URL: https://hayatoyamashita.github.io/sowing-discord/ (no custom domain yet). Pushing to `main` redeploys the site.
The publication timing is decided by the authors.
