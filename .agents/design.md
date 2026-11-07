# Settled design

Each line was decided by Chris during the grilling session on 2026-11-07. Terms are defined in `CONTEXT.md`.

## Destinations
- Portal Worlds only; Sectors are never Destinations.
- Arrival is the Portal World's Entrance. Distant Shore and Tile have no Entrance, so they are excluded.
- Visited is shared per save. Earlier visits count wherever the game recorded them; the mod records the rest itself from install onward.

## The Generator
- A deployable placed at base, not a handheld.
- Office tier, researched. Recipe: 1 Power Cell (`powercell`), 4 Tech Scrap (`scrap_tech`), 2 Circuit Board (`circuitboard`), 1 Power Supply Unit (`powersupply`).
- Looks: the Teleporter Pad mesh with a different tint. A custom model can replace it later.
- Must be powered to open a Portal.
- Interacting opens a menu listing the Destinations plus a Close Portal option.

## The Portal
- One-way. Players come home through the Portal World's own exit.
- One Portal per Generator; choosing another Destination replaces it.
- Stays open until closed at the Generator, or until the Generator loses power.

## Naming
- Mod/project: `PortalGenerator`. In-game item name: "Local Portal Generator".
