# Travel by moving players to the game's Entrance teleporter, found live

Every Portal World is a streaming sublevel of the always-loaded `Facility` map, so reaching one is a teleport within the same world, not a map change. The Generator moves players to the Portal World's Entrance teleporter and lets the game's own volume-based streaming and loading screen bring the world in. It finds that teleporter at runtime: `DT_Levels` row (Get Level Row) gives `EntranceTeleporter` (e.g. `fog_start`), then the `BP_Teleporter_ParentBP` actor whose `MyTeleporterID` matches it. All 20 Entrances live in the persistent `Facility` level, so they're always present. Verified in Play In Editor on 2026-11-07 (Flathill, from an unloaded state).

## Considered Options

- **Record each Entrance's position in our own table.** Simple and certain, but a game update that moves an Entrance would silently send players to a stale spot. Rejected because the live lookup was proven to work.
- **Drive the game's own portal or debug-teleport flow.** Its logic is in `/Game` Blueprints we can't inspect safely (T3D-exporting them crashes the editor), and a plain teleport turned out to be enough.

## Consequences

- A teleport fired before the game finishes starting up (save data still loading) hangs on "LOADING …" forever. The Generator must only send players once the world is fully loaded; normal play satisfies this, but test scripts that teleport right after Play starts will not.
- Actor labels such as `Portal_Fog_Start` exist only in the editor. Match on `MyTeleporterID`, never on labels.
