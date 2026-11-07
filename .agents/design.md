# Settled design

Each line was decided by Chris during the grilling session on 2026-11-07. Terms are defined in `CONTEXT.md`.

## Destinations
- Portal Worlds only; Sectors are never Destinations.
- Arrival is the Portal World's Entrance. Distant Shore and Tile have no Entrance, so they are excluded.
- A Portal World becomes a Destination only once Anchored: someone used the consumable there (ADR 0004, Q22). Having visited doesn't count. Shared per save, permanent.
- One generic consumable (Q23): using it inside a Portal World Anchors the world you're in (`LevelManagerSubsystem.FindLatestLevelPlayerIsIn`, upload-filter allowed), recorded with `SetWorldFlag` on our `OCXX2_` flag rows.

## The Generator
- A deployable placed at base, not a handheld.
- Office tier, researched. Recipe: 1 Power Cell (`powercell`), 4 Tech Scrap (`scrap_tech`), 2 Circuit Board (`circuitboard`), 1 Power Supply Unit (`powersupply`).
- Looks: the Teleporter Pad mesh with a different tint. A custom model can replace it later.
- Must be powered to open a Portal.
- Has a side Terminal. Tapping F on it (powered) cycles: each tap closes the current Portal and opens the next Visited Destination's Portal; after the last one the cycle goes to "off" (no Portal). Chris chose this over a menu for now (Q20).
- Later upgrade: a list popup widget (Chris will do the widget layout by hand). `OpenPortal(Destination)` stays as the entry point so only the tap logic changes.

## The Portal
- Is the game's own portal (`BP_Teleporter_ParentBP`) spawned floating over the Generator's pad (75 cm up, Chris's tuning; beside the pad clipped into walls), copying the real portal to that world (ADR 0002). Night Realm, Arcade Winter, Salem and Snowglobe have none, so they use the default portal look.
- Entered by walking into it, exactly like the game's portals.
- One-way. Players come home through the Portal World's own exit.
- One Portal per Generator; choosing another Destination replaces it.
- Stays open until closed at the Generator, or until the Generator loses power.

## Naming
- Mod/project: `PortalGenerator`. In-game item name: "Local Portal Generator".
