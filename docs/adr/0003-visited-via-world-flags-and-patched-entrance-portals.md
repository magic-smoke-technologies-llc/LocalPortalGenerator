# Visited comes from world flags, with Visited flags added to the game's entrance portals

A Destination is Visited when any of its game world flags is set, or our own `OCXX2_Visited_<Destination>` flag is. When a Generator loads, it fills the empty `WorldFlagToTriggerOnUse` on each Destination's real entrance portal (in the always-loaded Facility) with our flag, so normal trips through those portals record visits from then on. It never overwrites a flag the game already set (Alps, Anteverse C, Shadowgate, the Wall have their own). This is not saved into the portals; it is reapplied whenever a Generator loads. Chris chose this (Q21).

## Considered Options

- **The game's per-level save files** (`AbioticGameInstance.DoesWorldSaveExist`): exact and covers every past visit, but the upload filter blocks it, and `WorldSaveMap` / `GetWorldSaveFileList` too.
- **Game flags only**: Cabin, Rise and Botanical have none and could never be Destinations.
- **Setting our flag from our own Portal**: circular, since a Destination must already be Visited to get a Portal.

## Consequences

- Visits made before any Generator exists only count where the game flagged them.
- Worlds without a real entrance portal (Night Realm, Arcade Winter, Salem, Snowglobe) rely on game flags only.
