# gimagereader-flatpak

**gImageReader** is a simple optical character recognition (OCR) application which acts as a frontend to the tesseract OCR engine.

![gimagereader-gtk3-flatpak screenshot](gimagereader-gtk3-flatpak.png)

![gimagereader-qt5-flatpak screenshot](gimagereader-qt5-flatpak.png)

[Homepage](https://github.com/manisandro/gImageReader)

This repo is about the flatpak package (Gtk+3/Qt5).

## Instructions

### Requirements

* [flatpak](https://github.com/flatpak/flatpak)
* [flatpak-builder](https://github.com/flatpak/flatpak-builder)

For EL7:

```
# yum install 'flatpak' 'flatpak-builder'
```

You may also wish to install the `xdg-desktop-portal*` packages:

```
# yum install 'xdg-desktop-portal*'
```

See also:

* [flatpak setup](https://flatpak.org/setup)

### Adding repository

```
$ flatpak remote-add --if-not-exists "flathub" "https://dl.flathub.org/repo/flathub.flatpakrepo"
```

See also:

* [flathub setup](http://docs.flatpak.org/en/latest/using-flatpak.html#add-a-remote)

### Prepare

```
$ flatpak install "flathub" "org.kde.Sdk//5.12"
```

```
$ flatpak install "flathub" "org.kde.Platform//5.12"
```

### Build

```
$ flatpak-builder "build" "com.github.manisandro.gImageReader.yaml" --force-clean --install-deps-from="flathub"
```

### Test

```
$ flatpak-builder --run "build" "com.github.manisandro.gImageReader.yaml" "sh"
```

### Install

```
$ flatpak-builder --repo="repo" --force-clean "build" "com.github.manisandro.gImageReader.yaml"
```

```
$ flatpak --user remote-add --no-gpg-verify "gimagereader" "repo"
```

```
$ flatpak --user install "gimagereader" "com.github.manisandro.gImageReader"
```

### Run

```
$ flatpak run "com.github.manisandro.gImageReader"
```

### Uninstall

```
$ flatpak --user uninstall "com.github.manisandro.gImageReader"
```

```
$ flatpak --user remote-delete "gimagereader"
```

See also: [Building your first Flatpak](http://docs.flatpak.org/en/latest/first-build.html)

## FAQ

### Known issues

`gimagereader-gtk`:
 * Unable to hide the `Manage Languages` position from menu when using `System-wide paths` and using **PackageKit** doesn't make much sense in the sandboxed environment.
 * Unable to manage languages when using `User paths`: `Failed to fetch list of available languages: Failed to fetch list of available languages: ` (`gio.File.read_finish`: `Operation not supported` - probably missing required dependencies for **GVFS**, maybe the `http` backend?).
 * Unable to download dictionaries when using `User paths`: `Could note read https://cgit.freedesktop.org/libreoffice/dictionaries/tree/: .` (`gio.File.read_finish`: `Operation not supported` - probably missing required dependencies for **GVFS**, maybe the `http` backend?).

### Are you the author of gImageReader?

No, I only created the flatpak package for it.

See also:

* [GitHub repo](https://github.com/manisandro/gImageReader)

