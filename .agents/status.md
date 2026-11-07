# Status

## Done
- Design fully settled (`.agents/design.md`, `CONTEXT.md`).
- Mod project created from an Items template: `PortalGeneratorPeO4A/`, content root `/PortalGeneratorPeO4A`, row prefix `OCXX2`. Template assets still unchanged: `bed_PortalGenerator` (deployable row), `recipe_PortalGenerator`, `salvage_PortalGenerator`, `Blueprints/Deployed_Furniture_PortalGenerator`.
- Travel proven feasible in Play (ADR 0001).
- Destination → Visited flag mapping done (`game-facts.md`).

## Next
1. Turn the template into the Generator: item row (name, Teleporter Pad mesh, tint), Office-tier recipe, power requirement.
2. Build the travel logic: Destination lookup, Entrance lookup, teleport.
3. Build the Destination menu and Portal open/close/replace behaviour.
4. Visited tracking with mod world flags.
