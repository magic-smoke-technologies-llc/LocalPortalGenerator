# Settled design

Each line was decided by Chris during the grilling session on 2026-11-07. Terms are defined in `CONTEXT.md`.

## Destinations
- Portal Worlds only; Sectors are never Destinations.
- Arrival is the Portal World's Entrance. Distant Shore and Tile have no Entrance, so they are excluded.
- A Portal World becomes a Destination only once Anchored: someone used the consumable there (ADR 0004, Q22). Having visited doesn't count. Shared per save, permanent.
- One generic consumable (Q23): using it inside a Portal World Anchors the world you're in (`LevelManagerSubsystem.FindLatestLevelPlayerIsIn`, upload-filter allowed), recorded with `SetWorldFlag` on our `OCXX2_` flag rows.
- The consumable is called "Portal Anchor" in game (Q25).
- Anchor recipe (Chris, replacing Q24's cheap recipe): 3 Anteverse Gem (`gem`), 1 Personal Teleporter (`PersonalTeleporter`), 1 Desk Phone (`phone`), 3 Metal Scrap (`scrap_metal`); Labs tier (matches the Personal Teleporter), researched.

## The Generator
- A deployable placed at base, not a handheld.
- Office tier, researched. Recipe: 1 Power Cell (`powercell`), 4 Tech Scrap (`scrap_tech`), 2 Circuit Board (`circuitboard`), 1 Power Supply Unit (`powersupply`).
- Looks: the Teleporter Pad mesh with a different tint. A custom model can replace it later.
- Must be powered to open a Portal.
- Has a side Terminal. Tapping F on it (powered) cycles: each tap closes the current Portal and opens the next Visited Destination's Portal; after the last one the cycle goes to "off" (no Portal). Chris chose this over a menu for now (Q20).
- Planned (Chris, replaces tap-to-cycle entirely): interacting with the Terminal opens the game's in-world computer desktop with a "Portals" app listing Anchored Destinations by in-game name, plus Close Portal; picking one calls `OpenPortal`. Built on the game's terminal/OS system the way the Trader Holograms mod (mod.io 6472552) does: `Deployed_DatabaseTerminal` / `ComputerTerminal_ParentBP`, `W_OperatingSystem_Main`, `W_OsAppWrapper`, `I_TerminalApp`, `I_TerminalUse`. Cycling is removed once this works.

## The Portal
- Is the game's own portal (`BP_Teleporter_ParentBP`) spawned floating over the Generator's pad (75 cm up, Chris's tuning; beside the pad clipped into walls), copying the real portal to that world (ADR 0002). Night Realm, Arcade Winter, Salem and Snowglobe have none, so they use the default portal look.
- Entered by walking into it, exactly like the game's portals.
- One-way. Players come home through the Portal World's own exit.
- One Portal per Generator; choosing another Destination replaces it.
- Stays open until closed at the Generator, or until the Generator loses power.

## Naming
- Mod/project: `PortalGenerator`. In-game item name: "Local Portal Generator".
