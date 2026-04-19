# leonardodcalves.github.io

Meu blog pessoal. Escrevo sobre o que eu quiser escrever.

**Site ao vivo:** [leonardodcalves.github.io](https://leonardodcalves.github.io)

## Sobre mim

Sou o Leonardo. Engenheiro Agrônomo, sul-mato-grossense, cozinheiro, fotógrafo, viajante, músico, e apaixonado por computadores.

## Sobre o site

Este blog é um site estático gerado por um pequeno script Python. Sem frameworks pesados, sem banco de dados, sem JavaScript rodando no cliente - apenas HTML, CSS, e alguns arquivos Markdown.

---

# Notes to self (maintenance)

This repository holds only the generated output — the HTML and CSS that GitHub Pages serves. The source files (the Python script, the Markdown posts, the stylesheet) live in a separate folder on my machine.

## Folder structure on my laptop

```
blog_py/
├── build.py      # generator script
├── style.css     # site style
├── posts/        # .md source files
├── images/       # image files (jpg, png, etc)
└── dist/         # build output — this is what gets uploaded here
```

## First-time setup

Install the dependency using `uv`:

```bash
uv pip install markdown
```

If you want to keep dependencies isolated in a virtual environment:

```bash
uv venv
uv pip install markdown
source .venv/bin/activate
```

## Workflow

### Adding or editing a post

1. Write or edit a post inside `posts/` as a `.md` file with front-matter:
   ```markdown
   ---
   title: "My Post Title"
   date: "2026-04-19"
   summary: "A short description for the homepage."
   tag: "optional-category"
   ---
   
   Your content here in **Markdown**.
   ```

2. Run the build script:
   ```bash
   uv run build.py
   ```
   (Or just `python3 build.py` if you're using the activated venv)

3. The `dist/` folder is automatically regenerated with fresh HTML files.

### Adding images to a post

1. Place your image file in the `images/` folder (create it if it doesn't exist):
   ```
   blog_py/
   └── images/
       └── my-photo.jpg
   ```

2. Reference it in your `.md` post using Markdown syntax:
   ```markdown
   ![alt text here](images/my-photo.jpg)
   ```

3. Run `uv run build.py` — the script automatically copies the `images/` folder into `dist/`.

4. When uploading to GitHub, make sure to include the `images/` folder from inside `dist/`.

### Adding an image to the About page

The About page is configured in `build.py` under `ABOUT_HTML`. Add an `<img>` tag:

```python
ABOUT_HTML = """
<img src="images/profile_picture.png" alt="Description" style="max-width: 200px; height: auto; border-radius: 8px; margin-bottom: 32px;">
<p>Your bio text here...</p>
"""
```

Then place your image in the `images/` folder and run `uv run build.py`.

## Publishing to GitHub

1. Run `uv run build.py` to regenerate everything.
2. Go to your repo: **Add file → Upload files**
3. Drag in **the entire contents of the `dist/` folder** (all `.html` files, `style.css`, and the `images/` folder)
4. Commit changes
5. Wait ~60 seconds, then hard-refresh your live site

## Site-wide configuration

All blog-wide settings live at the **top of `build.py`**, in the block marked:
```
# ═══════════════════════════════════════════════════════════════════════════
#  EDIT THIS SECTION TO CUSTOMIZE YOUR BLOG
# ═══════════════════════════════════════════════════════════════════════════
```

Edit:
- `SITE_TITLE` — your blog title
- `SITE_LOGO` — logo text in the header
- `HERO_LINE_1` & `HERO_LINE_2` — homepage headline
- `FOOTER_TEXT` — copyright footer
- `GITHUB_URL` — your GitHub profile link
- `ABOUT_TITLE` & `ABOUT_HTML` — your About page content

After editing, run `uv run build.py` to regenerate all pages.

## Important gotchas

⚠️ **The `dist/` folder gets wiped and rebuilt every run.** Never hand-edit HTML files in `dist/` — they will be overwritten next time you run the script. Always edit source files instead (`build.py`, posts in `posts/`, `style.css`).

⚠️ **Image paths must match.** If you reference `images/photo.jpg` in your markdown, the file must exist at `blog_py/images/photo.jpg` locally. The script copies the whole folder into `dist/`, so everything lines up.

⚠️ **Front-matter is required.** Every `.md` post must start with:
```markdown
---
title: "..."
date: "YYYY-MM-DD"
summary: "..."
tag: "optional"
---
```
