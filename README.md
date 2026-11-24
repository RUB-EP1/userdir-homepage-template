# EP1 homepage template

[![License](https://img.shields.io/github/license/RUB-EP1/userdir-homepage-template)](./LICENSE)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)
[![Spelling checked](https://img.shields.io/badge/cspell-checked-brightgreen.svg)](https://github.com/streetsidesoftware/cspell/tree/main/packages/cspell)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

This repository is a template for personal EP1 homepages served from `https://ep1.rub.de/~<username>/`.

It uses [Quarto](https://quarto.org) for the static website and publishes the rendered site to the `~/WWW` directory on the EP1 infrastructure with [`userdir-publish`](https://rub-ep1.github.io/userdir-publish).

## Create your homepage repository

Create a new repository from this template and clone it to your machine. Then customize the template values in:

- [`docs/index.qmd`](./docs/index.qmd): homepage content
- [`docs/_quarto.yml`](./docs/_quarto.yml): page title, description, links, and site URL
- [`pyproject.toml`](./pyproject.toml): package metadata

At minimum, replace all occurrences of `Your Name`, `username`, and `YOUR_GITHUB_USERNAME`.

## Installation instructions

The developer dependencies required to develop this project are installed with the [`uv`](https://docs.astral.sh/uv) package manager. Once you navigate into a local clone of this repository, run:

```shell
uv sync
source .venv/bin/activate
```

In addition, install [Poe the Poet](https://poethepoet.natn.io), which runs the common tasks defined in [`pyproject.toml`](./pyproject.toml), and [`prek`](https://prek.j178.dev), which runs style checks before each commit:

```shell
uv tool install poethepoet
uv tool install prek
```

Then activate the `prek` hooks in your clone, so that style checks run on every commit:

```shell
prek install
```

The most important task is to build the website and start a preview server:

```shell
poe doclive
```

## Updating your EP1 homepage

The homepage is published to the `WWW/` directory in your EP1 home directory with [`userdir-publish`](https://rub-ep1.github.io/userdir-publish). Build and publish the site with:

```shell
poe website
```

This renders the Quarto site from a clean build directory and copies it to `/home/tau/<username>/WWW` with `rsync`, directly on EP1 machines and over SSH to `ep1.rub.de` from anywhere else. Files that are no longer part of the build are removed, while the subdirectories that other projects publish to are preserved. If your EP1 login differs from your local user name, set it once in `~/.config/userdir-publish/config.toml`:

```toml
user = "your-ep1-username"
```
