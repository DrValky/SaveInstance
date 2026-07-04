# SaveInstance 420 Edition - FIXED by Valky

The saveinstance that actually saves your game **the way it looks.**

Most saveinstance scripts hand you a broken file — grey parts, missing images, no scripts, half the map. This one doesn't.

## Why use this one

- 🎨 **Correct colors & sizes** — other savers drop these and everything loads grey and default-sized. This saves them right.
- 🖼️ **Decals, images & sounds save** — the stuff modern savers silently miss.
- 🧩 **Unions & terrain render properly** — not invisible, not grey boxes.
- 🗺️ **Grabs the WHOLE map** — force-loads streaming games so you get the entire place, not just what's next to you.
- 📜 **Decompiles scripts even if your executor can't** — free built-in fallback, plus a fast parallel mode for script-heavy games.
- ☀️ **Opens bright** — optional one-liner so your save isn't dark and foggy.
- 🧱 **Recovers meshes** — pull private mesh geometry out to `.obj` (Blender-ready).
- ⚡ **Fast and won't crash** — handles huge games without running out of memory.
- 🔌 **Works on any executor** — Volt, Solara, Wave, and the rest.

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

That's it — one call, no extra scripts. Every option is off by default; flip on what you want.

📖 **Full option list:** https://realslimshady2000.github.io/SaveInstance420Edition/

## Credits

Built on the original **[UniversalSynSaveInstance](https://luau.github.io/)** by the luau project — please support them.
Streaming & prepass ideas by [centerepic](https://github.com/centerepic). Decompiler by [lua.expert](https://lua.expert).

Modified by **Robloxscripts.com** — Discord: discord.robloxscripts.com
