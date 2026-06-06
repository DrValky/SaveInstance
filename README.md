# SaveInstance (Modified) — Full Union & Terrain Support

A modified build of [UniversalSynSaveInstance (USSI)](https://github.com/luau/UniversalSynSaveInstance) with fixes for correctly saving **UnionOperations** (CSG `MeshData2` geometry) and **Terrain** (`SmoothGrid` / `PhysicsGrid`).

## Usage

```lua
local Params = {
    RepoURL = "https://raw.githubusercontent.com/RealSlimShady2000/SaveInstanceMODIFIEDFullUnionSupport/main/",
    SSI = "saveinstance",
}

local synsaveinstance = loadstring(game:HttpGet(Params.RepoURL .. Params.SSI .. ".luau", true), Params.SSI)()

local Options = { safemode = false } -- Docs: https://luau.github.io/UniversalSynSaveInstance/api/SynSaveInstance
synsaveinstance(Options)
```

## What's different from the normal save instance

- **Unions render correctly.** Re-enabled `gethiddenproperty` during the save (it was being disabled unconditionally) so the union's `MeshData2` is actually read, and stopped `IgnoreSharedStrings` from dropping the `MeshData2` / `ChildData2` SharedStrings. On executors that can't read union mesh data, unions fall back to a visible bounding-box Part instead of being invisible.
- **Terrain** `SmoothGrid` / `PhysicsGrid` are serialized.
- **`SetStreaming`** — optionally force-loads an entire `StreamingEnabled` map before saving (see below).
- **Faster, lighter saves** — the file is assembled with a table buffer instead of repeated string concatenation, fixing the `O(n²)` growth that caused "not enough memory" on large games.
- A progress bar accompanies the on-screen save status.

> Note: `ChildData` is `NotReplicated`, so client-side saves render unions but can't make them editable/separable in Studio.

## Map streaming (StreamingEnabled games)

Many big maps use **StreamingEnabled**, which only loads the chunks near your character — so a normal save captures just a fraction of the map. Set `SetStreaming = true` and the tool sweeps the whole map (pinning loaded content so it can't stream back out) **before** saving, so you get the entire thing in one shot — no flying around manually.

```lua
local Options = {
    SetStreaming = true, -- force-load the whole map first, then save
    -- optional tuning (defaults shown):
    -- StreamingAreaSize = 10000,  -- studs swept around your start position
    -- StreamingRadius = 1024,     -- per-request radius (auto-detected when possible)
    -- StreamingConcurrency = 8,   -- requests kept in flight (higher = faster, more load)
    -- StreamingSlices = 2,        -- vertical layers (raise for tall maps)
    -- StreamingTimeout = 20,
}
synsaveinstance(Options)
```

Runs headlessly (progress shows in the save status bar), then saving begins automatically. Expect lag on large maps while it streams. This integrates and speeds up the approach from [centerepic/Streamer7](https://github.com/centerepic/Streamer7) — instead of teleport-and-poll per chunk, it fans out concurrent `RequestStreamAroundAsync` requests that each yield when their region is loaded.

## Credits

All credit for the original SaveInstance goes to the **luau** project — please support them:

- Project home & docs: **[luau.github.io](https://luau.github.io/)**
- Source: [luau/UniversalSynSaveInstance](https://github.com/luau/UniversalSynSaveInstance)
- API reference: [luau.github.io/UniversalSynSaveInstance/api/SynSaveInstance](https://luau.github.io/UniversalSynSaveInstance/api/SynSaveInstance)

Modified by **Robloxscripts.com** — Discord: discord.robloxscripts.com
