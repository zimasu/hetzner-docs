# hetzner-docs

Infrastructure documentation for Hetzner deployments, built with [MkDocs](https://www.mkdocs.org/) and served via nginx in Docker.

## Structure

```
hetzner-docs/
├── docs/                  # Source — edit these Markdown files
├── .github/workflows/     # CI: build, tag, gitops manifest update
├── Dockerfile             # nginx image serving the built site
├── nginx.conf             # nginx config
├── mkdocs.yml             # MkDocs config (theme, nav, plugins)
├── requirements.txt       # Python deps (mkdocs + plugins)
└── site/                  # Built output — do not edit, not in git
```

## Local development

**Prerequisites:** Python 3.x

```bash
pip install -r requirements.txt
mkdocs serve
```

Open [http://localhost:8000](http://localhost:8000). Changes to `docs/` hot-reload automatically.

## Build

```bash
mkdocs build        # outputs to site/
```

## Docker

```bash
docker build -t hetzner-docs .
docker run -p 8080:80 hetzner-docs
```

## Deployment

Pushing to `main` triggers the GitHub Actions workflow, which:

1. Builds the MkDocs site
2. Builds and pushes a Docker image with a SHA tag
3. Updates the GitOps manifest with the new image tag

## Contributing

Edit files under `docs/`. The nav structure is defined in `mkdocs.yml`.
