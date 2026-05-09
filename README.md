# Cursorex — public releases

This repository publishes **only the local bridge** (native host + bridge runtime) for people who install the [**Cursorex** extension in the Chrome Web Store](https://chromewebstore.google.com/detail/infbgmlkjfimojcjikknabbaifbafjoo?utm_source=github&utm_medium=wideserg-public&utm_campaign=cursorex_readme) and need a matching bridge build without access to the private source repository.

## Installation

1. **Extension.** Add [Cursorex in the Chrome Web Store](https://chromewebstore.google.com/detail/infbgmlkjfimojcjikknabbaifbafjoo?utm_source=github&utm_medium=wideserg-public&utm_campaign=cursorex_readme) to Chrome.

2. **Bridge bundle.** In this repo open [**Releases**](https://github.com/wideserg/cursorex-public/releases) and download **`cursorex-bridge-*.zip`**. It is a prebuilt bridge package, not the source tree of `cursorex-public`.

3. **Prerequisites.** **Node.js** LTS (20+) with `node` on your PATH, **Google Chrome** (stable), and the **Cursor CLI** on your machine if you use the local Cursor app-server flow (see the main Cursorex docs).

4. **Register the bridge.** Extract the zip. In the **root** of the extracted folder, run **one** launcher for your OS:

| OS | Install | Uninstall |
|----|---------|-----------|
| Windows | Double-click **`install_windows.bat`** | **`uninstall_windows.bat`** |
| macOS | Double-click **`install_macos.command`** | **`uninstall_macos.command`** |
| Linux | **`chmod +x install_linux.sh`** if needed, then **`./install_linux.sh`** | **`./uninstall_linux.sh`** |

5. **Finish in Chrome.** Reload the Cursorex extension, then open the side panel and use **Check connection**.

For other Chrome channels (Beta, etc.), pass the same flags as for `node install-native-host.mjs` in the full project, or run that script with extra arguments.

## About this repository

- Bridge artifacts are built from a private repository and published here automatically.  
- There is no application source or CI development in this repo—only releases and this README.
