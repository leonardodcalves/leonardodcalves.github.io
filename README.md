# leonardodcalves.github.io

Meu blog pessoal. Escrevo sobre o que eu quiser escrever.

**Site ao vivo:** [leonardodcalves.github.io](https://leonardodcalves.github.io)

## Sobre mim

Sou o Leonardo. Engenheiro Agrônomo, sul-mato-grossense, cozinheiro, fotógrafo, viajante, músico, e apaixonado por computadores.

## Sobre o site

Este blog é um site estático gerado por um pequeno script Python. Sem frameworks pesados, sem banco de dados, sem JavaScript rodando no cliente - apenas HTML, CSS, e alguns arquivos Markdown.

---

## Notes to self (maintenance)

This repository holds only the *generated* output - the HTML and CSS that GitHub Pages serves. The source files (the Python script, the Markdown posts, the stylesheet) live in a separate folder on my machine.

### Folder on my laptop

```
blog_py/
├── build.py      # generator script
├── style.css     # site style
├── posts/        # .md source files
└── dist/         # build output — this is what gets uploaded here
```

### Workflow

1. Write or edit a post inside `posts/` as a `.md` file with front-matter (title, date, summary, tag).
2. Run `python3 build.py` to regenerate `dist/`.
3. On this repo: `Add file → Upload files`, drag in the contents of `dist/`, commit.
4. Wait ~60 seconds, hard-refresh the live site.

### If I forget how to install the dependency

```bash
uv pip install markdown
```

### Things that already bit me once

- The `dist/` folder gets wiped and rebuilt every run. Never hand-edit its contents.
- All blog-wide config (title, logo, hero text, bio, footer) lives at the top of `build.py`, in the block marked `EDIT THIS SECTION TO CUSTOMIZE YOUR BLOG`.
