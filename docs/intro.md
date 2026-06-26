---
sidebar_position: 1
---

# Getting Started

A modified build of **UniversalSynSaveInstance (USSI)** that correctly saves
**UnionOperations**, **Terrain**, **MeshPart colors/sizes**, **decals/images/sounds**, with optional
**full-map streaming**, a **parallel decompile prepass**, **lighting neutralization**, and a
**`.obj` mesh-geometry exporter** for recovering private meshes.

## Usage

```lua
local Params = {
    RepoURL = "https://raw.githubusercontent.com/RealSlimShady2000/SaveInstanceMODIFIEDFullUnionSupport/main/",
    SSI = "saveinstance",
}

local synsaveinstance = loadstring(game:HttpGet(Params.RepoURL .. Params.SSI .. ".luau", true), Params.SSI)()

synsaveinstance({
    -- all optional, all default false — flip to true to enable:
    SetStreaming = false,       -- force-load an entire StreamingEnabled map before saving
    DecompilePrepass = false,   -- decompile all scripts in parallel before saving (script-heavy games)
    NeutralizeLighting = false, -- open the saved place in clean daylight, not the game's dark/foggy lighting
    ExportObj = false,          -- also bake all MeshPart geometry to a .obj (recovers private meshes)
})
```

See the **[SynSaveInstance API](../api/SynSaveInstance)** for the full option list.

## What's different from normal SaveInstance

- **Unions render correctly** — `MeshData2` / `ChildData2` / `PhysicalConfigData` are saved.
- **Part Color & Size are saved** — uses the official Roblox CDN API dump (community dumps strip the
  serialized `Color3uint8` / `size` members, which made parts load grey & default-sized).
- **Decals, images & sounds are saved** — the new `Content` DataType (Image/Texture/SoundId) is handled.
- **Terrain** `SmoothGrid` / `PhysicsGrid` are serialized (and re-captured after streaming).
- **`SetStreaming`** — force-loads an entire StreamingEnabled map before saving.
- **`NeutralizeLighting`** — resets Lighting/Atmosphere/effects to clean midday.
- **`ExportObj`** — recovers private MeshPart geometry to a world-space `.obj` (Blender / Studio import).
- **`DecompilePrepass`** + **lua.expert fallback** — fast, complete decompiles on script-heavy games.

> Credit for the original SaveInstance goes to the **[luau](https://luau.github.io/)** project.
> Modified by **Robloxscripts.com** — Discord: discord.robloxscripts.com
