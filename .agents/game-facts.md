# Verified game facts

Checked in the Mod Editor (UE 5.4.4) on 2026-11-07. Re-verify after a game update.

## Levels and travel
- `DT_Levels` (`/Game/Blueprints/DataTables/Environment/DT_Levels`, row struct `LevelMetadata`): Portal Worlds have `ResettablePortalWorld = true` and an `EntranceTeleporter` name. Read a row at runtime with `LevelHandleFunctionLibrary.GetLevelRow`.
- Destinations (row → EntranceTeleporter): AnteverseA→anteverse_a_start, AnteverseB→anteverse_b_start, AnteverseC→anteverse_c_start, Flathill→fog_start, Warehouse→warehouse_start, MirrorWorld→mirrorworld_start, Alps→alps_start, Suomi→shadowgate_start, Train→train_start, Wall→wall_start, HCabin→H_Cabin_Start, Rise→rise_start, NightRealm→nightrealm_start_A, ArcadeWinter→VWinter_Start, Salem→salem_begin, V_INQ→INQ_Entrance, V_BOTANICAL→botanical_future_01, V_ISLAND→island_start, V_Snowglobe→V_Snowglobe_Start, V_SIGNAL→signal_start.
- Every Portal World map (`V_FOG`, `V_NIGHT`, …) is a `LevelStreamingDynamic` sublevel of `/Game/Maps/Facility`.
- Entrance teleporters are `BP_Teleporter_ParentBP` actors (native parent `TeleporterParent`) in the persistent Facility level, so always loaded. Their ID is the Blueprint variable `MyTeleporterID`; all 20 IDs above match one. Other variables seen in Details: `DestinationTeleporter`, `IsTeleporterActive`, `PlayersOnly`.
- Streaming is volume-based (`AbioticLevelStreamingVolume`, `LevelManagerSubsystem`). Moving a player into a Portal World's volume makes the game show "LOADING …", hold the player, and stream the world in.
- See `docs/adr/0001-travel-via-entrance-teleporters.md` for the startup-timing gotcha.

## Visited
- `WorldFlagSubsystem` (Blueprint-callable `HasWorldFlag` / `SetWorldFlag`) holds per-save flags. Mods can add flags with `WorldFlagModRowAsset`.
- In Python, get the subsystem with `unreal.find_object(None, world.get_path_name()+":WorldFlagSubsystem_0")`; `get_world_flags()` lists the set flags.
- Destination → game flags that count as Visited (any one is enough; Chris chose to include MapReveal):
  - AnteverseA: `MapReveal_AnteverseA`
  - AnteverseB: `LABS_CompletedAnteverseB`, `MapReveal_AnteverseB`
  - AnteverseC: `Plant_AnteC_Entered`
  - Flathill: `Fog_Completed`, `Flathill_CornWeb`, `MapReveal_Flathill`
  - Warehouse: `MapReveal_Warehouse`
  - MirrorWorld: `MirrorWorld_Entered`
  - Suomi: `Reactors_SG_Entered`, `MapReveal_Shadowgate`
  - Train: `TrainCompletedOnce`
  - Wall: `Residence_Wall`, `Wall_AG_met`, `MapReveal_Wall`
  - NightRealm: `NightRealm_Entered`
  - ArcadeWinter: `VWinter_Complete`, `VWinter_LamogiCave`
  - Salem: `Salem_Complete`, `Salem_MetRiggs`
  - V_INQ: `V_INQ_HastaMet`, `V_INQ_SunDiskTouched`
  - V_Snowglobe: `SnowglobeComplete`
  - V_ISLAND: `End_PostBoss_MetCahn_Island`, `End_PostBoss_MetJanet_Island`, `End_PostBoss_MetWitch_Island`, `End_PostBoss_MetRiggs_Island`
  - V_SIGNAL: `V_Signal_Entered`
  - Alps, HCabin, Rise, V_BOTANICAL: none; mod flag only.
- Rejected as evidence: `*_Opened` / `*_PortalOpened` (portal opened, not entered), `Res_EnteredBotanicals` (could be the Facility Botanical Sector), `V_INQ_Entrance` (entry point opened).
- `MapReveal_*` caveat: arriving at the Entrance does not set it, and no trigger inside V_FOG sets it (the only `Trigger_WorldFlag` is by the exit). Its source is unknown and may be outside the Portal World, so a world can appear before anyone has entered it.

## Crafting
- Recipe tiers are `RecipeTags`: `Recipe.Office`, `Recipe.Labs`, `Recipe.Manufacturing`, `Recipe.Security`, `Recipe.Dam`, `Recipe.Residences`, `Recipe.Reactors`.
- Reference recipes: `recipe_teleporterpad` (Reactors, hard research), `recipe_personalteleporter` (Labs, medium).

## Interaction and power (Blueprint interfaces on AbioticDeployed_ParentBP)
- `I_Interactable` (`/Game/Blueprints/Interfaces/I_Interactable`): on furniture, **A = F key = package** (handled by `AbioticDeployed_Furniture_ParentBP`; never override it) and **B = E key = use**. Use needs `CanInteractWith_B` returning true plus `InteractWith_B`. `InteractWith_B_LocalFX` runs on the interacting client (the Teleporter Pad opens its popup there); `DeliverString` / `DeliverInt` hand a popup's choice back. Also: `GetInteractText`, `LongInteractWith_A/B`, `RadialWheelInteractWith_A`.
- Interaction needs a collision component with profile `InteractOnly` (the Teleporter Pad's `InteractHelper` box). Our Generator has one around its side `Terminal`.
- `I_Powerable`: `IsPowered`, `TogglePowerFX`, `RequiresPowerSocket`.
- Furniture power is the `RequiresPower` variable on `AbioticDeployed_Furniture_ParentBP`.
- List a cooked Blueprint's functions by iterating `unreal.ObjectIterator(unreal.Object)` for paths starting with the class path (functions show as `<Class>_C:<Name>`).

## Editor gotchas
- Overriding an inherited function that has outputs (e.g. `CanInteractWith_B`) can't be done from Python (`add_function_graph` makes a new function, not an override) and the Override dropdown is a popup the MCP screenshot/keys can't drive. Ask Chris to do it: My Blueprint > Functions > Override.
- `build_graph` with `clear=true` then re-pasting a custom event whose name still exists in the compiled class renames the new event to `CustomEvent`. Clear, compile, then paste; or check function names afterwards.
- The Blueprint editor's Viewport preview doesn't refresh after Python adds components; spawn the class in the editor world to check real placement.
- The `abf-mod-editor` MCP tools `build_graph` and `discover_pins` probe pins in a throwaway Blueprint under `/Engine/Transient`, which the server's crash guard refused. Patched on 2026-11-07 in `%USERPROFILE%\abf-mod-editor-mcp\server.py` (`export_mod_t3d` now allows `/Engine/Transient/BP_McpProbe*`; original in `server.py.bak`). If the tool is reinstalled, the patch is lost and those tools refuse again.
- Never T3D-export a `/Game` Blueprint: it crashes the editor. Inspect a game Blueprint's variables through the Details panel of a placed instance during Play instead.
- `get_actor_label()` is editor-only; labels like `Portal_Fog_Start` don't exist in the shipped game.
- Python can't see Blueprint variables via `dir()`; `get_editor_property('MyTeleporterID')` works when you know the name.
