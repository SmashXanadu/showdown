# Todo

Full design doc: `docs/design.md`. Read that first when resuming, it's the
single source of truth for every decision made so far (ruleset, roster, BST
spreads, types, abilities, items, movesets, economy, visual concepts,
names).

## Open design decisions

- Reconsider the "Prism Shards" currency name. It was picked back when types
  were still an elemental placeholder (Fire/Water/Grass); it may not fit the
  finalized Martial/Magic/Ranged combat-triangle identity.
- Set exact prices: held items, and the ability-change consumable
  (re-capsuling is unlimited-use but should carry a significant cost per
  use, the cost is the intended balance lever).

## Deliberately deferred, do not start yet

- Move/ability flavor naming pass: move and ability names (Cinder Burst,
  Riptide Crash, Tidal Surge, Verdant Pulse, etc.) still carry old
  Fire/Water/Grass flavor left over from before the Martial/Magic/Ranged
  rename. Their type category assignments are already correct, only the
  names/flavor text needs updating. Explicitly held off until after
  hands-on testing, not an oversight.

## Not started

- Implementing any of this in the actual Pokemon Showdown codebase (stats,
  types, abilities, moves, items for the 18 mons). Everything so far is
  design-only in `docs/design.md`, no code has been written or committed.
