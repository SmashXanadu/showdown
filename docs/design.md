# Custom Pokemon Balance Project, Design Doc

## Core Ruleset

- **Base Stat Total:** fixed at 600 for every mon. No EVs, no IVs. Since every
  mon shares the same power budget, the *distribution shape* of those 600
  points (plus ability and movepool) is the only thing that differentiates
  one mon from another, not raw stat total.
- **Kit:** each mon gets exactly 1 passive ability + 4 moves + 1 held item.
  Moves are permanently locked per mon, the player never picks or swaps a
  mon's moves. Abilities and items are different: both use a swappable
  shared-pool model (see Meta-Economy).
- **Type system:** 3-type rock-paper-scissors wheel, single-type only (no
  dual-typing), for maximum matchup clarity. Standard multipliers apply:
  2x super effective / 1x neutral / 0.5x resisted, with **no immunities**.
  True RPS has no "doesn't affect you" case, so none exists here. Any
  Water-Absorb-style absorb/immunity interaction should be built as a
  specific mon's *signature ability* (a rare, memorable exception), never a
  system-wide type-chart rule.
  - **Type names: Martial / Magic / Ranged.** Wheel: **Martial beats Ranged,
    Ranged beats Magic, Magic beats Martial**, a combat-role triangle (melee
    closes the gap on ranged; ranged snipes the caster before the spell
    resolves; magic's burst/control drops the fighter before it closes in).
    Chosen instead of an elemental trio so the identity reads as original
    rather than a Pokemon reskin.
  - **Coverage rule:** an attacker's own STAB is always resisted by the type
    that beats it, and that resister is in turn beaten by the attacker's own
    type's prey. Concretely: **Martial attackers want Ranged coverage,
    Ranged attackers want Magic coverage, Magic attackers want Martial
    coverage.**
  - **Move/ability flavor naming pass, deliberately deferred:** move and
    ability names (Cinder Burst, Riptide Crash, Tidal Surge, Verdant Pulse,
    etc.) still carry leftover Fire/Water/Grass elemental flavor from before
    the Martial/Magic/Ranged rename. Their type category assignment is
    already correct (see the Type column below and the Move Glossary), only
    the flavor text is stale. Fixing this is intentionally on hold until
    after hands-on testing, see Open/Not Yet Decided. In the meantime, the
    Move Glossary lists a real Pokemon Showdown move to stand in for each
    custom move during testing, so implementation isn't blocked on naming.
- **Roster size:** 18 mons. Chosen for symmetry, 6 mons per type exactly,
  after starting from a 20-mon draft that split 7/7/6 and turned out to be
  one asymmetric type too many. Confirmed good as-is; no further adds/cuts
  planned until testing surfaces a reason to revisit.
- **No em dashes in any project content.** Standing style rule: use commas,
  colons, parentheses, or separate sentences instead.

## Roster

Distilled from Smogon's official ADV (Gen 3) OU Threat List
(smogon.com/rs/articles/adv_threatlist), merging pokemon that represent the
same underlying playstyle so the roster has no redundant picks. Baton Pass
support (originally its own slot, inspired by Vaporeon/Umbreon/Jolteon) was
cut entirely, not represented in this game at all.

Original numbering (1-20) is kept as stable IDs even though 2 slots were cut
later, so every cross-reference elsewhere in this doc still points at the
same mon. **#11 and #16 are cut**: gaps in the numbering are intentional,
not missing rows. Every stat spread sums to exactly 600, and none duplicates
a real Pokemon's exact base stats (four slots originally matched Tyranitar,
Celebi, Salamence, and Metagross exactly by coincidence, since those four
happen to already be 600 BST with a shape that fit; all four were
deliberately perturbed to avoid the duplication).

| # | Name | Type | Playstyle | HP | Atk | Def | SpA | SpD | Spe | Ability | Item | Gen 3 inspiration |
|---|---|---|---|--:|--:|--:|--:|--:|--:|---|---|---|
| 1 | Kethrax | Magic | Weather setter, mixed wallbreaker | 100 | 130 | 114 | 95 | 100 | 61 | Tidal Surge | Life Orb | Tyranitar |
| 2 | Harmund | Magic | Physical wall + hazard/phaze | 120 | 70 | 170 | 50 | 100 | 90 | Bulwark | Leftovers | Skarmory |
| 3 | Aswin | Martial | Special wall + cleric | 190 | 30 | 30 | 130 | 140 | 80 | Purifying Aura | Leftovers | Blissey |
| 4 | Tolmar | Ranged | Bulky setup wall to sweeper | 100 | 60 | 120 | 110 | 120 | 90 | Steady Growth | Leftovers | Suicune |
| 5 | Rane | Ranged | Dedicated counter-attacker (checks #1) | 110 | 130 | 120 | 40 | 110 | 90 | Overgrowth Ward | Rocky Helmet | Swampert |
| 6 | Sundra | Ranged | Dual-role pivot (support or sweeper) | 105 | 95 | 100 | 105 | 95 | 100 | Adaptive Instinct | Sitrus Berry | Celebi |
| 7 | Caldrek | Magic | Bulky setup sweeper, resists own answers | 95 | 130 | 80 | 115 | 80 | 100 | Momentum | Weakness Policy | Salamence / Gyarados |
| 8 | Dresh | Martial | Glass-cannon Choice wallbreaker | 110 | 200 | 60 | 30 | 80 | 120 | Overheat Drive | Choice Band | Medicham / Heracross / Slaking |
| 9 | Ixara | Martial | Fast special setup sweeper | 100 | 30 | 65 | 175 | 90 | 140 | Static Charge | Life Orb | Raikou / Jirachi |
| 10 | Morvex | Magic | Ability-based trapper | 120 | 90 | 110 | 50 | 100 | 130 | Undertow | Rocky Helmet | Dugtrio / Magneton |
| 12 | Fiorel | Magic | Offensive pivot spinner (fast, dual-purpose) | 75 | 60 | 90 | 130 | 90 | 155 | Rapid Current | Heavy-Duty Boots | Starmie |
| 13 | Grix | Martial | Defensive hazard setter + spin support (max bulk) | 110 | 110 | 150 | 30 | 100 | 100 | Iron Hide | Leftovers | Forretress |
| 14 | Nyseth | Ranged | Disruption/status ghost | 100 | 50 | 100 | 130 | 130 | 90 | Unnerve Field | Leftovers | Dusclops / Gengar |
| 15 | Pryn | Ranged | Sleep-enable + breaker combo | 90 | 170 | 90 | 30 | 90 | 130 | Focus Drive | Focus Sash | Breloom |
| 17 | Elgorath | Martial | Slow bulky setup attacker | 185 | 130 | 95 | 40 | 120 | 30 | Juggernaut | Leftovers | Snorlax |
| 18 | Onder | Ranged | Stall-loop defensive attacker | 120 | 50 | 100 | 140 | 100 | 90 | Undying Will | Leftovers | Zapdos |
| 19 | Brune | Magic | Sacrificial nuke | 85 | 135 | 125 | 95 | 90 | 70 | Detonation Core | Life Orb | Metagross |
| 20 | Vash | Martial | Speed-based cleaner | 85 | 130 | 65 | 45 | 75 | 200 | Adrenaline Rush | Focus Sash | Aerodactyl |

**Type distribution** (kept as a quick-glance summary alongside the flat
table above, since it answers a different question, whether each type is a
viable self-contained team):

| Type | Mons (#) |
|---|---|
| Magic | 1, 2, 7, 10, 12, 19 |
| Ranged | 4, 5, 6, 14, 15, 18 |
| Martial | 3, 8, 9, 13, 17, 20 |

**Notes:**

- **#5 and #7's counter identity comes from stats/ability, not typing.** In
  real Gen 3, Swampert counters Tyranitar via a typing immunity (Ground
  no-sells Electric) and Salamence/Gyarados "resist their own answers" via
  dual-typing quirks. Neither mechanic exists in a 3-type, no-immunity,
  single-type wheel. Instead, #5 (Ranged) was deliberately assigned as the
  type that beats #1's type (Magic) in the wheel, giving it a real
  mechanical hard counter (2x damage, 0.5x taken) without needing an
  immunity. #7's identity had no equivalent typing fix available and relies
  purely on stats/ability.
- **Balance flag, #10 (ability-based trapper):** in real Gen 3, Dugtrio and
  Magneton offset a game-warping trapping ability by being deliberately
  weak everywhere else (Dugtrio is only 365 BST). That discount isn't
  available here since every mon is forced to 600, so #10 got a moderate,
  support-shaped spread instead of a specialist one. Its actual balance has
  to come from the ability/movepool design, not stats. Its ability
  (Undertow, an unconditional no-escape trap) is the single most
  game-warping mechanic in the whole kit list. If early testing shows it's
  oppressive, the first lever to pull is conditioning the trap (e.g. only
  traps mons below an HP threshold, or only lasts N turns), not removing it
  outright. This is also why ability-change consumables are restricted to
  the shared pool only, see Meta-Economy: transplanting Undertow onto a
  high-Attack mon like #8 (200 Atk) via consumable would likely be
  uncounterable.

## Ability Glossary

Ability names are original, not reused from real Pokemon, even where the
underlying mechanic echoes a familiar one (noted inline for implementation
reference). Signature abilities stay locked to their original mon; only
shared-pool abilities (marked "Pool only" below) are valid targets for an
ability-change consumable.

| Ability | Effect | Default for |
|---|---|---|
| Tidal Surge | Summons a 5-turn Rain field on switch-in (Water moves x1.5, Fire moves x0.5, team-wide) | #1 Kethrax |
| Bulwark | Survives any hit from full HP with 1 HP left (Sturdy-style) | #2 Harmund |
| Purifying Aura | Cures its own status on switch-out (Natural Cure-style) | #3 Aswin |
| Steady Growth | +1 Sp. Atk at the end of each turn on field, max +3 | #4 Tolmar |
| Overgrowth Ward | Attack rises sharply, once, when HP first drops below 1/3 | #5 Rane |
| Adaptive Instinct | Takes 25% less damage from the first hit after switching in | #6 Sundra |
| Momentum | Offensive stat that scored the KO rises 1 stage after any KO (Moxie-style) | #7 Caldrek |
| Overheat Drive | Attack x1.5 while statused; burn does not reduce its Attack (Guts-style, no downside) | #8 Dresh |
| Static Charge | +1 Speed at the end of each turn on field (Speed Boost-style) | #9 Ixara |
| Undertow | Opposing active mon cannot switch out while this mon is active (Arena Trap-style) | #10 Morvex |
| Rapid Current | Its Speed cannot be lowered by opponents' moves/abilities | #12 Fiorel |
| Iron Hide | Takes 20% less damage from contact moves | #13 Grix |
| Unnerve Field | Opposing mons cannot consume held Berries while this mon is active (Unnerve-style) | #14 Nyseth |
| Focus Drive | Moves with power 60 or less deal 1.5x damage (Technician-style) | #15 Pryn |
| Juggernaut | Stat boosts from its own moves cannot be lowered by opponents | #17 Elgorath |
| Undying Will | Once per battle, survives a KO hit with 1 HP | #18 Onder |
| Detonation Core | If KO'd by a contact move, deals 25% of the attacker's max HP back (Aftermath-style) | #19 Brune |
| Adrenaline Rush | Its Speed cannot be lowered by status or opponents' effects | #20 Vash |
| Featherweight | Takes no recoil damage from its own moves | Pool only |
| Iron Will | Cannot be made to flinch | Pool only |
| Steel Nerve | Immune to confusion, infatuation, and flinching | Pool only |
| Thick Hide | Takes 25% less damage from super-effective hits | Pool only |
| Cleanse Step | Removes all hazards from its own side on switch-in | Pool only |
| Grit | Attack and Sp. Atk cannot be lowered by opponents | Pool only |
| Steadfast Guard | Defense and Sp. Def cannot be lowered by opponents | Pool only |
| Quickstep | Moves first in its priority bracket while at full HP | Pool only |
| Renewal | Restores 33% max HP when switching out | Pool only |
| Toughen Up | Def and Sp. Def each rise 1 stage the first time it takes damage in a battle | Pool only |
| Wounded Fury | Attack rises 1 stage whenever it drops below 50% HP, repeatable | Pool only |

## Item Glossary

All items reuse standard competitive-item mechanics directly since those are
generic genre vocabulary, not mon-specific flavor, and Pokemon Showdown
already implements them. Every signature item below is also a normal member
of the shared pool, there's no separate "signature-only" item category, a
mon's signature item is just its default loadout.

| Item | Effect | Default for |
|---|---|---|
| Leftovers | Restore 1/16 max HP each turn | #2, #3, #4, #13, #14, #17, #18 |
| Life Orb | +30% move power; 10% recoil per hit | #1, #9, #19 |
| Choice Band | +50% Attack; locked into first move used | #8 |
| Choice Specs | +50% Sp. Atk; locked into first move used | Pool only |
| Choice Scarf | +50% Speed; locked into first move used | Pool only |
| Assault Vest | +50% Sp. Def; cannot use status moves | Pool only |
| Rocky Helmet | Contact attackers take 1/6 max HP damage | #5, #10 |
| Focus Sash | Survives a hit that would KO it from full HP, left at 1 HP | #15, #20 |
| Heavy-Duty Boots | Immune to all entry-hazard effects on switch-in | #12 |
| Sitrus Berry | Restores 25% max HP once, when HP drops below half | #6 |
| Weakness Policy | +2 Atk and +2 Sp. Atk once, when hit by a super-effective move | #7 |
| Expert Belt | +20% power when the move isn't resisted by the target | Pool only |
| Shell Bell | Restores 12.5% of damage dealt as HP each hit | Pool only |
| Toxic Orb | Badly poisons the holder after 1 turn (synergy with #8's Overheat Drive) | Pool only |

## Move Glossary

Moves are permanently fixed per mon (see Movesets below), never
player-chosen. The **Testing stand-in** column is a real, already-implemented
Pokemon Showdown move used in place of the custom name for hands-on testing,
so implementation isn't blocked on the deferred naming pass. Power/effect
may differ slightly from the custom design values, that's expected and gets
tuned later; the point is to test the kit shape with zero new move-scripting
required. Status moves with no listed type are universal, any mon regardless
of its own type can use them.

| Move | Type | Category | Power | Effect | Testing stand-in | Used by |
|---|---|---|--:|---|---|---|
| Riptide Crash | Magic | Physical | 110 | STAB | Wave Crash | #1 |
| Cinder Burst | Martial | Special | 90 | Coverage | Flamethrower | #1 |
| War Cry | (any) | Status | | +1 Atk, +1 Spe (self) | Dragon Dance | #1, #5 |
| Recover | (any) | Status | | Heal self 50% max HP | Recover | #1, #2, #3, #4, #5, #6, #7, #9, #10, #12, #13, #17, #19 |
| Riptide Slam | Magic | Physical | 65 | STAB | Waterfall | #2 |
| Barricade Spikes | (any) | Status | | Stacking hazard, damages opposing switch-ins | Spikes | #2, #13 |
| Retreat Call | (any) | Status | | Forces the target to switch out | Whirlwind | #2, #14 |
| Scorch Wave | Martial | Special | 85 | STAB, may burn | Lava Plume | #3 |
| Cleansing Wave | (any) | Status | | Cures the user's own status | Refresh | #3 |
| Toxic Bloom | (any) | Status | | Badly poisons the target | Toxic | #3, #10, #14 |
| Verdant Pulse | Ranged | Special | 90 | STAB | Energy Ball | #4 |
| Tidewave | Magic | Special | 85 | Coverage | Scald | #4 |
| Focus Mind | (any) | Status | | +1 SpA, +1 SpD (self) | Calm Mind | #4, #6, #9 |
| Bramble Slam | Ranged | Physical | 95 | STAB | Power Whip | #5 |
| Torrent Fang | Magic | Physical | 85 | Coverage | Liquidation | #5 |
| Bloom Beam | Ranged | Special | 80 | STAB | Giga Drain | #6 |
| Tidal Pulse | Magic | Special | 80 | Coverage | Scald | #6 |
| Torrent Crush | Magic | Physical | 100 | STAB | Crabhammer | #7 |
| Sharpen Claws | (any) | Status | | +2 Atk (self) | Swords Dance | #7, #8, #20 |
| Cinder Fang | Martial | Physical | 90 | Coverage | Blaze Kick | #7 |
| Inferno Slam | Martial | Physical | 120 | STAB | Flare Blitz | #8 |
| Ashen Fang | Martial | Physical | 95 | STAB, flinch chance | Fire Fang | #8 |
| Bramble Fist | Ranged | Physical | 100 | Coverage | Wood Hammer | #8 |
| Blaze Beam | Martial | Special | 95 | STAB | Heat Wave | #9 |
| Thorn Burst | Ranged | Special | 90 | Coverage | Petal Blizzard | #9 |
| Riptide Fang | Magic | Physical | 85 | STAB | Aqua Tail | #10 |
| Cinder Snap | Martial | Physical | 85 | Coverage | Blaze Kick | #10 |
| Tidal Beam | Magic | Special | 90 | STAB | Muddy Water | #12 |
| Cinder Spark | Martial | Special | 85 | Coverage | Mystical Fire | #12 |
| Clear Tide | (any) | Status | | Removes all hazards from the user's side | Rapid Spin | #12, #13 |
| Ember Crush | Martial | Physical | 85 | STAB | Blaze Kick | #13 |
| Bloom Shade | Ranged | Special | 85 | STAB, debuff chance | Petal Blizzard | #14 |
| Tide Veil | Magic | Special | 80 | Coverage | Scald | #14 |
| Slumber Spores | Ranged | Status | | Exclusive sleep move, not in the universal pool | Spore | #15 |
| Thorn Jab | Ranged | Physical | 60 | Priority | Grassy Glide (terrain-dependent in real PS, flag for custom scripting later) | #15 |
| Thorn Focus | Ranged | Physical | 130 | STAB | Wood Hammer | #15 |
| Tide Fist | Magic | Physical | 90 | Coverage | Aqua Tail | #15 |
| Magma Slam | Martial | Physical | 90 | STAB | Fire Punch | #17 |
| Grim Resolve | (any) | Status | | Spe -1, Atk +2, Def +2 (self) | Curse | #17 |
| Thorn Crush | Ranged | Physical | 85 | Coverage | Seed Bomb | #17 |
| Thorn Pulse | Ranged | Special | 85 | STAB | Energy Ball | #18 |
| Mire Bolt | Magic | Special | 90 | Coverage | Muddy Water | #18 |
| Restful Slumber | (any) | Status | | User sleeps, but fully heals HP and status | Rest | #18 |
| Dream Action | (any) | Status | | While asleep, automatically executes a random other move in the set | Sleep Talk | #18 |
| Torrent Slam | Magic | Physical | 90 | STAB | Aqua Tail | #19 |
| Cinder Crush | Martial | Physical | 85 | Coverage | Blaze Kick | #19 |
| Last Resort Blast | (any) | Status/self-KO | | Self-KO, heavy damage to target | Explosion | #19 |
| Tidal Fang | Magic | Physical | 90 | STAB, flinch chance | Waterfall | #20 |
| Cinder Slash | Martial | Physical | 85 | Coverage | Blaze Kick | #20 |
| Shield Up | (any) | Status | | Blocks all damage/effects this turn | Protect | #20 |

**Currently unused** (defined but not on any of the 18 movesets, available if
the roster grows later):

| Move | Effect | Testing stand-in |
|---|---|---|
| Scorch | Burns the target | Will-O-Wisp |
| Barrier Wall | +1 Def, +1 SpD (self) | Cosmic Power |
| Guard Break | -1 Def, -1 SpD (target) | No clean real-move match found; would need custom scripting if ever used |
| Mirror Image | Creates a decoy (Substitute-style) | Substitute |

## Movesets

Each mon's exact 4 moves are permanently locked, chosen from its signature
attacks plus whichever glossary moves the archetype actually needs to
function (e.g. #18 needs Restful Slumber + Dream Action together as one
unit, that's the RestTalk loop; #2 needs its hazard + phaze + recovery all
at once). Full type/power/effect for each move is in the Move Glossary
above; this table just lists names.

| # | Name | Moveset (4) |
|---|---|---|
| 1 | Kethrax | Riptide Crash, Cinder Burst, War Cry, Recover |
| 2 | Harmund | Riptide Slam, Barricade Spikes, Retreat Call, Recover |
| 3 | Aswin | Scorch Wave, Recover, Cleansing Wave, Toxic Bloom |
| 4 | Tolmar | Verdant Pulse, Tidewave, Focus Mind, Recover |
| 5 | Rane | Bramble Slam, Torrent Fang, War Cry, Recover |
| 6 | Sundra | Bloom Beam, Tidal Pulse, Focus Mind, Recover |
| 7 | Caldrek | Torrent Crush, Sharpen Claws, Cinder Fang, Recover |
| 8 | Dresh | Inferno Slam, Ashen Fang, Bramble Fist, Sharpen Claws |
| 9 | Ixara | Blaze Beam, Thorn Burst, Focus Mind, Recover |
| 10 | Morvex | Riptide Fang, Cinder Snap, Toxic Bloom, Recover |
| 12 | Fiorel | Tidal Beam, Cinder Spark, Clear Tide, Recover |
| 13 | Grix | Ember Crush, Barricade Spikes, Clear Tide, Recover |
| 14 | Nyseth | Bloom Shade, Tide Veil, Retreat Call, Toxic Bloom |
| 15 | Pryn | Slumber Spores, Thorn Jab, Thorn Focus, Tide Fist |
| 17 | Elgorath | Magma Slam, Grim Resolve, Thorn Crush, Recover |
| 18 | Onder | Thorn Pulse, Mire Bolt, Restful Slumber, Dream Action |
| 19 | Brune | Torrent Slam, Cinder Crush, Last Resort Blast, Recover |
| 20 | Vash | Tidal Fang, Cinder Slash, Sharpen Claws, Shield Up |

**Notes:**

- **#8:** Sharpen Claws is a slightly awkward fit alongside Choice Band
  (setup and move-lock don't really synergize), kept deliberately anyway so
  the mon isn't dead weight if it's ever given a different item via the
  swappable item pool.
- **Movepool review (2026-09-22):** checked all 18 fixed movesets for
  coverage gaps. #2, #3, and #13 have no coverage move and are hard-walled
  by their counter type, intentional, since they're wall/support archetypes
  and this is the RPS system working as designed. #6 had the same gap but
  its archetype (meant to have no glaring weakness) made it a real problem,
  fixed by swapping in Tidal Pulse for coverage. #18 was also found to be
  mistyped during the type/moveset cross-check (assigned Ranged but had a
  Martial STAB move), fixed by making Thorn Pulse its STAB and adding a new
  Magic-type coverage move, Mire Bolt. Both fixes are reflected in the
  tables above.

## Meta-Economy: Currency, Items & Ability Changes

Items and ability changes are earned/purchased with a meta currency, but
behave differently once acquired:

- **Held items** are bought once, then owned permanently and can be freely
  equipped to/removed from any mon at no further cost, standard "Bag item"
  behavior, drawn from the Item Glossary above.
- **Ability changes** are a consumable (real-Pokemon equivalent: Ability
  Capsule). Using one permanently overwrites a mon's current ability with a
  different one. A mon can be re-capsuled as many times as the player wants,
  there is no hard cap, but each use carries a significant currency cost.
  The cost is the intended balance lever, not a usage limit.
- **Currency is earned through battle wins.** Win streaks grant a bonus that
  increases the longer the streak runs, rewarding sustained play over
  one-off wins.
- **Balance guardrail (important):** ability-change consumables may only
  assign an ability from the shared pool (marked "Pool only" in the Ability
  Glossary), never another mon's signature ability. See the balance flag on
  #10 above for why.

**Open:** currency name. "Prism Shards" was suggested when types were still
an elemental placeholder; "prism" nods at light splitting into colors, which
doesn't connect as cleanly to a Martial/Magic/Ranged combat triangle. Worth
reconsidering. Exact prices for items and ability-change consumables are
also still undecided.

## Visual Concepts

Direction: MOBA-style hero design rather than cute-creature Pokemon
aesthetics. Each mon should read from silhouette alone, and each of the
three types has its own non-elemental visual language. Descriptions below
are single, static poses suitable as sprite art reference, not depictions of
change over time.

**Type-level visual language:**

- **Martial**: forged and grounded. Physical bodies of muscle, bone, stone,
  or metal; tangible weapons (blades, hammers, fists); heavy material
  culture. Palette: iron grey, bronze, granite, bone white, warm neutrals.
- **Magic**: ethereal and arcane. Partially incorporeal, geometric/runic
  markings, floating elements, power channeled through gesture, sigil, or
  glow rather than a held weapon. Palette: violet, deep blue, silver,
  void-black; cool, otherworldly, asymmetric.
- **Ranged**: precise and mechanical-agile. Lean, aerodynamic builds, tools
  of tension and distance (bows, throwing blades, coiled cable/sinew),
  exposed joint/mechanism detail. Palette: slate, bronze, sand, muted
  practical tones with one sharp accent.

### Martial (3, 8, 9, 13, 17, 20)

- **#3 Aswin**: hooded ascetic in bandage-wrapped robes, standing with palms
  open at chest height, a soft warm glow between the palms. No weapon, no
  armor. Bone-white wrappings, dull gold trim.
- **#8 Dresh**: hulking armored brute, one massive cleaver fused to its right
  arm, weapon dragging low, broad low stance. Dark iron plating over corded
  muscle, one glowing orange seam down the blade.
- **#9 Ixara**: whip-thin duelist in minimal banded leather, low sprinting
  crouch, one leg forward, torn cloth ribbons tied at wrists and ankles
  trailing backward. Bronze-tan skin, dark leather straps.
- **#13 Grix**: squat box-shaped riveted construct on short stubby legs,
  retractable spike plates along back and shoulders, a large spoked wheel
  visible at its base. Dull iron, exposed rivets and cogwork.
- **#17 Elgorath**: massive hunched humanoid, oversized fists near the
  ground, wide low stance, cracked granite skin with a network of glowing
  orange fracture lines across chest and arms.
- **#20 Vash**: lean sprinter, minimal chest armor, mid-stride running pose
  with arms swept back, spiky hair/mane blown backward, fights bare-handed.
  Sand-tan skin, dark wraps.

### Magic (1, 2, 7, 10, 12, 19)

- **#1 Kethrax**: towering hooded figure holding a tall runic staff, heavy
  robes flaring outward at the base, a fixed ring of glowing glyphs floating
  around its feet. Deep violet robes, silver rune markings.
- **#2 Harmund**: crystalline humanoid, faceted geode-like body, both arms
  fused into broad flat shield-plates held in front of the chest, squat wide
  stance. Pale amethyst, dark violet glow lines.
- **#7 Caldrek**: gaunt hunched spellblade in tattered void-black robes, arms
  outstretched with claw-like fingers, violet glowing sigils across its
  exposed chest and forearms, sunken glowing eyes.
- **#10 Morvex**: hooded torso with no legs; below the waist its form is a
  mass of spectral grasping hands reaching outward in all directions.
  Near-black robes fading to translucent void, silver-white glowing hands.
- **#12 Fiorel**: slender caster standing atop a flat glyph-disc, two glowing
  orbs orbiting at shoulder height, one arm raised, leaning forward. Bright
  white/silver robes, thin build.
- **#19 Brune**: rounded cloaked figure with a cracked opening in its chest
  revealing a glowing core beneath the ribs, arms held slightly out from the
  body. Dark robes, blinding white-gold light from the crack.

### Ranged (4, 5, 6, 14, 15, 18)

- **#4 Tolmar**: broad rooted archer, wide planted stance, a massive bow
  built into its own forearm held fully drawn, taut bowstring. Weathered
  bronze plating, thick woven cable wrapping the arms.
- **#5 Rane**: lean armored duelist in a low coiled ready-stance, one curved
  throwing blade in each hand held close to the body, amber marks tattooed
  along both forearms. Dark leather, silver blades.
- **#6 Sundra**: figure split down the centerline: right side has sharp
  angular blade-plating on arm and shoulder, left side has smooth rounded
  plating with a glowing orb cradled in an open palm. Cool grey right, warm
  gold left.
- **#14 Nyseth**: very tall gaunt hooded figure in a long tattered slate-grey
  cloak draping to the ground, hands hidden in long sleeves, face shadowed
  except for one glowing yellow eye.
- **#15 Pryn**: compact, sharp-featured fighter in a tight low stance, weight
  coiled forward as if about to spring, fists wrapped in dark cloth. Several
  small pale-blue motes hover close around its fists.
- **#18 Onder**: ancient stone guardian seated cross-legged, eyes closed, a
  bow fused directly into its forward arm with the string drawn, dormant
  amber glow lines along its stone surface.

## Open / Not Yet Decided

- **Move/ability flavor naming pass**, deliberately deferred until after
  hands-on testing (see Core Ruleset). Testing stand-ins are in place in the
  Move Glossary so this isn't blocking.
- Reconsider the "Prism Shards" currency name now that types are
  Martial/Magic/Ranged rather than elemental.
- Exact prices for items and ability-change consumables, including the
  significant per-use cost for ability re-capsuling.
