# Pokemon Showdown Balance

Personal project: a custom, from-scratch balanced Pokemon roster (18
original mons, each a fixed 600 base stat total, a 3-type Martial/Magic/
Ranged rock-paper-scissors system) built on top of the real Pokemon
Showdown battle engine, so it can actually be playtested rather than just
theorycrafted on paper.

## Start here

- **`docs/design.md`**, the full design doc and single source of truth for
  every decision made so far: core ruleset, the 18-mon roster, base stat
  spreads, the Martial/Magic/Ranged type system, abilities, items, fixed
  movesets, the meta-currency economy, visual concepts, and names.
- **`docs/todo.md`**, what's still open right now. Read this first when
  picking the project back up.

## What this repo actually is

Cloned with full commit history from the real
[smogon/pokemon-showdown](https://github.com/smogon/pokemon-showdown) server
codebase. That upstream is kept as the `upstream` git remote (not `origin`),
so upstream fixes/updates can be pulled later and diffed against without
losing track of what's custom.

## Upstream references that still apply

Since this runs on the unmodified real PS engine for now, its own docs are
still accurate for getting a server running locally:

- [COMMANDLINE.md](./COMMANDLINE.md), running battles from the command line
- [sim/README.md](./sim/README.md), the battle simulation library
- [server/README.md](./server/README.md), running a local server
- [PROTOCOL.md](./PROTOCOL.md), client/server communication, only relevant
  if the client ever gets touched

## Status

Design phase is done for the initial 18-mon roster (see `docs/design.md`).
No engine code has been changed yet and nothing custom is implemented.
Moves currently use real, stock Pokemon Showdown moves as stand-ins for
testing (mapping is in `docs/design.md`'s Move Glossary) so the kits can be
tested without writing any new move-scripting first. Next step is wiring the
18 mons into the engine and playtesting; see `docs/todo.md` for the current
punch list.

## License and credits

This is Pokemon Showdown's own server code, distributed under the
[MIT License](./LICENSE), owned and built by Guangcong Luo (Zarel) and the
Smogon/PS team. See http://pokemonshowdown.com/credits for full credits.
Nothing in this fork changes that license or attribution.
