# mkdocs-site

Автор: Кашапов Константин

## Отчёт - Практика 1


### 1. Установка MkDocs

```bash
pip install mkdocs
```

### 2. Генерирую проект

Используем `./` вместо названия для использования текущей директории.

```bash
mkdocs new ./
```

### 3. Меняю содержимое

Файл `docs/index.md`.

```md
# Welcome to MkDocs

## Lab 1

ITMO-PYTHON
```

### 4. Создаю Action

Файл `.github/workflows/mkdocs.yml`.

```yml
name: Deploy MkDocs to Pages

on:
  push:
    branches: ["main"]

  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.12
      - name: Setup MkDocs
        run: pip install mkdocs
      - name: Build
        run: mkdocs build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: 'site/'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 5. Результат

Страница доступна по ссылке [https://kashapovk.github.io/mkdocs-site/](https://kashapovk.github.io/mkdocs-site/) 
