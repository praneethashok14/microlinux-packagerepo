# MicroLinux package repository

Packages for MicroLinux, a tiny Linux distribution for
**x86_64** and **aarch64**, built from source with Buildroot 2026.02.3.

## Using it (on MicroLinux)

```sh
sudo mlpkg update
mlpkg list                    # applications (mlpkg list -a: also libraries)
sudo mlpkg install python3 git mpv
sudo mlpkg remove mpv && sudo mlpkg autoremove
```

MicroLinux already has this repository in `/etc/mlpkg/repos.conf`:

    https://github.com/praneethashok14/microlinux-packagerepo/releases/download/packages-<arch>

Each architecture is a GitHub release (`packages-x86_64`, `packages-aarch64`)
whose assets are the packages (`*.mlp`, SquashFS images) and an `INDEX`:

    name|version|file|sha256|size|description|depends|section

`mlpkg` verifies every download against the SHA-256 in the INDEX and installs
dependencies first.

## This repository

| Path | Content |
|------|---------|
| `x86_64/INDEX`, `aarch64/INDEX` | package lists (the same files as the release assets) |
| `x86_64/SOURCES.txt`, `aarch64/SOURCES.txt` | every package's version, license and upstream source |
| `*/*.mlp` | the packages: git-ignored here, uploaded as release assets |

The packages are produced by the MicroLinux build
([praneethashok14/microlinux](https://github.com/praneethashok14/microlinux):
`scripts/build.sh`, with the list in `external/configs/fragments/repo.config`)
and published with `scripts/publish-repo.sh`.

## Licenses and sources

Each package keeps its upstream license (listed in `SOURCES.txt`). The
corresponding source is the upstream release named there plus Buildroot's
patches for that package:
https://gitlab.com/buildroot.org/buildroot/-/tree/2026.02.3/package
