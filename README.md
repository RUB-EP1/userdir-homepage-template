# EP1 homepage template

[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)
[![Spelling checked](https://img.shields.io/badge/cspell-checked-brightgreen.svg)](https://github.com/streetsidesoftware/cspell/tree/main/packages/cspell)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

This repository is a template for personal EP1 homepages served from `https://www.ep1.rub.de/~<username>/`.

It uses [Quarto](https://quarto.org) for the static website and includes a small helper script for copying the rendered site to the `~/WWW` directory on the EP1 infrastructure.

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

In addition, you can install [Poe the Poet](https://poethepoet.natn.io), which defines common tasks under [`pyproject.toml`](./pyproject.toml):

```shell
uv tool install --python=3.13 --with poethepoet poe
```

The most important task is to build the website and start a preview server:

```shell
poe doclive
```

It is also recommended to install [`pre-commit`](https://pre-commit.com) to run style checks before committing changes:

```shell
uv tool install --with pre-commit-uv pre-commit
```

## Updating your EP1 homepage

The [`update-www`](./update-www) script can be used to update the content of your EP1 homepage. This is the `WWW/` directory in your EP1 home directory. On EP1 machines, create the directory once:

```shell
mkdir ~/WWW
```

Then publish the rendered site with:

```shell
./update-www
```

The script builds the Quarto site, replaces the generated homepage content in `~/WWW`, preserves existing subdirectories, and sets permissions suitable for public web serving.

### Updating from a non-EP1 machine

It is also possible to update your homepage externally using [`sshfs`](https://github.com/libfuse/sshfs). For this, mimic the `/home/tau/$EP1_USERNAME` directory structure locally, with `$EP1_USERNAME` set to your EP1 username:

```shell
sudo mkdir -p /home/tau/$USER
sudo chown -R $USER /home/tau/$USER
```

Mount the remote directory:

```shell
EP1_USERNAME=your-ep1-username
sshfs $EP1_USERNAME@ep1.rub.de:/home/tau/$EP1_USERNAME /home/tau/$USER
```

> [!WARNING]
> Your local `$USER` name can differ from `$EP1_USERNAME`. The [`update-www`](./update-www) script uses `/home/tau/$USER`.

The [`update-www`](./update-www) script can now be run from your local machine, as it will update the mounted remote directory.
