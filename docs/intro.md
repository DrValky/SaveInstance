---
sidebar_position: 1
---

# Getting Started

The saveinstance that actually saves your game **the way it looks** — correct colors, images, unions, terrain, the whole map, and even the scripts. No more grey, broken, half-empty saves.

## Usage

```lua
local Params = {
    RepoURL = "https://raw.githubusercontent.com/RealSlimShady2000/SaveInstance420Edition/main/",
    SSI = "saveinstance",
}

local synsaveinstance = loadstring(game:HttpGet(Params.RepoURL .. Params.SSI .. ".luau", true), Params.SSI)()

synsaveinstance({
    SetStreaming = false,       -- true = capture the whole streaming map
    DecompilePrepass = false,   -- true = decompile all scripts fast, up front
    NeutralizeLighting = false, -- true = save opens in bright daylight
    ExportObj = false,          -- true = also dump meshes to a .obj
})
```

One call, no extra scripts. Every option is off by default — flip on what you want.

## Why use this one

- 🎨 **Colors & sizes save right** (others load everything grey and default-sized)
- 🖼️ **Decals, images & sounds save** (the stuff most savers miss)
- 🧩 **Unions & terrain render properly**
- 🗺️ **Grabs the whole streaming map**, not just what's near you
- 📜 **Decompiles scripts even if your executor can't**
- ☀️ **Opens bright** instead of dark and foggy
- 🧱 **Recovers meshes** to `.obj`
- ⚡ **Fast and won't crash** on huge games

👉 See the **[Options Reference](./options)** for every setting.

> Built on the original **[UniversalSynSaveInstance](https://luau.github.io/)**. Modified by **Robloxscripts.com** — Discord: discord.robloxscripts.com
