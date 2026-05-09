# Cursorex — public releases

This repository publishes **only the local bridge** (native host + bridge runtime) for people who install the [**Cursorex** extension in the Chrome Web Store](https://chromewebstore.google.com/detail/infbgmlkjfimojcjikknabbaifbafjoo?utm_source=github&utm_medium=wideserg-public&utm_campaign=cursorex_readme) and need a matching bridge build without access to the private source repository.

## Installation

1. **Extension.** Add [Cursorex in the Chrome Web Store](https://chromewebstore.google.com/detail/infbgmlkjfimojcjikknabbaifbafjoo?utm_source=github&utm_medium=wideserg-public&utm_campaign=cursorex_readme) to Chrome.

2. **Bridge bundle.** In this repo open [**Releases**](https://github.com/wideserg/cursorex-public/releases) and download **`cursorex-bridge-*.zip`**. It is a prebuilt bridge package, not the source tree of `cursorex-public`.

3. **Prerequisites.** **Node.js** LTS (20+) with `node` on your PATH, **Google Chrome** (stable), and the **Cursor CLI** on your machine if you use the local Cursor app-server flow (see the main Cursorex docs).

4. **Register the bridge.** Extract the zip. In the **root** of the extracted folder, run **one** launcher for your OS. The window stays open and prints **SUCCESS** or **FAILED**. By default the installer registers **Google Chrome** Stable/Beta/Dev/Canary and **Microsoft Edge** (Windows); use `--browser=chrome` on the underlying `node install-native-host.mjs` if you need a single channel.

| OS | Install | Uninstall |
|----|---------|-----------|
| Windows | Double-click **`install_windows.bat`** | **`uninstall_windows.bat`** |
| macOS | Double-click **`install_macos.command`** | **`uninstall_macos.command`** |
| Linux | **`chmod +x install_linux.sh`** if needed, then **`./install_linux.sh`** | **`./uninstall_linux.sh`** |

5. **Finish in Chrome.** Reload the Cursorex extension, then open the side panel and use **Check connection**.

**About “Allowed extension IDs” in the installer output:** the script may list more than one ID. The **primary** line is from your bundle’s `manifest` key (or an ID you pass in). **Extra** IDs are **discovered** from local Chrome/Edge profile data (another install, an old unpacked build, or a second profile) when they match this extension’s permissions and layout—so native messaging keeps working if you still have that install around.

## About this repository

- Bridge artifacts are built from a private repository and published here automatically.  
- There is no application source or CI development in this repo—only releases and this README.

## Advanced: install / uninstall flags

The `.bat` / `.command` / `.sh` launchers run `node install-native-host.mjs` or `node uninstall-native-host.mjs` in the extracted folder and **forward all extra arguments** (`%*` / `"$@"`). Double-clicking uses **no** extra flags—only the defaults below.

### Install (`install_windows.bat`, …)

**Default when you only double-click**

- Registers the native host for **all Google Chrome channels** the script supports on your OS (Stable, Beta, Dev, Canary, etc.) and **Microsoft Edge** on **Windows**.
- Picks the extension ID from the bundled `manifest.json` and may **discover additional IDs** already present in your Chrome/Edge profiles (see the note in [Installation](#installation)).

**Run manually only if you need to**

Open a terminal in the **extracted bundle root** (where the `.mjs` files live), ensure `node` is on your PATH, then:

```bash
node install-native-host.mjs
```

Useful options (combine as needed):

| Flag / argument | Purpose |
|-----------------|--------|
| `<extension-id>` | First positional argument. Use the ID from `chrome://extensions` if it differs from the installer default. |
| `--browser=chrome` | Limit to one channel (or a comma-separated list, e.g. `chrome,edge`). **Omit** `--browser` for the full default set. |
| `--profile-dir=/path/to/profile` | Extra native-messaging manifest under that Chromium profile (**non-Windows**). On Windows, Chrome uses **registry** registration; this flag is not the main path—see installer hints if setup still waits. |
| `--include-legacy-extension-ids` | Widen allowed extension IDs for older side-by-side installs (only if you know you need it). |

Examples:

```bash
node install-native-host.mjs abcdefghijklmnopqrstuvwxyz123456
node install-native-host.mjs --browser=chrome
```

### Uninstall (`uninstall_windows.bat`, …)

**Default when you only double-click**

- Removes browser registrations for the **same broad set** of Chrome channels + Edge (Windows) as install.
- Deletes the **entire CursorSidepanel data directory** for your user (native host copy, native messaging manifests under that tree, default workspace, generated images, logs, `secrets.json`, etc.): on Windows `%LOCALAPPDATA%\CursorSidepanel`, on macOS `~/Library/Application Support/CursorSidepanel`, on Linux both `~/.config/cursor-sidepanel` and `~/.local/share/cursor-sidepanel`.

**Run manually only if you need to**

```bash
node uninstall-native-host.mjs
```

| Flag | Purpose |
|------|--------|
| `--keep-user-data` | **Do not** delete the CursorSidepanel folders above—only remove the installed native host files and `NativeMessagingHosts` layout under the config dir. Use this if you want to keep local workspace or caches but drop registration. |
| `--with-secrets` | Only meaningful **with** `--keep-user-data`: also delete `secrets.json` (saved API keys). Full default uninstall already removes the whole directory, so secrets go away without this flag. |
| `--browser=…` | Unregister only the listed channel(s), same comma-separated style as install. On **Windows**, omit `--browser` or use `chrome` / `chrome-beta` / `chrome-dev` / `chrome-canary` / `edge` (not `chromium` / `chrome-for-testing` for uninstall). |

Example (unregister but keep your local CursorSidepanel data):

```bash
node uninstall-native-host.mjs --keep-user-data
```
