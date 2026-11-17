# Overlord God releases

This repository holds the published builds of the Overlord God team client: the command line tools
(`overlord-god`, `overlord-god-stdio`), the local hub service and the desktop app. It has no source
code. The builds are made and signed on the maintainer's machine and uploaded here.

**Downloads:** [latest release](https://github.com/ovld-team/overlord-god-releases/releases/latest) ·
[all releases](https://github.com/ovld-team/overlord-god-releases/releases)

## Install

Download the archive for your system from the latest release, unpack it and run the installer
inside it. `README-INSTALL.md` in the archive has the details.

| System | Archive | Installer |
|---|---|---|
| macOS (Apple silicon) | `overlord-god_VERSION_macos_arm64.zip` | `bash install.sh` |
| Windows (x64) | `overlord-god_VERSION_windows_amd64.zip` | `powershell -NoProfile -ExecutionPolicy Bypass -File .\install.ps1` |
| Linux (x86_64, CLI only) | `overlord-god_VERSION_linux_amd64.tar.gz` | `bash install.sh` |

On Windows, run `Get-ChildItem -Recurse | Unblock-File` in the unpacked folder first. The apps are
not notarised (macOS) or Authenticode-signed (Windows); the installers handle the macOS quarantine
flag.

Check a download against `SHA256SUMS`:

```sh
shasum -a 256 -c SHA256SUMS --ignore-missing
```

## Updates

The desktop app checks this repository for a newer version: quietly once a day at start, or on
demand from **Check for Updates** in the app menu (macOS), the tray menu, or Settings > General >
App updates. It reads `latest.json` of the latest release, shows the version and its notes, and
installs the update only when the bundle carries the app's update signature (minisign, checked by
the Tauri updater against the public key built into the app).

The command line tools can check too: `overlord-god update --check-remote`.

Each release holds:

- the three install archives and `SHA256SUMS`
- `overlord-god_VERSION_macos_arm64.app.tar.gz` and `overlord-god_VERSION_windows_amd64-setup.exe`,
  the update bundles the app downloads, each with its `.sig`
- `latest.json`, the update manifest
