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
- Game flags seen for visits: `NightRealm_Entered`, `MirrorWorld_Entered`, `Tile_Entered`, `V_Signal_Entered`, `MapReveal_Flathill`, `Voussoir_Entered`. The full Destination → flag mapping is still to do.

## Crafting
- Recipe tiers are `RecipeTags`: `Recipe.Office`, `Recipe.Labs`, `Recipe.Manufacturing`, `Recipe.Security`, `Recipe.Dam`, `Recipe.Residences`, `Recipe.Reactors`.
- Reference recipes: `recipe_teleporterpad` (Reactors, hard research), `recipe_personalteleporter` (Labs, medium).

## Editor gotchas
- Never T3D-export a `/Game` Blueprint: it crashes the editor. Inspect a game Blueprint's variables through the Details panel of a placed instance during Play instead.
- `get_actor_label()` is editor-only; labels like `Portal_Fog_Start` don't exist in the shipped game.
- Python can't see Blueprint variables via `dir()`; `get_editor_property('MyTeleporterID')` works when you know the name.
