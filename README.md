[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

# EdgeTX Lua Stubs

> **Auto-generated LuaLS-compatible `.d.lua` stubs and manifest for the EdgeTX Lua API — published by [edgetx-lua-gen](https://github.com/JeffreyChix/edgetx-lua-gen).**

---

## What this repo is

This repo is the output target of the [edgetx-lua-gen](https://github.com/JeffreyChix/edgetx-lua-gen) pipeline. Every time the generator runs, it commits updated stubs and a manifest here. **Do not edit files in this repo manually** — all content is generated, and any manual changes will be overwritten on the next run.

The [EdgeTX Dev Kit](https://github.com/JeffreyChix/edgetx-dev-kit) VS Code extension consumes this repo directly — fetching `manifest.json` on activation and downloading only the stubs that have changed.

---

## Repo structure

```
/
├── manifest.json               ← consumed by the VS Code extension
└── stubs/
    ├── 2.10/
    │   ├── edgetx-lua-api.json
    │   ├── edgetx-script-types.json
    │   ├── edgetx.globals.d.lua
    │   ├── edgetx.constants.d.lua
    │   ├── edgetx.scripts.d.lua
    │   ├── edgetx.bitmap.d.lua
    │   ├── edgetx.lcd.d.lua
    │   └── edgetx.model.d.lua
    └── 2.9/
        └── ...
    └── 2.11/
        └── ...
    │   ├── edgetx.lvgl.d.lua
```

Each versioned folder maps to an EdgeTX firmware release. The generator produces one `.d.lua` file per Lua module — any new module in a future EdgeTX release is handled automatically.

---

## How the extension consumes this repo

On activation, the EdgeTX Dev Kit extension:

1. Fetches `manifest.json` from this repo via `raw.githubusercontent.com`
2. Compares the `stubHash` for the active EdgeTX version against the locally cached value
3. If changed, downloads only the updated stub files listed under `files` for that version
4. Injects the stubs into `Lua.workspace.library` for LuaLS IntelliSense

Stubs are cached locally in the extension's global storage and updated silently in the background — no manual intervention needed.

---

## Manifest

`manifest.json` tracks the state of every generated version:

```json
{
  "manifestVersion": 2,
  "updatedAt": "2026-03-16T06:00:00Z",
  "versions": {
    "2.10": {
      "generatedAt": "2026-03-16T06:00:00Z",
      "stubHash": "f7e6d5c4a3b2e1d0...",
      "sources": {
        "radio/src/lua/api_colorlcd.cpp": "fda476ff4e5bd1cccc2cc55b30176086c6fd2be2",
        "radio/src/lua/api_general.cpp": "a1b2c3d4e5f6g7h8...",
        "radio/src/lua/api_misc.cpp": "e5f6g7h8i9j0k1l2..."
      },
      "files": [
        "edgetx-lua-api.json",
        "edgetx-script-types.json",
        "edgetx.globals.d.lua",
        "edgetx.constants.d.lua",
        "edgetx.scripts.d.lua",
        "lcd.d.lua",
        "model.d.lua"
      ]
    }
  }
}
```

| Field             | Description                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------- |
| `manifestVersion` | Schema version of the manifest itself. Only bumped on breaking structural changes. Current supported version is 2.             |
| `updatedAt`       | Timestamp of the last generation run that produced any change                                  |
| `generatedAt`     | When this specific version's stubs were last generated                                         |
| `stubHash`        | SHA-256 of all stub files combined. Extension compares this to detect if re-download is needed |
| `sources`         | Map of each parsed C++ source file path to its git blob SHA                                    |
| `files`           | Exact list of files available for this version under `stubs/<version>/`                        |

---

## Related

- [edgetx-lua-gen](https://github.com/JeffreyChix/edgetx-lua-gen) — the generator pipeline that produces this repo's content
- [edgetx-dev-kit](https://github.com/JeffreyChix/edgetx-dev-kit) — the VS Code extension that consumes it
