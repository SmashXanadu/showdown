# Custom Pokemon Balance Project, Design Doc

## Core Ruleset

- **Base Stat Total:** fixed at 600 for every mon. No EVs, no IVs. Since every
  mon shares the same power budget, the *distribution shape* of those 600
  points (plus ability and movepool) is the only thing that differentiates
  one mon from another, not raw stat total.
- **Kit:** each mon gets exactly 1 passive ability + 4 moves + 1 held item.
- **Type system:** 3-type rock-paper-scissors wheel, single-type only (no
  dual-typing), for maximum matchup clarity. Standard multipliers apply:
  2x super effective / 1x neutral / 0.5x resisted, with **no immunities**.
  True RPS has no "doesn't affect you" case, so none exists here. Any
  Water-Absorb-style absorb/immunity interaction should be built as a
  specific mon's *signature ability* (a rare, memorable exception), never a
  system-wide type-chart rule.
  - **Final type names: Martial / Magic / Ranged.** Replaces the
    Fire/Water/Grass placeholder used during mechanics design. Wheel:
    **Martial beats Ranged, Ranged beats Magic, Magic beats Martial**, a
    combat-role triangle (melee closes the gap on ranged; ranged snipes the
    caster before the spell resolves; magic's burst/control drops the
    fighter before it closes in), chosen instead of another elemental trio so
    the identity reads as original rather than a Pokemon reskin. Maps
    directly onto the old placeholder: **Fire to Martial, Grass to Ranged,
    Water to Magic** (this mapping matters for reading the rest of this doc
    until the follow-up pass below is done).
  - **Follow-up still needed:** individual move and ability *names* (Cinder
    Burst, Riptide Crash, Verdant Pulse, Tidal Surge, etc.) still carry the
    old Fire/Water/Grass elemental flavor baked in from before the rename.
    The type category each belongs to hasn't changed, but the flavor text
    will read wrong under Martial/Magic/Ranged until they get their own
    naming pass, tracked in Open/Not Yet Decided.
- **Roster size:** 18 mons (see cuts below). Chosen for symmetry (6 mons per
  type, exactly) after starting from a 20-mon draft that split 7/7/6 across
  types and turned out to be one asymmetric type too many. Not fixed in
  stone; mons may still be added or cut later while balancing counters.
- **No em dashes in any project content.** Standing style rule from here on:
  use commas, colons, parentheses, or separate sentences instead.

## 18-Playstyle Roster (draft, pending stat/typing revision from 20 to 18)

Distilled from Smogon's official ADV (Gen 3) OU Threat List
(smogon.com/rs/articles/adv_threatlist), merging pokemon that represent the
same underlying playstyle so the roster has no redundant picks. Baton Pass
support (originally its own slot, inspired by Vaporeon/Umbreon/Jolteon) was
cut entirely per decision, not being represented in this game at all.

Original numbering (1-20) is kept as stable IDs rather than renumbered after
the cut below, so every cross-reference elsewhere in this doc (#5/#7/#10,
etc.) still points at the same mon. **#11 and #16 are cut**: gaps in the
numbering are intentional, not missing rows.

| # | Playstyle | Gen 3 inspiration |
|---|---|---|
| 1 | Weather setter, mixed wallbreaker | Tyranitar |
| 2 | Premier physical wall + hazard/phaze | Skarmory |
| 3 | Premier special wall + cleric | Blissey |
| 4 | Bulky setup wall to sweeper | Suicune |
| 5 | Dedicated counter-attacker (checks #1) | Swampert |
| 6 | Dual-role pivot (support *or* sweeper) | Celebi |
| 7 | Bulky setup sweeper, resists own answers | Salamence / Gyarados |
| 8 | Glass-cannon Choice wallbreaker | Medicham / Heracross / Slaking |
| 9 | Fast special setup sweeper | Raikou / Jirachi |
| 10 | Ability-based trapper | Dugtrio / Magneton |
| ~~11~~ | ~~Prediction/Pursuit trapper~~, **cut** (overlapped with #10's trapper niche) | ~~Houndoom~~ |
| 12 | Offensive pivot spinner (fast, dual-purpose) | Starmie |
| 13 | Defensive hazard setter + spin support (max bulk) | Forretress |
| 14 | Disruption/status ghost | Dusclops / Gengar |
| 15 | Sleep-enable + breaker combo | Breloom |
| ~~16~~ | ~~Adaptive defensive pivot~~, **cut** (overlapped with #1/#7's flexibility) | ~~Porygon2~~ |
| 17 | Slow bulky setup attacker | Snorlax |
| 18 | Stall-loop defensive attacker | Zapdos |
| 19 | Sacrificial nuke | Metagross |
| 20 | Speed-based cleaner | Aerodactyl |

**Note on #5 and #7:** in real Gen 3, Swampert "counters" Tyranitar via a
typing immunity (Ground no-sells Electric) and Salamence/Gyarados "resist
their own answers" via dual-typing quirks. Neither mechanic exists once
typing is reduced to a 3-type, no-immunity, single-type wheel, so those two
slots' hard-counter identity had to come from stats/ability instead of
typing once we assigned types.

## BST Distribution Draft

Every mon sums to exactly 600. **No spread reuses a real Pokemon's exact base
stats**: four slots (1, 6, 7, 19) originally matched Tyranitar, Celebi,
Salamence, and Metagross exactly (each of those four happens to already sit
at 600 BST in the real games with a shape that fit the archetype), so those
four were deliberately perturbed to keep the same functional identity without
duplicating a real stat line. Rows for cut mons (#11, #16) are removed here
since they no longer need stats.

| # | Playstyle | HP | Atk | Def | SpA | SpD | Spe | Notes |
|---|---|--:|--:|--:|--:|--:|--:|---|
| 1 | Weather setter, mixed wallbreaker | 100 | 130 | 114 | 95 | 100 | 61 | |
| 2 | Physical wall + hazard/phaze | 120 | 70 | 170 | 50 | 100 | 90 | highest Def in roster |
| 3 | Special wall + cleric | 190 | 30 | 30 | 130 | 140 | 80 | highest HP and SpD; physically frail on purpose |
| 4 | Bulky setup wall to sweeper | 100 | 60 | 120 | 110 | 120 | 90 | symmetric bulk, dumped Atk |
| 5 | Dedicated counter-attacker | 110 | 130 | 120 | 40 | 110 | 90 | tankier and harder-hitting than #1, no SpA |
| 6 | Dual-role pivot | 105 | 95 | 100 | 105 | 95 | 100 | near-flat generalist |
| 7 | Bulky setup sweeper | 95 | 130 | 80 | 115 | 80 | 100 | |
| 8 | Glass-cannon Choice wallbreaker | 110 | 200 | 60 | 30 | 80 | 120 | highest Atk in roster |
| 9 | Fast special setup sweeper | 100 | 30 | 65 | 175 | 90 | 140 | highest SpA in roster |
| 10 | Ability-based trapper | 120 | 90 | 110 | 50 | 100 | 130 | see balance flag below |
| 12 | Offensive pivot spinner | 75 | 60 | 90 | 130 | 90 | 155 | 2nd-fastest, dual-purpose |
| 13 | Defensive hazard setter + spin | 110 | 110 | 150 | 30 | 100 | 100 | hits harder than #2, slightly less bulky |
| 14 | Disruption/status ghost | 100 | 50 | 100 | 130 | 130 | 90 | bulky special-side disruptor |
| 15 | Sleep-enable + breaker | 90 | 170 | 90 | 30 | 90 | 130 | 2nd-hardest physical hitter |
| 17 | Slow bulky setup attacker | 185 | 130 | 95 | 40 | 120 | 30 | slowest in roster |
| 18 | Stall-loop defensive attacker | 120 | 50 | 100 | 140 | 100 | 90 | 3rd-highest SpA |
| 19 | Sacrificial nuke | 85 | 135 | 125 | 95 | 90 | 70 | |
| 20 | Speed-based cleaner | 85 | 130 | 65 | 45 | 75 | 200 | highest Speed in roster |

**Balance flag for #10 (ability-based trapper):** in real Gen 3,
Dugtrio/Magneton offset a game-warping trapping ability by being deliberately
weak everywhere else (Dugtrio is only 365 BST). That discount isn't
available here since every mon is forced to 600, so #10 got a moderate,
support-shaped spread instead of a specialist one. Its actual balance will
have to come from the ability/movepool design (e.g. limiting what it can do
once it traps something), not from stats. Worth remembering when we design
its kit.

## Type Assignment Draft

Anchored on the #5/#7 counter-logic problem noted above: since #5 is supposed
to hard-counter #1 (the weather setter), #5's type was chosen as whichever
type beats #1's type in the wheel. **#1 = Magic** was picked arbitrarily,
which forces **#5 = Ranged** (Ranged beats Magic 2x and resists Magic's STAB
at 0.5x), a real mechanical hard-counter, no immunity needed. #7's "resists
own answers" identity could *not* be rebuilt via typing (a pure 3-type cycle
gives every type exactly one hard counter, with no dual-type escape hatch
since typing is single-type-only), so that one still has to come from
stats/ability, not typing.

The rest were distributed to keep each type a viable, self-contained team
(a mix of walls/sweepers/utility within every type, not one type being
all-offense). After cutting #11 (Martial) and #16 (Magic), this now lands on
an even 6/6/6 split:

| Type | Mons (#) |
|---|---|
| Magic (6) | 1, 2, 7, 10, 12, 19 |
| Ranged (6) | 4, 5, 6, 14, 15, 18 |
| Martial (6) | 3, 8, 9, 13, 17, 20 |

(Type names finalized as Martial/Magic/Ranged; see Core Ruleset for the
Fire to Martial, Grass to Ranged, Water to Magic mapping from the old
placeholder. What matters mechanically is each mon's *position in the wheel
relative to the others*, especially the #1/#5 relationship above. That
hasn't changed, only the labels have.)

## Signature Abilities & Items

Each mon's default/intended kit. Ability names are original (not reused from
real Pokemon) even where the underlying mechanic echoes a familiar concept;
that's noted inline for our own implementation reference. Items reuse
standard competitive-item mechanics directly (Leftovers, Life Orb, Choice
items, etc.) since those are generic genre vocabulary, not mon-specific
flavor, and Pokemon Showdown already implements them.

| # | Playstyle | Ability (signature) | Item (signature) |
|---|---|---|---|
| 1 | Weather setter, mixed wallbreaker | **Tidal Surge**: summons a 5-turn Rain field on switch-in (Water moves x1.5, Fire moves x0.5, team-wide) | Life Orb |
| 2 | Physical wall + hazard/phaze | **Bulwark**: survives any hit from full HP with 1 HP left (Sturdy-style) | Leftovers |
| 3 | Special wall + cleric | **Purifying Aura**: cures its own status on switch-out (Natural Cure-style) | Leftovers |
| 4 | Bulky setup wall to sweeper | **Steady Growth**: +1 Sp. Atk at the end of each turn on field (max +3) | Leftovers |
| 5 | Dedicated counter-attacker | **Overgrowth Ward**: Attack rises sharply, once, when HP first drops below 1/3 | Rocky Helmet |
| 6 | Dual-role pivot | **Adaptive Instinct**: takes 25% less damage from the first hit after switching in | Sitrus Berry |
| 7 | Bulky setup sweeper | **Momentum**: offensive stat that scored the KO rises 1 stage after any KO (Moxie-style) | Weakness Policy |
| 8 | Glass-cannon Choice wallbreaker | **Overheat Drive**: Attack x1.5 while statused; burn does not reduce its Attack (Guts-style, no downside) | Choice Band |
| 9 | Fast special setup sweeper | **Static Charge**: +1 Speed at the end of each turn on field (Speed Boost-style) | Life Orb |
| 10 | Ability-based trapper | **Undertow**: opposing active mon cannot switch out while this mon is active (Arena Trap-style) | Rocky Helmet |
| 12 | Offensive pivot spinner | **Rapid Current**: its Speed cannot be lowered by opponents' moves/abilities | Heavy-Duty Boots |
| 13 | Defensive hazard setter + spin | **Iron Hide**: takes 20% less damage from contact moves | Leftovers |
| 14 | Disruption/status ghost | **Unnerve Field**: opposing mons cannot consume held Berries while this mon is active (Unnerve-style) | Leftovers |
| 15 | Sleep-enable + breaker | **Focus Drive**: moves with power 60 or less deal 1.5x damage (Technician-style) | Focus Sash |
| 17 | Slow bulky setup attacker | **Juggernaut**: stat boosts from its own moves cannot be lowered by opponents | Leftovers |
| 18 | Stall-loop defensive attacker | **Undying Will**: once per battle, survives a KO hit with 1 HP | Leftovers |
| 19 | Sacrificial nuke | **Detonation Core**: if KO'd by a contact move, deals 25% of the attacker's max HP back (Aftermath-style) | Life Orb |
| 20 | Speed-based cleaner | **Adrenaline Rush**: its Speed cannot be lowered by status or opponents' effects | Focus Sash |

**Balance note on #10's Undertow:** ties directly into the earlier balance
flag on this slot. A guaranteed, unconditional trap is the single most
game-warping mechanic in the whole kit list, doubly so paired with full 600
BST (real Dugtrio/Magneton only got away with it by being weak everywhere
else). If early playtesting shows it's oppressive, first lever to pull is
conditioning the trap (e.g. only traps mons below a HP threshold, or only
lasts N turns) rather than removing it outright.

## Shared Ability Pool (swappable, not tied to one mon)

| Ability | Effect |
|---|---|
| Featherweight | Takes no recoil damage from its own moves |
| Iron Will | Cannot be made to flinch |
| Steel Nerve | Immune to confusion, infatuation, and flinching |
| Thick Hide | Takes 25% less damage from super-effective hits |
| Cleanse Step | Removes all hazards from its own side on switch-in |
| Grit | Attack and Sp. Atk cannot be lowered by opponents |
| Steadfast Guard | Defense and Sp. Def cannot be lowered by opponents |
| Quickstep | Moves first in its priority bracket while at full HP |
| Renewal | Restores 33% max HP when switching out |
| Toughen Up | Def and Sp. Def each rise 1 stage the first time it takes damage in a battle |
| Wounded Fury | Attack rises 1 stage whenever it drops below 50% HP (repeatable) |

## Shared Item Pool (standard-style held items)

| Item | Effect |
|---|---|
| Leftovers | Restore 1/16 max HP each turn |
| Life Orb | +30% move power; 10% recoil per hit |
| Choice Band | +50% Attack; locked into first move used |
| Choice Specs | +50% Sp. Atk; locked into first move used |
| Choice Scarf | +50% Speed; locked into first move used |
| Assault Vest | +50% Sp. Def; cannot use status moves |
| Rocky Helmet | Contact attackers take 1/6 max HP damage |
| Focus Sash | Survives a hit that would KO it from full HP, left at 1 HP |
| Heavy-Duty Boots | Immune to all entry-hazard effects on switch-in |
| Sitrus Berry | Restores 25% max HP once, when HP drops below half |
| Weakness Policy | +2 Atk and +2 Sp. Atk once, when hit by a super-effective move |
| Expert Belt | +20% power when the move isn't resisted by the target |
| Shell Bell | Restores 12.5% of damage dealt as HP each hit |
| Toxic Orb | Badly poisons the holder after 1 turn (synergy with #8's Overheat Drive) |

## Movesets (fixed, not player-chosen)

**Decision:** moves are permanently locked per mon. The player never picks
or swaps a mon's moves. This is different from abilities/items, which do
still use the swappable shared-pool model from the previous section; the
move library below was only ever a design tool for authoring each mon's
fixed 4, not a player-facing pool.

**Coverage rule (derived, keep for all future move design):** in the
Martial to Ranged to Magic to Martial cycle, an attacker's own STAB is always
resisted by the type that beats it, and that resister is in turn beaten by
the attacker's own type's prey. Concretely: **Martial attackers want Ranged
coverage, Ranged attackers want Magic coverage, Magic attackers want Martial
coverage.** This is also why #1 is legitimately "mixed" rather than just
flavor-mixed: Magic STAB + Martial coverage is the mechanically correct
pairing for a Magic-type that wants to punch through Ranged walls.

*(The move names in the tables below, like Riptide, Cinder, Verdant, Tidal,
etc., still use the old Fire/Water/Grass flavor and haven't been renamed to
match Martial/Magic/Ranged yet; see Open/Not Yet Decided. Their type category
is unaffected: read Water-flavored moves as Magic-type, Grass-flavored as
Ranged-type, Fire-flavored as Martial-type.)*

### Move Library (design reference, not player-facing)

| Move | Effect |
|---|---|
| Recover | Heal self 50% max HP |
| Toxic Bloom | Badly poisons the target |
| Scorch | Burns the target |
| Barrier Wall | +1 Def, +1 SpD (self) |
| War Cry | +1 Atk, +1 Spe (self) |
| Focus Mind | +1 SpA, +1 SpD (self) |
| Sharpen Claws | +2 Atk (self) |
| Retreat Call | Forces the target to switch out |
| Guard Break | -1 Def, -1 SpD (target) |
| Barricade Spikes | Stacking hazard, damages opposing switch-ins |
| Shield Up | Blocks all damage/effects this turn |
| Mirror Image | Creates a decoy (Substitute-style) |
| Cleansing Wave | Cures the user's own status |
| Last Resort Blast | Self-KO, heavy damage to target |
| Restful Slumber | User sleeps, but fully heals HP and status |
| Clear Tide | Removes all hazards from the user's side |
| Grim Resolve | Spe -1, Atk +2, Def +2 (self) |
| Dream Action | While asleep, automatically executes a random other move in the set |

### Fixed Movesets (final, locked, not player-adjustable)

Each mon's exact 4 moves, chosen from its signature attacks plus whichever
library moves the archetype actually needs to function (e.g. #18 needs
Restful Slumber + Dream Action together as one unit, that's the RestTalk
loop; #2 needs its hazard + phaze + recovery all at once per its archetype
definition).

| # | Playstyle | Fixed moveset (4) |
|---|---|---|
| 1 | Weather setter, mixed wallbreaker | Riptide Crash (Water/Phys/110), Cinder Burst (Fire/Spec/90, coverage), War Cry, Recover |
| 2 | Physical wall + hazard/phaze | Riptide Slam (Water/Phys/65), Barricade Spikes, Retreat Call, Recover |
| 3 | Special wall + cleric | Scorch Wave (Fire/Spec/85, may burn), Recover, Cleansing Wave, Toxic Bloom |
| 4 | Bulky setup wall to sweeper | Verdant Pulse (Grass/Spec/90), Tidewave (Water/Spec/85, coverage), Focus Mind, Recover |
| 5 | Dedicated counter-attacker | Bramble Slam (Grass/Phys/95), Torrent Fang (Water/Phys/85, coverage), War Cry, Recover |
| 6 | Dual-role pivot | Bloom Beam (Grass/Spec/80), Tidal Pulse (Water/Spec/80, coverage), Focus Mind, Recover |
| 7 | Bulky setup sweeper | Torrent Crush (Water/Phys/100), Sharpen Claws, Cinder Fang (Fire/Phys/90, coverage), Recover |
| 8 | Glass-cannon Choice wallbreaker | Inferno Slam (Fire/Phys/120), Ashen Fang (Fire/Phys/95, flinch chance), Bramble Fist (Grass/Phys/100, coverage), Sharpen Claws |
| 9 | Fast special setup sweeper | Blaze Beam (Fire/Spec/95), Thorn Burst (Grass/Spec/90, coverage), Focus Mind, Recover |
| 10 | Ability-based trapper | Riptide Fang (Water/Phys/85), Cinder Snap (Fire/Phys/85, coverage), Toxic Bloom, Recover |
| 12 | Offensive pivot spinner | Tidal Beam (Water/Spec/90), Cinder Spark (Fire/Spec/85, coverage), Clear Tide, Recover |
| 13 | Defensive hazard setter + spin | Ember Crush (Fire/Phys/85), Barricade Spikes, Clear Tide, Recover |
| 14 | Disruption/status ghost | Bloom Shade (Grass/Spec/85, debuff chance), Tide Veil (Water/Spec/80, coverage), Retreat Call, Toxic Bloom |
| 15 | Sleep-enable + breaker | Slumber Spores (Grass/Status, exclusive sleep move), Thorn Jab (Grass/Phys/60, priority), Thorn Focus (Grass/Phys/130), Tide Fist (Water/Phys/90, coverage) |
| 17 | Slow bulky setup attacker | Magma Slam (Fire/Phys/90), Grim Resolve, Thorn Crush (Grass/Phys/85, coverage), Recover |
| 18 | Stall-loop defensive attacker | Thorn Pulse (Grass/Spec/85), Mire Bolt (Water/Spec/90, coverage), Restful Slumber, Dream Action |
| 19 | Sacrificial nuke | Torrent Slam (Water/Phys/90), Cinder Crush (Fire/Phys/85, coverage), Last Resort Blast, Recover |
| 20 | Speed-based cleaner | Tidal Fang (Water/Phys/90, flinch chance), Cinder Slash (Fire/Phys/85, coverage), Sharpen Claws, Shield Up |

**Note on #8:** Sharpen Claws is a slightly awkward fit alongside Choice Band
(setup and move-lock don't really synergize), kept deliberately anyway so the
mon isn't dead weight if it's ever given a different item via the swappable
item pool.

**Movepool review (2026-09-22):** checked all 18 fixed movesets for coverage
gaps. #2, #3, and #13 have no coverage move and are hard-walled by their
counter type, intentional, since they're wall/support archetypes and this is
the RPS system working as designed (the same mechanism that makes #5 counter
#1). #6 had the same gap but its archetype ("dual-role pivot," meant to have
no glaring weakness) made it a real problem, so it was fixed: `Verdant Slash`
was swapped for `Tidal Pulse` (Water/Spec coverage). #18 was also found to be
mistyped during the type/moveset cross-check: it's assigned Ranged-type
(originally Grass) but had a Martial-flavored (Fire) STAB move; fixed by
making `Thorn Pulse` (Ranged) its STAB and adding a new Magic-type coverage
move, `Mire Bolt`, in place of the old Fire move. See the moveset table above
for both corrected lines.

## Meta-Economy: Currency, Items & Ability Changes

**Decision:** items and ability changes are earned/purchased with a meta
currency, but behave differently once acquired:

- **Held items** are bought once, then owned permanently and can be freely
  equipped to/removed from any mon at no further cost, standard "Bag item"
  behavior, drawn from the shared item pool.
- **Ability changes** are a consumable (real-Pokemon equivalent: Ability
  Capsule). Using one permanently overwrites a mon's current ability with a
  different one. **Decision:** a mon can be re-capsuled as many times as the
  player wants, there is no hard cap, but each use carries a significant
  currency cost. The cost is the balance lever, not a usage limit.

**Decision: how currency is earned.** Battle wins. Win streaks grant a bonus
that increases the longer the streak runs, rewarding sustained play over
one-off wins.

**Balance guardrail (important):** ability-change consumables may only
assign an ability from the **shared ability pool**, never another mon's
*signature* ability. This exists specifically because of the balance flag
already on #10: Undertow (unconditional, no-escape trapping) is only
tolerable stapled to a mon with mediocre offense. If it could be transplanted
via consumable onto a high-Attack mon (e.g. #8, 200 Atk), that combination
would likely be uncounterable. Signature abilities stay locked to their
original mon; only shared-pool abilities are swap targets.

Currency name suggestion: **Prism Shards**, picked when types were still an
elemental placeholder. "Prism" nods at light splitting into colors, which
doesn't connect as cleanly to a Martial/Magic/Ranged combat triangle. Worth
reconsidering during the naming pass below rather than treated as locked.

## Visual Concepts

Direction: MOBA-style hero design rather than cute-creature Pokemon
aesthetics. Each mon should read from silhouette alone, and each of the
three types has its own non-elemental visual language (this replaced an
earlier elemental-flavored draft entirely, per decision). Descriptions below
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

- **#3 Special wall + cleric**: hooded ascetic in bandage-wrapped robes,
  standing with palms open at chest height, a soft warm glow between the
  palms. No weapon, no armor. Bone-white wrappings, dull gold trim.
- **#8 Glass-cannon Choice wallbreaker**: hulking armored brute, one massive
  cleaver fused to its right arm, weapon dragging low, broad low stance.
  Dark iron plating over corded muscle, one glowing orange seam down the
  blade.
- **#9 Fast special sweeper**: whip-thin duelist in minimal banded leather,
  low sprinting crouch, one leg forward, torn cloth ribbons tied at wrists
  and ankles trailing backward. Bronze-tan skin, dark leather straps.
- **#13 Defensive hazard + spin**: squat box-shaped riveted construct on
  short stubby legs, retractable spike plates along back and shoulders, a
  large spoked wheel visible at its base. Dull iron, exposed rivets and
  cogwork.
- **#17 Slow bulky setup attacker**: massive hunched humanoid, oversized
  fists near the ground, wide low stance, cracked granite skin with a
  network of glowing orange fracture lines across chest and arms.
- **#20 Speed-based cleaner**: lean sprinter, minimal chest armor, mid-stride
  running pose with arms swept back, spiky hair/mane blown backward, fights
  bare-handed. Sand-tan skin, dark wraps.

### Magic (1, 2, 7, 10, 12, 19)

- **#1 Weather setter, mixed wallbreaker**: towering hooded figure holding a
  tall runic staff, heavy robes flaring outward at the base, a fixed ring of
  glowing glyphs floating around its feet. Deep violet robes, silver rune
  markings.
- **#2 Physical wall + hazard/phaze**: crystalline humanoid, faceted
  geode-like body, both arms fused into broad flat shield-plates held in
  front of the chest, squat wide stance. Pale amethyst, dark violet glow
  lines.
- **#7 Bulky setup sweeper**: gaunt hunched spellblade in tattered
  void-black robes, arms outstretched with claw-like fingers, violet
  glowing sigils across its exposed chest and forearms, sunken glowing
  eyes.
- **#10 Ability-based trapper**: hooded torso with no legs; below the waist
  its form is a mass of spectral grasping hands reaching outward in all
  directions. Near-black robes fading to translucent void, silver-white
  glowing hands.
- **#12 Offensive pivot spinner**: slender caster standing atop a flat
  glyph-disc, two glowing orbs orbiting at shoulder height, one arm raised,
  leaning forward. Bright white/silver robes, thin build.
- **#19 Sacrificial nuke**: rounded cloaked figure with a cracked opening in
  its chest revealing a glowing core beneath the ribs, arms held slightly
  out from the body. Dark robes, blinding white-gold light from the crack.

### Ranged (4, 5, 6, 14, 15, 18)

- **#4 Bulky setup wall to sweeper**: broad rooted archer, wide planted
  stance, a massive bow built into its own forearm held fully drawn, taut
  bowstring. Weathered bronze plating, thick woven cable wrapping the arms.
- **#5 Dedicated counter-attacker**: lean armored duelist in a low coiled
  ready-stance, one curved throwing blade in each hand held close to the
  body, amber marks tattooed along both forearms. Dark leather, silver
  blades.
- **#6 Dual-role pivot**: figure split down the centerline: right side has
  sharp angular blade-plating on arm and shoulder, left side has smooth
  rounded plating with a glowing orb cradled in an open palm. Cool grey
  right, warm gold left.
- **#14 Disruption/status ghost**: very tall gaunt hooded figure in a long
  tattered slate-grey cloak draping to the ground, hands hidden in long
  sleeves, face shadowed except for one glowing yellow eye.
- **#15 Sleep-enable + breaker (Pryn)**: compact, sharp-featured fighter in a
  tight low stance, weight coiled forward as if about to spring, fists
  wrapped in dark cloth. Several small pale-blue motes hover close around
  its fists.
- **#18 Stall-loop defensive attacker**: ancient stone guardian seated
  cross-legged, eyes closed, a bow fused directly into its forward arm with
  the string drawn, dormant amber glow lines along its stone surface.

## Names

Every mon now has a name, chosen with two deliberate constraints: all 18
first letters are unique (no two mons can be confused by name alone), and
after an initial pass that accidentally produced several close-sounding
pairs (e.g. Torvin/Corvane, Ravik/Pravos, Hesk/Bosk), names were reviewed
against each other for sound-alike collisions and reworked. The set also
deliberately mixes single-syllable names (blunt, punchy, fits
brute/bunker/bomber/sprinter/duelist kits) with two- and three-syllable names
rather than being uniform. The # column stays the stable ID used everywhere
else in this doc; name is an added attribute, not a replacement for it.

| # | Playstyle | Name |
|---|---|---|
| 1 | Weather setter, mixed wallbreaker | Kethrax |
| 2 | Physical wall + hazard/phaze | Harmund |
| 3 | Special wall + cleric | Aswin |
| 4 | Bulky setup wall to sweeper | Tolmar |
| 5 | Dedicated counter-attacker | Rane |
| 6 | Dual-role pivot | Sundra |
| 7 | Bulky setup sweeper | Caldrek |
| 8 | Glass-cannon Choice wallbreaker | Dresh |
| 9 | Fast special setup sweeper | Ixara |
| 10 | Ability-based trapper | Morvex |
| 12 | Offensive pivot spinner | Fiorel |
| 13 | Defensive hazard setter + spin | Grix |
| 14 | Disruption/status ghost | Nyseth |
| 15 | Sleep-enable + breaker | Pryn |
| 17 | Slow bulky setup attacker | Elgorath |
| 18 | Stall-loop defensive attacker | Onder |
| 19 | Sacrificial nuke | Brune |
| 20 | Speed-based cleaner | Vash |

**Roster status:** confirmed good as-is for now. No further adds/cuts planned
until hands-on testing surfaces a reason to revisit.

## Open / Not Yet Decided

- **Move/ability flavor naming pass**: rename move and ability names (Cinder
  Burst, Riptide Crash, Tidal Surge, Verdant Pulse, etc.) to match the
  finalized Martial/Magic/Ranged identity instead of the old Fire/Water/Grass
  placeholder flavor. Their type category assignments don't change, only the
  names/flavor text. **Deliberately deferred**: to be done as a later pass
  once hands-on testing has happened, not before.
- Reconsider the "Prism Shards" currency name now that types are
  Martial/Magic/Ranged rather than elemental
- Exact prices for items and ability-change consumables, including the
  significant per-use cost for ability re-capsuling
