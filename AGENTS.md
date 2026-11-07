# PortalGenerator

Abiotic Factor mod: a craftable deployable that opens a one-way Portal to any Visited Portal World. Built with the Abiotic Factor Mod Editor (MCP server `abiotic-mod-editor`).

- **Vocabulary**: `CONTEXT.md` is the glossary. Use its terms (Portal World, Sector, Entrance, Visited, Destination, Generator, Portal) in code, assets and conversation.
- **Decisions**: `docs/adr/` holds the hard-to-reverse ones; `.agents/design.md` holds every settled design choice. Read both before changing behaviour.
- **Game internals**: `.agents/game-facts.md` lists verified tables, classes, functions and gotchas. Read it before searching the game again.
- **Where we are**: `.agents/status.md` holds progress and next steps. Update it at the end of every session.

## Layout

- Repo root: docs and agent notes only.
- `PortalGeneratorPeO4A/`: the mod project. Upload zips this whole folder and mod.io rejects `.md` files, so keep every document at the repo root.

## Working rules

- Commit after each settled decision or working step, with a message saying what changed.
- Test with the `test_mod` tool, then tell the user exactly what to check in the game window.
- The user clicks every upload button.
