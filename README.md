# Cursorex — public releases

This repository publishes **only the local bridge** (native host + bridge runtime) so Chrome Web Store users can install a compatible build without access to the private source repository.

## Extension (Chrome Web Store)

Install **Cursorex** from the store:

https://chromewebstore.google.com/detail/infbgmlkjfimojcjikknabbaifbafjoo?utm_source=github&utm_medium=wideserg-public&utm_campaign=cursorex_readme

## What to download here

Open **Releases** and download **`cursorex-bridge-*.zip`**. That archive is a ready-made bridge bundle, not the source tree of this repo.

## Requirements

- **Node.js** LTS (20+), with `node` on your PATH  
- **Google Chrome** (stable)  
- **Cursor CLI** on the machine if you use the local Cursor app-server flow (same as the main Cursorex setup docs)

## Install the bridge (after extracting the zip)

Run **one** launcher for your OS. All of these sit in the **root** of the extracted folder:

| OS | Install | Uninstall |
|----|---------|-----------|
| Windows | Double-click **`install_windows.bat`** | **`uninstall_windows.bat`** |
| macOS | Double-click **`install_macos.command`** | **`uninstall_macos.command`** |
| Linux | In a terminal: **`chmod +x install_linux.sh`** if needed, then **`./install_linux.sh`** | **`./uninstall_linux.sh`** |

Then in Chrome: **Reload** the extension → in the side panel use **Check connection**.

For other Chrome channels (Beta, etc.), pass the same flags as for `node install-native-host.mjs` (see the full project) or run that script directly with extra arguments.

## About this repository

- Bridge artifacts are built from a private repository and published here automatically.  
- There is no application source or CI development in this repo—only releases and this README.
