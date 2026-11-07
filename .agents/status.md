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

## Next
1. Destination menu (replace the hard-wired "Flathill"), with Close Portal.
2. Close the Portal when the Generator loses power or is packaged/destroyed.
3. Visited: only list Visited Destinations; set the mod flag via `WorldFlagToTriggerOnUse`.
4. Tint the Generator (material instance).
5. Check whether a spawned Portal survives save/reload (ADR 0002 open question).
