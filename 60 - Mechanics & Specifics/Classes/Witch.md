# The Witch

### Base Class — Game Design Document

_Draft 2 | Base class only | No subclasses_

---

## Design Philosophy

The Witch is not defined by their hat, their robes, or their aesthetic. They are defined by one thing: the bond between a sundered mortal soul and the dark soul — the Stygian — that was once part of them.

Witches are the result of Hags being separated by the House of Empty during the Age of Redemption. A Hag — a fusion of mortal and beast soul created to gather tribute — was split into two: the mortal (the Witch) and the dark soul (the Stygian). They are not master and familiar. They are not mage and pet. They are one thing learning to function as two.

Every mechanical feature of the Witch class exists to express this relationship. The player is always playing both bodies simultaneously — not a caster with a companion, but a sundered being trying to coordinate its two halves.

> **The Aesthetic Is Yours** A plague doctor with an axe and a crow Stygian is the same class as a barefoot herbalist with a staff and a toad Stygian. A noble fencer with a rapier and a raven is the same class as a swamp witch with a scythe and a black cat. The bond is the class. The look is the player's.

---

## Class Identity

### Primary Fantasy

Investigator and utility specialist first. Combat is the crescendo, not the whole meal. The Witch excels at reading situations, gathering information, navigating obstacles — because they have two sets of senses, two bodies, and one shared mind. In combat, they are a dual threat: a weapon and a magical second body that the enemy cannot ignore.

### The Three Pillars

|Pillar|Expression|
|---|---|
|Protection|Two bodies create natural pressure. The Stygian disrupts attackers. The bond enables escape.|
|Offensive|The Witch strikes with a weapon. The Stygian follows with magic. One resource escalates both.|
|Identity|Bond Movement — the ability to pull, snap, or swap positions freely, once per turn.|

### Role in the Party

- Primary investigator — dual senses, ritual magic, Stygian as undetected scout
- Secondary martial — reliable weapon attacks with magical rider damage
- Utility caster — half-caster spell list focused on information, control, and disruption
- Not a healer, not a tank — a threat multiplier that is hard to pin down

---

## Core Statistics

|||
|---|---|
|Hit Dice|1d10 per Witch level|
|HP at 1st Level|10 + Constitution modifier|
|HP at Higher Levels|1d10 (or 6) + Constitution modifier per level|
|Armor Proficiency|Light armor, medium armor|
|Weapon Proficiency|All simple and martial weapons|
|Saving Throws|Constitution, Intelligence|
|Skills|Choose two: Arcana, Deception, Investigation, Insight, Nature, Perception, Persuasion, or Religion|
|Spellcasting|Half-caster (Intelligence)|
|Spell Save DC|8 + proficiency bonus + Intelligence modifier|
|Spell Attack Modifier|Proficiency bonus + Intelligence modifier|

> _Note on d10 HP: The Witch is physically durable because neither body can truly die while the other lives. The shared HP pool means the player is never managing two HP bars — there is one pool, one threshold, one death. The d10 reflects the toughness of a sundered being that refuses to fall._

---

## The Stygian

The Stygian is not a familiar. It is not a pet or a summoned creature. It is the other half of the Witch — a dark soul wearing the shape of a small animal, returned to the world alongside its mortal counterpart.

Stygians take the form of classic omen animals: black cats, ravens, toads, hares, owls, spiders, crows. The specific form is the player's choice and carries no mechanical difference at base — the Stygian's form is flavor that the player builds into through Stygian Evolution choices at later levels.

### Stygian Base Statistics

|||
|---|---|
|Size|Tiny or Small (player's choice at character creation)|
|Speed|30 ft. (modified by Evolution choices)|
|Armor Class|Equal to the Witch's spell save DC|
|Hit Points|Shared pool with the Witch|
|Saving Throws|Uses the Witch's saving throw values|
|Condition Immunities|Frightened, Charmed|
|Languages|Understands all languages the Witch knows|
|Initiative|Rolls its own initiative, acts on its own turn|

### Shared HP Pool

The Witch and Stygian share a single hit point pool. Damage dealt to either body comes from the same pool. If the pool reaches 0, the Stygian's physical form dissipates — it does not die, it dissolves back into the bond. The Stygian reforms when the Witch returns to at least 1 hit point.

If both bodies are caught in the same area of effect, each rolls their own saving throw and each instance of damage is applied to the shared pool separately. Being in the same space is a meaningful risk — it is the tax on certain uses of Bond Movement.

### The Bond

- The Witch and Stygian share an unbreakable telepathic bond across any distance.
- Both can perceive through each other's senses simultaneously, unless one side wills otherwise.
- The Stygian cannot travel further than 60 feet from the Witch without being pulled back.
- If either is transported to another plane, the other is instantly transported alongside them, appearing within 5 feet.
- Conditions are applied to each body independently. A charmed Stygian does not charm the Witch.

### Appearing Mundane

The Stygian, when not actively using magic, appears to be a perfectly ordinary animal. Without magical detection or direct knowledge of Witches, there is no way to distinguish it from a mundane creature. This is not an ability — it is simply what Stygians are.

_A black cat sits on a windowsill. A raven watches from the rafters. You cannot prove it is anything more than that. That is the point._

This creates a natural investigative advantage: the Stygian can be present in spaces where a magical companion would be confiscated, questioned, or noticed. It provides a second set of senses in rooms the Witch cannot enter.

---

## The Three Pillars — Detailed Design

### Pillar 1 — Identity: Bond Movement

_Class Feature, 1st level_

Once per turn, as part of your movement, choose one of the following:

**Pull** — You drag the Stygian to an unoccupied space within 5 feet of you. This does not cost the Stygian any of its movement.

**Snap** — You move to an unoccupied space within 5 feet of the Stygian. This movement does not provoke opportunity attacks.

**Swap** — You and the Stygian exchange positions simultaneously. Neither of you provokes opportunity attacks from this movement.

The Stygian's AC is its own and is not shared. Bond Movement costs no action, no bonus action, and no resource — it is simply part of how the Witch moves.

#### Design Notes

- Movement is mundane — both bodies can move independently every turn at no cost. Bond Movement is the one special thing that happens once per turn on top of normal movement.
- Snap is the escape tool. Engage, attack, snap back behind the Stygian. No opportunity attack taken.
- Pull is the rescue tool. Stygian is surrounded, Witch pulls it to safety. No action spent.
- Swap is the repositioning tool. Enemy thinks they have cornered one body. Suddenly they haven't. Creates the most tactical depth — the Witch ends up where the Stygian was, which may be exposed.
- The AoE vulnerability when using Swap (both bodies briefly adjacent) is the intentional tax. Smart enemies who learn the Witch's pattern can bait the swap and drop an AoE on the landing point.
- A player new to the class just uses Snap to escape. An experienced player uses Swap to bait, manipulate, and outmaneuver. High ceiling, low floor.

---

### Pillar 2 — Protection: Sympathetic Interference

_Class Feature, 1st level_

When a creature that you can see hits you with an attack, you can use your Stygian's reaction to impose disadvantage on that attack roll, potentially causing it to miss.

The Stygian does not need to be adjacent to you or the attacker. The interference is a function of the bond — the Stygian disrupts the attacker's focus through presence, noise, movement, or sheer wrongness.

Using this feature costs the Stygian its reaction for the round.

#### Design Notes

- This is the Witch's Uncanny Dodge equivalent — reliable mitigation that costs a reaction, not a resource.
- The cost is the Stygian's reaction, which competes with the offensive use of the Stygian's reaction (see Pillar 3). This creates a real decision each round: protect or attack.
- Narratively: the crow screeches. The cat launches itself at the attacker's face. The toad lands on their weapon hand. The attack goes wide.
- The passive protection layer is simply geometry: two bodies means the enemy is always adjacent to at least one of you, always threatened, always splitting their attention.

---

### Pillar 3 — Offensive: Stygian Strike

_Class Feature, 1st level_

When you make a weapon attack, your Stygian can use its bonus action or its reaction to make a magical attack against the same target or a different target within 30 feet of the Stygian.

Stygian Strike is a ranged spell attack using your Intelligence modifier. On a hit, it deals force damage (see scaling below). The damage type can be changed through Stygian Evolution.

The Stygian does not need to be adjacent to the target. Range is the only limit.

**Bonus action** — costs the Stygian's bonus action on its own turn, used on the Witch's turn. **Reaction** — costs the Stygian's reaction, competing with Sympathetic Interference.

The player chooses which option fits the situation.

#### Stygian Strike Damage Scaling

|Level|Damage|
|---|---|
|1st — 4th|1d6|
|5th — 10th|2d6|
|11th — 16th|3d6|
|17th — 20th|4d6|

#### Design Notes

- The base attack is always free — no resource cost, just an action economy cost (bonus action or reaction).
- The bonus action option enables dual wielding: Witch dual wields (bonus action weapon attack), Stygian still has its reaction for either the magical attack or Sympathetic Interference. Nothing conflicts.
- The reaction option creates the core tension: every round the Stygian has one reaction and two things that want it — Sympathetic Interference (protection) or Stygian Strike (offense). This is the primary decision point of the class.
- The Stygian's own turn enables independent action: on the Stygian's turn, it can move and attack freely without competing with the Witch's economy.
- Damage type, rider effects, and additional properties are added through Stygian Evolution — the base chassis is deliberately simple.

---

## The Resource — Resonance

_Class Feature, 2nd level_

Resonance represents the depth of synchrony between the Witch and Stygian in a given moment — the degree to which the two halves of a sundered being are acting as one. It is not mana. It is not willpower. It is the pulse of the bond under pressure.

You have a number of Resonance points equal to your proficiency bonus. You regain all expended Resonance points on a short or long rest.

Resonance can be spent in three ways:

**Protection** — When you use Sympathetic Interference, you may spend 1 Resonance to also reduce the damage of the triggering attack by 1d10 + your Intelligence modifier, even if the attack still hits.

**Stygian Escalation** — When your Stygian makes a Stygian Strike, you may spend 1 Resonance to activate one Stygian Evolution effect on that attack.

**Witch's Edge** — When you make a weapon attack, you may spend 1 Resonance to add your Intelligence modifier as bonus necrotic damage on a hit. The bond bleeds into the strike.

### Design Notes

- Short rest recovery makes Resonance feel reliable across an adventuring day, not precious. It's a tool, not a rationed treasure.
- Three competing uses with proficiency bonus points (2–6 across levels) means the player always has choices but never feels overwhelmed.
- Witch's Edge is important because it keeps the Witch herself from feeling like just a delivery system for the Stygian. She has her own ceiling too.
- The damage reduction on Protection spend is meaningful at all levels because it scales with Intelligence modifier.
- Stygian Escalation is the evolution system's gateway — it gives Evolutions a resource cost so powerful rider effects aren't free every attack.

---

## Level Progression — Base Features

|Level|Feature|
|---|---|
|1|Stygian, Bond Movement, Sympathetic Interference, Stygian Strike, Spellcasting|
|2|Resonance, Ritualist|
|3|Stygian Evolution (1st choice), Witch Coven|
|4|Ability Score Improvement|
|5|Stygian Strike 2d6, Extra Attack|
|6|Witch Coven Feature|
|7|Stygian Evolution (2nd choice)|
|8|Ability Score Improvement|
|9|—|
|10|Stygian Evolution (3rd choice)|
|11|Untangled Thoughts (separate bonus actions), Stygian Strike 3d6|
|12|Ability Score Improvement|
|13|—|
|14|Witch Coven Feature|
|15|Stygian Evolution (4th choice)|
|16|Ability Score Improvement|
|17|Stygian Strike 4d6|
|18|Stygian Evolution Capstone|
|19|Ability Score Improvement|
|20|Archstygian (separate actions) + Hag Capstone|

### Action Economy Progression

The Witch's defining progression is the gradual separation of action economy between the two bodies — representing the two halves becoming more coordinated, not less separate.

|Level|State|
|---|---|
|1–10|Shared economy — one action, one bonus action, one reaction, one concentration. Split between turns.|
|11|Untangled Thoughts — each body gains its own bonus action. Must be used on that body's turn.|
|20|Archstygian — each body gains its own action. Must be used on that body's turn.|

_The progression is not "gaining power over a familiar." It is remembering what it felt like to be one thing — without crossing the line into becoming a Hag._

---

## Level 20 Capstone — The Hag

At 20th level the Witch has achieved something no other class achieves: a capstone that is genuinely dangerous to use. The Hag form is powerful, horrifying, and potentially fatal — not to enemies, but to the Witch themselves.

### Become the Hag

_Capstone Feature, 20th level_

As an action, you open your mouth. Your Stygian opens its mouth. The bond collapses inward.

You merge into a Hag. Your Stygian's body ceases to exist as a separate entity — it is back where it belongs.

**In Hag form you gain:**

- Your hit point maximum doubles for the duration.
- You gain a +4 bonus to Strength, Constitution, and Intelligence.
- You gain a 30-foot fear aura (Wisdom save DC equals your spell save DC or become frightened for 1 minute).
- You can cast any spell you know without expending a spell slot.
- Your weapon attacks deal an additional 3d8 necrotic damage.

**The Hunger:** At the end of each of your turns in Hag form, make a Wisdom saving throw (DC 15 + number of turns spent in Hag form). On a failed save, the Hag's hunger asserts itself — you must use your action to attack the nearest creature. You may attempt the save again at the end of that turn.

If you kill a creature while in Hag form, the DC of the Wisdom save immediately increases by 5.

**Reverting:** You may revert to Witch form as a bonus action on your turn, provided you have not failed a Wisdom save this turn. When you revert, your hit points are reduced by the amount your hit point maximum was increased (minimum 1 hp).

**Lost:** If you fail three cumulative Wisdom saves while in Hag form, the Hag is complete. You are gone. The DM takes control of the Hag. It is no longer your character.

---

### The Homunculus

_Capstone Consequence_

A Hag that gorges — killing and consuming enough flesh and souls — eventually returns to the House of Empty. The flesh it consumed is left behind.

If the Hag (former Witch) kills 5 or more creatures while in Hag form before being stopped or reverting, it produces a Homunculus when it finally dies or departs.

The Homunculus is a DM-controlled creature. It is humanoid in shape, physically overwhelming (all ability scores 20, cap 26), and mentally infantile. It copies the behavior of the first creature it observes after emergence.

The Homunculus is not evil. It does not understand what it is. It is a tragedy — born from hunger and death, incapable of understanding either.

Homunculi are the reason Hags are hunted the moment one appears. They are the reason Witches do not become Hags. They are the reason the class has a capstone with a cost.

### Design Intent

- Every other class capstone is unambiguously good. This one is not. That is intentional.
- The Hag form is a desperation button — something you reach for when the fight is lost and something terrible needs to happen. The power is real. The cost is real.
- The Hunger mechanic ties the save DC to kills, not time. A clever player can stay in Hag form longer by not killing — using the fear aura, using spells, intimidating. But in a desperate fight where things are dying, the saves come fast and hard exactly when the power is most needed.
- Three failed saves is forgiving enough that a lucky player might never lose control. It is ruthless enough that an unlucky player in a bloody fight might lose their character in three rounds.
- The Homunculus is a campaign event, not just a consequence. The party has to decide what to do with a creature that did not ask to exist, that is stronger than them, that might follow them home.

---

## Spellcasting

The Witch is a half-caster. Magic comes from the Stygian — from the dark soul's ancient memory of what Hags knew and what the House of Empty taught them. The Witch deciphers those whispers and gives them form.

|||
|---|---|
|Spellcasting Ability|Intelligence|
|Spell Slots|Half-caster progression (as Paladin / Ranger)|
|Cantrips Known|2 at 1st, +1 at 4th, +1 at 10th (4 total)|
|Spells Known|Scale with level per spell table|
|Spellcasting Focus|Cannot use a standard arcane focus — spells require material components or a component pouch, since the magic source is unknown and irregular|
|Ritual Casting|Available via Ritualist feature at 2nd level|

### Ritualist — 2nd Level

Your Stygian begins to recall rites it knew in life. You gain access to the Occult Rite list and may cast any spell from it as a ritual, without knowing the spell and without expending a spell slot, as long as the spell level does not exceed your highest available spell slot level. Your Stygian must be within 5 feet of you for the entire casting duration.

---

## Open Questions — For Next Session

- **Stygian Evolution** — how many choices, at what levels, and how do evolutions interact with Resonance spending?
- **Spell list** — utility and investigation heavy, control over damage. What makes the Witch list distinct from Wizard or Ranger?
- **Extra Attack** — does the Witch get it at level 5 like other half-martials, or does the dual-body economy replace the need for it?
- **Subclasses** — Coven of Twin Moon, Coven of Poison Phoenix, Coven of Wild Hunt confirmed. What does the two-spellcasters Coven look like mechanically?
- **Occult Spells** — the reaction-based and positioning-based custom spells from the original draft. Which survive into this version?
- **The resource name** — Resonance is a working title. Does it fit the tone of the setting?

---

_The Witch — Base Class GDD | Draft 2_