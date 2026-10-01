# Irodori Table packages

Package repository hosting for [Irodori Table](https://github.com/irodori-table/irodori-table):
distribution files, APT metadata, and the signing key published through GitHub
Pages at <https://irodori-table.github.io/irodori-packages/>.

## What lives here

| Path | Purpose |
| --- | --- |
| `apt/` | The signed Debian/Ubuntu APT repository (`dists/`, `pool/`, keyring) |
| `index.html` | GitHub Pages landing page with install steps |
| `.github/workflows/pages.yml` | Publishes the repository root to GitHub Pages |

The `apt/` tree is generated and pushed by the Irodori Table release workflow
(`publish-apt` in `irodori-table/.github/workflows/release.yml`). Do not edit it
by hand: change the release workflow or `tools/release/apt-repo.mjs` in
`irodori-table` instead.

## Install

### Debian / Ubuntu (APT)

```sh
curl -fsSL https://irodori-table.github.io/irodori-packages/apt/irodori-archive-keyring.gpg \
  | sudo tee /usr/share/keyrings/irodori-archive-keyring.gpg >/dev/null

echo "deb [signed-by=/usr/share/keyrings/irodori-archive-keyring.gpg] https://irodori-table.github.io/irodori-packages/apt stable main" \
  | sudo tee /etc/apt/sources.list.d/irodori.list

sudo apt update
sudo apt install irodori-table
```

Supported architectures: `amd64`, `arm64`.

### Arch Linux (AUR)

The AUR package is generated from the release `.deb` payload:

```sh
yay -S irodori-table
# or: paru -S irodori-table
```

It installs the same binaries, desktop entry, and icons as the Debian package.

## Releasing

The APT tree is published only for stable releases. The release workflow signs
the repository with the project GPG key and pushes it here; GitHub Pages then
serves it. See `RELEASING.md` in `irodori-table` for the required secrets and
the key generation steps.
