# paru-overlay

Personal [Paru](https://github.com/Morganamilo/paru) PKGBUILD overlay.
Packages in this repository take priority over packages with the same name in
the AUR.

## Packages

- `telegram-desktop-futpib-git` - Telegram with the control socket, pinned Rust
  rendering and wallet backends, and generated wallet bindings.
- `opencode-git` - OpenCode from upstream's `v1` branch, preserving the
  `acp --pure` interface used by existing agents.
- `bun-bin` - Bun's upstream binaries with a versioned `bun` provide so
  version-constrained build dependencies can be resolved.

Keep fixes for packages maintained by `futpib` on the AUR in their repositories
under `~/code/aur`. Put fixes for other maintainers' packages and orphaned
packages in this overlay. Telegram is carried here while its AUR ownership
is unresolved.

## Configure Paru

Create `~/.config/paru/paru.conf` with:

```ini
Include = /etc/paru.conf

[options]
Mode = arp

[futpib-overlay]
Url = https://github.com/futpib/paru-overlay.git
```

`Mode = arp` enables AUR, repository, and PKGBUILD packages so the overlay
participates in normal installs and upgrades.

Refresh the overlay and inspect the package source:

```console
paru -Sya
paru -Si telegram-desktop-futpib-git
```

Install or upgrade it normally:

```console
paru -S telegram-desktop-futpib-git
```

Paru refreshes Git-backed PKGBUILD repositories during `paru -Syu` as well.

To test local changes before pushing, replace `Url` with an absolute checkout
path:

```ini
[futpib-overlay]
Path = /path/to/paru-overlay
```

Changes made through `Path` are visible to Paru immediately.

## Updating a package

Edit the package's `PKGBUILD`, then regenerate and commit its `.SRCINFO`:

```console
cd telegram-desktop-futpib-git
makepkg --printsrcinfo > .SRCINFO
```

Review both files before pushing. The repository layout supports additional
packages by placing each PKGBUILD in its own directory.
