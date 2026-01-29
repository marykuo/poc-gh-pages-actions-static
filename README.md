# PoC of Static Site Deployment to GitHub Pages via GitHub Actions

![Deploy Status](https://github.com/marykuo/poc-gh-pages-actions-static/actions/workflows/static.yml/badge.svg)

This is a proof of concept repository to demonstrate how to deploy a static site to GitHub Pages using GitHub Actions.

## GitHub Pages via GitHub Actions

- Source:
  - Controlled by a workflow file in `.github/workflows/`.
  - We can explicitly choose to deploy from the root (`.`) or a specific folder (e.g., `docs/`) by changing the `path` value in the workflow file.
  - We can explicitly bypass Jekyll processing, ensuring that folders with underscores (e.g., `_css/`) are not ignored.
- Pros:
  - High Transparency: Real-time logs for every deployment step.
  - Customizable: Can include Linting, Testing, or Minification before deployment.
  - Clean History: Keeps the `main` branch clean from build artifacts.
- Cons:
  - Requires a one-time configuration of a YAML workflow file.

How to Enable:

1. Go to Settings > Pages.
2. Under Build and deployment > Source, select GitHub Actions.
3. GitHub will automatically detect and run your workflow file (e.g., `static.yml`).

## The Workflow Logic (Static HTML)

In this PoC, we use the official `Static HTML` workflow. Unlike the branch-based method, this process explicitly uploads your files as an Artifact before deploying them to the GitHub Pages server.

Even though the files are in the repository, GitHub Pages only "sees" what the Action uploads.

## Example Structure and Behavior

### Case #1: Deploy from Root ('.')

The repository root is treated as the web root.

```
├── .github/workflows
│   └── static.yml <-- The deployment engine
├── public <-- (Optional) Specific folder for public assets
├── README.md
└── index.html <-- Homepage
```

### Case #2: Deploy from 'docs' Folder

The `docs/` directory is treated as the web root. Files outside this folder (like `README.md` in root) will not be accessible online.

```
├── .github/workflows
│   └── static.yml <-- The deployment engine
├── public <-- (Optional) Specific folder for public assets
├── docs
│   ├── index.html <-- Homepage
│   └── _css <-- Folder with underscore
│     └── style.css
└── README.md
```
