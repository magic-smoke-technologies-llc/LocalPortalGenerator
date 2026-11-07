# Status

## Done
- Design fully settled (`.agents/design.md`, `CONTEXT.md`).
- Mod project `PortalGeneratorPeO4A/`, content root `/PortalGeneratorPeO4A`, row prefix `OCXX2` (other rows refer to ours as `OCXX2_<row>`).
- Generator item and Blueprint built (template bed removed):
  - `Blueprints/Deployed_PortalGenerator`: child of `AbioticDeployed_Furniture_ParentBP`, `RequiresPower = true`, FurnitureMesh = `SM_CraftedTeleporter_Lodestone`, deconstructs to `OCXX2_portal_generator`. Deliberately not a child of `Deployed_TeleporterPad`, so pads and Personal Teleporters can't link to it.
  - `DataTables/ItemTable_Craftables/portal_generator`: copied from `teleporter_pad`, renamed "Local Portal Generator".
  - `recipe_PortalGenerator`: Office tier, Travel category, crafting bench, medium research.
  - `salvage_PortalGenerator`: 2-3 Tech Scrap, 0-1 Circuit Board.
- Travel proven feasible in Play (ADR 0001).
- Destination → Visited flag mapping done (`game-facts.md`).

- Confirmed in game (2026-11-07): item, placement, power, recipe under Travel; tap F on the side Terminal opens a Flathill Portal over the pad; walking in loads Flathill.
- Blueprint: `OpenPortal(Destination)` custom event + `InteractWith_B` (power-gated) calling it with "Flathill"; `CanInteractWith_B` override (Chris made it); variables `ActivePortal`, `PortalImageToUse`, `PortalBoxToUse` (Chris made them).

- Portal Anchor built (untested): item `ItemTable_Pickups/portal_anchor` (Lodestone Fragment look) → buff `OCXX2_Buff_PortalAnchor` → `Blueprints/BuffObject_PortalAnchor` sets `OCXX2_Anchored_<Destination>` (20 rows in `DataTables/DT_WorldFlags`). Recipe `recipe_PortalAnchor`.
- Generator cycle now only offers Anchored Destinations (`HasWorldFlag`), then off.

## Next
1. Recipe unlock: game unlocks a recipe only once ALL its ingredients have been picked up (`ItemsPickedUpArray`, `Server_CheckForNewInventedRecipes`). Chris wants any one ingredient to unlock the Anchor; candidate: link the Anchor recipe to the Generator's via `LinkedRecipesToUnlock`.
2. Don't consume the Anchor when used outside a Portal World or in an Anchored one (unverified whether possible); feedback message on success.
3. Buff icon (still the Reaper panic icon); portal destination label.
4. Close the Portal on power loss / packaging.
5. Tint; save/reload check (ADR 0002).
6. Terminal menu replacing cycling (design.md). Start by studying how `Deployed_DatabaseTerminal` opens `W_OperatingSystem_Main` and how apps plug in via `I_TerminalApp` / `I_TerminalUse`; route the pick to the server (e.g. `DeliverString`); test co-op.
