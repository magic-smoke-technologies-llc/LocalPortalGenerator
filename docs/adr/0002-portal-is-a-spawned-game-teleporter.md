# The Portal is the game's own teleporter, spawned beside the Generator

Chris wants the Portal to be the same portal the game uses to reach that Portal World, entered by touching it. The Generator spawns `BP_Teleporter_ParentBP` beside itself with `DestinationTeleporterID` set to the Destination's `EntranceTeleporter` (from `DT_Levels`) and `IsTeleporterActive = true`. Its look (`PortalImage`, `OverlapBoxSize`) is copied from the game's real portal whose `DestinationTeleporterID` matches. The game's teleporter then handles touch, travel, streaming and the loading screen, so we never move players ourselves. All of these settings are exposed on spawn.

## Considered Options

- **Teleport the player ourselves (ADR 0001).** Worked, but looked and felt nothing like the game's portals.

## Consequences

- Night Realm, Arcade Winter, Salem and Snowglobe have no real portal to copy; they get the default portal look (Chris's choice).
- `WorldFlagToTriggerOnUse` on the spawned portal sets a flag when someone steps through, which records Visited for us.
- Unverified: whether a spawned teleporter saves itself into the world save (`SavePortalState`) and reappears after reload.
