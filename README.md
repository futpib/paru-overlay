# paru-overlay

Personal [Paru](https://github.com/Morganamilo/paru) PKGBUILD overlay.
Packages in this repository take priority over packages with the same name in
the AUR.

## Packages

- `buzz-desktop-git` - Buzz desktop built from the latest `main` branch,
  including the `buzz-backend-kubernetes` sidecar required by the desktop
  application's **Run on** feature.

## Configure Paru

Create `~/.config/paru/paru.conf` with:

```ini
Include = /etc/paru.conf

[futpib-overlay]
Url = https://github.com/futpib/paru-overlay.git
```

Refresh the overlay and inspect the package source:

```console
paru -Sya
paru -Si buzz-desktop-git
```

Install or upgrade it normally:

```console
paru -S buzz-desktop-git
```

Paru refreshes Git-backed PKGBUILD repositories during `paru -Syu` as well.

For local development before the GitHub repository exists, replace `Url` with
an absolute checkout path:

```ini
[futpib-overlay]
Path = /path/to/paru-overlay
```

Changes made through `Path` are visible to Paru immediately.

## Updating a package

Edit the package's `PKGBUILD`, then regenerate and commit its `.SRCINFO`:

```console
cd buzz-desktop-git
makepkg --printsrcinfo > .SRCINFO
```

Review both files before pushing. The repository layout supports additional
packages by placing each PKGBUILD in its own directory.
