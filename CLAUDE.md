# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A simple Flask web application ("Hello, World!") containerized and deployed via GitHub Actions to the GitHub Container Registry (`ghcr.io`).

## Development Commands

```bash
# Install dependencies
uv sync

# Run the app locally (serves on port 8080)
uv run python app.py

# Add a dependency
uv add <package>

# Build container image locally
docker build -t alb-test .
```

## Architecture

- **app.py** — Single-file Flask app. Routes: `/` (hello world), `/health` (JSON health check).
- **Dockerfile** — Uses `python:3.14-slim` with `uv` copied from the official image for dependency installation.
- **.github/workflows/build.yml** — Builds and pushes the container image to `ghcr.io` on push to `main`; build-only on PRs.

## Key Details

- Python ≥ 3.14 required (set in `pyproject.toml`)
- Dependency management via `uv` (not pip) — lockfile is `uv.lock`
- App listens on `0.0.0.0:8080`
