# Status

## Done
- Design fully settled (`.agents/design.md`, `CONTEXT.md`).
- Mod project created from an Items template: `PortalGeneratorPeO4A/`, content root `/PortalGeneratorPeO4A`, row prefix `OCXX2`. Template assets still unchanged: `bed_PortalGenerator` (deployable row), `recipe_PortalGenerator`, `salvage_PortalGenerator`, `Blueprints/Deployed_Furniture_PortalGenerator`.
- Travel proven feasible in Play (ADR 0001).

## Next
1. Map each Destination to its game Visited flag, or mark it as needing a mod flag.
2. Turn the template into the Generator: item row (name, Teleporter Pad mesh, tint), Office-tier recipe, power requirement.
3. Build the travel logic: Destination lookup, Entrance lookup, teleport.
4. Build the Destination menu and Portal open/close/replace behaviour.
5. Visited tracking with mod world flags.
