# Destinations are unlocked by using a consumable in that world, not by having visited

Chris replaced the Visited rule (Q22): a Portal World becomes a Destination only when someone carries a consumable item there and uses it, which consumes it. Having been somewhere no longer counts. The unlock is remembered per save in our own world flags (`OCXX2_...` mod rows), since flags are the only save storage a mod can reach.

## Considered Options

- **Visited, from game flags plus patched entrance portals (ADR 0003)**: guesswork about what each game flag means, three worlds with no flag, and a runtime patch to the game's portals.
- **Visited from the game's per-level save files**: blocked by the upload filter.

## Consequences

- Every world, Flathill included, needs one trip with the consumable, even if already visited.
- No game flags, MapReveal or portal patching involved.
