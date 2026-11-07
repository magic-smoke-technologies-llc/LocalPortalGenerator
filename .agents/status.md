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

## Next
1. Confirm in-game: item, placement, mesh, power prompt, recipe. Then the tint (needs a material instance).
2. Build the travel logic: Destination lookup, Entrance lookup, teleport.
3. Build the Destination menu and Portal open/close/replace behaviour.
4. Visited tracking with mod world flags.
