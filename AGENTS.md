# Repository maintenance

This is the live WsAAAH APT source at `https://wsaaah.github.io/`.

## Layout

- Put published package files in `debs/`; never invent package entries or hand-edit generated indexes.
- Put optional package metadata under `depictions/<package id>/`.
- Keep `sileo-featured.json` empty unless its package and artwork actually exist in this repository.
- `index.html` and `CydiaIcon.png` are the public source home page and icon.
- Do not commit `Packages`, `Packages.xz`, `Release`, `_site/`, or `.repo-build.*`.

## Checks

Run `bash -n scripts/update-repository.sh` for the local syntax check. The complete repository build runs on Ubuntu in GitHub Actions, where `apt-ftparchive`, `xz`, and `qrencode` are installed. It executes:

```sh
SOURCE_NAME=WsAAAH \
SOURCE_URL=https://wsaaah.github.io/ \
REPOSITORY_NAME=WsAAAH.github.io \
REPOSITORY_OWNER=WsAAAH \
./scripts/update-repository.sh
```

A successful full build writes the deployable site to `_site/`; that directory is generated and ignored. On each relevant push to `main`, `.github/workflows/update-repository.yml` builds `Packages`, `Packages.xz`, and `Release`, then deploys `_site/` with GitHub Pages Actions.

## Publishing

Preserve the existing `main` history. Commit normally and push without force. A GitHub Pages deployment may require the repository's Pages source to be set to **GitHub Actions** once in repository settings.
