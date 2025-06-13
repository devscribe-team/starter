# edit at 8:31 mf 1

# 🚀 Quickstart Guide for API Docs Platform

Welcome to our **API Documentation Platform**! This guide will help you set up and start creating docs for your customers in no time.

---

## 🎬 Table of Contents

1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Generating Documentation](#generating-documentation)
5. [Customizing Your Docs](#customizing-your-docs)
6. [Deployment](#deployment)
7. [Troubleshooting](#troubleshooting)
8. [Resources](#resources)

---

## 📝 Prerequisites

* **Operating System**: macOS, Linux, or Windows
* **Node.js** (v14+) or **Python** (v3.8+)
* **Git** installed and configured
* A valid **API definition** (OpenAPI / Swagger) file (`.yaml` / `.json`)

> Tip: Use `node -v` or `python3 --version` to check your versions.

---

## 💾 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-org/api-docs-platform.git
cd api-docs-platform
```

### 2. Install Dependencies

* **JavaScript** version:

  ```bash
  npm install
  ```
* **Python** version:

  ```bash
  pip install -r requirements.txt
  ```

---

## ⚙️ Configuration

Configure your API source and credentials.

| Variable              | Description                  | Example                      |
| --------------------- | ---------------------------- | ---------------------------- |
| `API_DEFINITION_PATH` | Path to your OpenAPI file    | `./spec/openapi.yaml`        |
| `OUTPUT_DIR`          | Directory for generated docs | `./docs`                     |
| `THEME`               | Doc theme name               | `light`, `dark`, `corporate` |

> You can set these in a `.env` file or pass via CLI:
>
> ```bash
> export API_DEFINITION_PATH=./spec/api.yaml
> export OUTPUT_DIR=./public/docs
> export THEME=dark
> ```

---

## 🔧 Generating Documentation

Run the CLI command as if it were a compiled tool:

```bash
./apiDocsGen ./spec/openapi.yaml ./output/docs --theme=light
```

> **Parameters**:
>
> * **Input file**: `./spec/openapi.yaml`
> * **Output folder**: `./output/docs`
> * **Theme**: `--theme=light`

### Example `curl` request to preview docs locally

```bash
curl -X GET \
  "http://localhost:3000/docs/index.html" \
  -H "Accept: text/html"
```

---

## 🎨 Customizing Your Docs

1. **Themes**

   * Switch via `--theme=dark`
   * Create a custom theme by editing `themes/custom.scss`
2. **Logo & Branding**

   * Replace `./assets/logo.png` (recommended: **.png**, **.svg**)
3. **Navigation**

   * Modify `nav.yml`:

     ```yaml
     - title: Home
       link: /index.html
     - title: Reference
       link: /reference.html
     ```

* [x] **Task List** example:

  * [x] Install platform
  * [ ] Customize theme
  * [ ] Deploy to production

---

## 🚀 Deployment

> Use GitHub Pages, Netlify, or any static host.

```bash
# Build static assets
./apiDocsGen ./spec/openapi.yaml ./public/docs

# Deploy via GitHub Pages
git add public/docs
git commit -m "Deploy API docs"
git subtree push --prefix public/docs origin gh-pages
```

---

## ❓ Troubleshooting

> **Issue**: *Docs not updating after spec changes*

```bash
# Clear cache and rebuild
rm -rf ./output/docs/*
./apiDocsGen ./spec/openapi.yaml ./output/docs
```

> **Issue**: *Page styling broken*

* Check your theme file syntax.
* Ensure your CSS is valid with a linter (e.g., `stylelint`).

```bash
npx stylelint "themes/**/*.scss"
```

---

## 📚 Resources

* 📖 [Official Docs](https://example.com/docs)
* 🛠️ [GitHub Repository](https://github.com/your-org/api-docs-platform)
* 💬 [Support Forum](https://forum.example.com)

> ^ This guide uses a variety of Markdown features: **headers**, *emphasis*, ~~strikethrough~~, `inline code`, code blocks, tables, task lists, blockquotes, links, images, and horizontal rules.

---

[^1]: Markdown is awesome! Remember to check your rendered docs in multiple browsers.
