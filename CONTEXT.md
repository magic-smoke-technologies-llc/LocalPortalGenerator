# Local Portal Generator

An Abiotic Factor mod: a craftable machine that opens a portal to any Portal World the players have Anchored, so they don't have to travel there the long way.

## Language

**Generator**:
The craftable deployable a player builds and places at base. It is the only way to open a Portal, must be powered to do so, and has at most one Portal open at a time.
_Avoid_: Portal generator item, device, machine, teleporter

**Portal**:
The game's own portal, spawned by a Generator over its pad and entered by walking into it, leading one way to one chosen Portal World's Entrance. It stays open until someone closes it at the Generator or the Generator loses power. Coming back uses that Portal World's own exit.
_Avoid_: Gate, rift, teleporter, warp

**Portal World**:
A separate place reached through a portal, such as Flathill, The Night Realm or Dunkeltaler Forest. Players know them by their in-game names (see `.agents/game-facts.md`), not the game's internal row names. These are the only destinations the generator can reach.
_Avoid_: World, level, map, vignette

**Entrance**:
The fixed spot in a Portal World where a traveller arrives, the same spot its own portal lands you. A Portal World without an Entrance (Distant Shore, Tile) is not a destination.
_Avoid_: Spawn, start point, landing

**Portal Anchor**:
The craftable consumable that, used inside a Portal World, makes that world Anchored. Used up on success.
_Avoid_: Beacon, key, token

**Anchored**:
A Portal World is Anchored once someone has used a Portal Anchor there. Shared by every player in that save, and permanent.
_Avoid_: Visited, discovered, unlocked

**Destination**:
A Portal World that has been Anchored and has an Entrance. The Generator cycles through exactly the Destinations.
_Avoid_: Target, location, option

**Sector**:
A part of the Facility, such as Office, Labs, Dam or Security. Sectors are not destinations for the generator.
_Avoid_: World, area, zone
