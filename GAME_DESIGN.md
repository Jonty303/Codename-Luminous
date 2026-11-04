# Codename-Luminous — Game Design Document

**Version:** 0.1 (initial conversation synthesis)  
**Date:** 4 November 2026  
**Status:** Living design document / pre-production  
**Repository:** Jonty303/Codename-Luminous  
**Design intent:** Capture the vision discussed so far without mistaking exploratory ideas for final commitments.

> **Elevator pitch:** A persistent, small-unit mech real-time tactics game. Command a company of named pilots in modular war machines through an evolving planetary conflict. Orders are immediate and familiar to RTS players, but pilots interpret them according to doctrine, skill, discipline, stress, and circumstance. Battles change the war; the war changes future battles; every pilot and machine builds a service history.

## 1. Design principles

1. **Traditional RTS controls, human execution.** Select individual mechs or squads and give move, attack, defend, patrol, and withdrawal commands directly. Squad leaders relay orders and pilots generally comply, but their actions are not robotic.
2. **Few units, high value.** Mechs, pilots, equipment, injuries, and salvage matter. A retreat, disabled machine, or rescued comrade is as consequential as an enemy kill.
3. **Emergent but understandable behaviour.** Autonomy should generate believable stories, not punish the player through arbitrary random disobedience. Give warnings, acknowledgements, and explanations.
4. **Machines are modular systems.** Chassis, body parts, armour, equipment slots, power, cooling, ammunition, and weapons create trade-offs. Component damage changes tactical capability.
5. **A living battlefield.** Cover, elevation, water, smoke, fire, destruction, and civilian presence affect tactics. Visual spectacle should reflect meaningful gameplay consequences.
6. **A living war.** One planet, two initial sides, established geography, regional objectives, and off-screen operations. Player-chosen missions alter the larger conflict.
7. **Recorded consequences.** Pilot service histories, mech histories, mission reports, and a war chronicle derive from a shared record of actual events.
8. **Authored and procedural content coexist.** A scripted mission can be affected by the current war state, and its result must feed back into that state.
9. **Build a playable vertical slice first.** The initial prototype tests the distinctive systems; it does not need a whole planetary war or photorealistic destruction.

### Influence and originality

Key **gameplay** reference points are the original MechCommander (1998), Dark Reign's configurable unit autonomy, and persistent-personnel campaign games. **Visual** reference points include FASA/BattleTech's industrial, silhouette-driven mechs and the mass/proportions of T'au battlesuits (Broadside, Riptide, Crisis, and an armed Stormsurge conversion). These are inspiration, **not assets or designs to copy**. Codename-Luminous needs original chassis silhouettes, terminology, factions, art, and setting.

Third-party game code and assets should not be presumed public domain merely because they are downloadable. Any imported materials require a source-and-licence audit; keep experimental third-party assets isolated from the public repository until rights and redistribution terms are confirmed. An eventual commercial path should not depend on restricted content.

## 2. Player role and core loops

The player commands a **mechanised company**, not necessarily the entire planetary military. Higher command, allied commanders, and an opposing military operate independently. The player chooses many operations, receives occasional directives, and decides how to execute them.

**Tactical loop:** receive intelligence and objectives → assign squads and doctrine → deploy → scout and position → engage / adapt / withdraw → meet objectives or accept a partial result → extract and salvage.

**Between-mission loop:** read after-action reports → treat wounded personnel → repair/reconfigure mechs → review promotions and training → examine war developments → choose the next operation.

**Campaign loop:** operational choices consume time and resources → player and AI operations alter regional control, logistics, infrastructure, and morale → new intelligence and mission opportunities emerge → authored events may intervene → the war progresses to victory, defeat, evacuation, occupation, or another outcome.

A mission need not end with the destruction of every opposing unit. A successful reconnaissance, retreat, rescue, or delaying action may be worth more than a tactical victory.

## 3. Tactical control, squad command, and doctrine

### 3.1 Familiar controls

Support ordinary RTS interactions: select one or several units, move, attack a target/area, attack-move, hold/defend, patrol, withdraw, and set rally or waypoint routes. Both individual and squad selection should be supported. The design must remain responsive; players should not have to negotiate every order.

### 3.2 Three layers of instruction

- **Immediate order:** the player's latest specific command, e.g. advance to Point Charlie or engage a marked target.
- **Standing doctrine:** reusable rules such as preferred range, aggression, independence, pursuit limit, engagement conditions, target priority, cover preference, and withdrawal tolerance. Movement orders and engagement doctrine remain separate.
- **Actual behaviour:** tactical execution informed by situation, mech condition, skill, personality, stress, morale, and communication.

Example: set a support mech to **prefer long range**, then order it to move to a ridge. If an enemy closes, it may automatically create distance while continuing to respect its broader mission, unless overridden by a stronger order, incapacity, panic, or a personality-driven mistake.

### 3.3 Squad leaders and radio acknowledgements

Squad leaders translate the player's squad-level intent into local assignments, formations, covering fire, rally attempts, and target allocation. A leader may say, “Alpha, advance to Point Charlie,” followed by individual replies like “On my way” or “I'm too damaged to make that crossing.” Experienced leaders may recommend a safer plan.

A pilot may:
- Follow exactly.
- Interpret sensibly (different route, better cover, preferred weapon range).
- Delay to cool down, reload, or recover.
- Partially comply.
- Withdraw autonomously after severe damage or shock.
- Freeze, panic, refuse, pursue recklessly, charge, rescue someone, or make a heroic last stand.

**Fairness rule:** most routine orders should work. Unusual deviations should have understandable causes, visible indicators, and usually an audible/text warning. Show **ordered task vs actual action** in the interface.

### 3.4 Autonomy and leadership

The initial AI can use a **utility-scored decision layer** to choose between attack, move, take cover, reposition, defend ally, withdraw, eject, and so on, with a state machine/behaviour tree executing the choice. Do not require machine learning.

Leader capabilities affect squad cohesion, rallying, coordinated fire, replacement command after casualties, and recovery from panic. Non-leaders with high Leadership can still steady or assist nearby comrades. Radio jamming or destroyed communications may isolate units, forcing them to follow last-known orders more independently.

**Possible later feature:** conditional tactical plans, e.g. “Hold ridge; engage at long range; if two mechs are disabled, fall back behind the river.” This should be optional rather than required for basic play.

## 4. Pilots: skills, condition, personality, and progression

### 4.1 Initial five-stat model

| Core stat | Meaning and typical effects |
| --- | --- |
| **Piloting** | Movement control, cornering, balance, evasion, recovery from falls, handling damaged actuators or legs. The machine sets physical limits; the pilot determines how well they are used. |
| **Targeting** | Aiming, leading targets, tracking, firing on the move, and effective use of available sensors and weapons. |
| **Health** | Physical condition, cockpit injury, incapacitation, unconsciousness, survival, and medical recovery. Not merely another trainable skill. |
| **Discipline** | Following orders and doctrine, keeping composure, formation discipline, managing panic, and reporting clearly under pressure. Not the same as good tactical judgement. |
| **Leadership** | Commanding, rallying, coordinating, mentoring, and steadying other pilots. Useful even outside formal squad command. |

A 0–100 representation is a **proposed implementation convenience**, not final balance. Separate trainable attributes from present health, injuries, and temporary status effects.

### 4.2 Personality vs state vs earned traits

**Personality** describes tendencies (cautious, aggressive, independent, protective, steadfast). **Temporary state** includes stress, morale/confidence, shock, fatigue, and physical condition. **Earned traits** arise from events and performance.

Possible positive traits: Deadeye, Ammo Conservation, Cool Under Fire, Iron Will, Guardian, Ace Pilot, Field Commander. They should alter decisions or capabilities in recognisable ways, not just add flat bonuses. For example, an ammo-conscious pilot waits for a better firing solution.

Possible adverse or mixed traits: heightened response to explosions after ejection, fear of fire after a cockpit blaze, recklessness, survivor's guilt, or a fictional fascination with incendiary weapons. Treat serious psychological effects thoughtfully; avoid claiming fictional game traits are realistic diagnoses. Trauma need not always produce harm, and recovery/rehabilitation should be possible.

Traits can interact: a protective pilot who fears fire may still attempt to rescue a friend in a burning mech. Avoid “trait farming” through exploitable thresholds or deliberately injuring personnel.

### 4.3 Rank and promotions

Promotions reflect service, conduct, leadership, and mission performance, not only accumulated XP. Illustrative ranks: Recruit → Corporal → Sergeant → Lieutenant → Captain. **Rank is separate from Leadership**: a brilliant sergeant could be a better squad commander than an inexperienced lieutenant.

Promotions may unlock appointments, doctrines, command capabilities, or responsibility. Commendations, discipline, recommendations, and exceptional conduct can be logged.

### 4.4 Injury, medical care, and augmentation

Cockpit penetrations, falls, explosions, fire, and ejection may wound a pilot. An injured pilot can be unavailable for days or missions, recover with temporary limitations, or return early at a cost. Longer-term consequences may include prosthetic limbs, implants, or scars. A bionic arm might grant improved control precision in a particular context but also require maintenance or create an equipment interaction. The example “+1 combat skill” is a **flavour proposal**, not a new sixth core stat; its eventual mechanical mapping needs balancing.

## 5. Service records and generated history

**This is a defining feature.** Every pilot receives a persistent, inspectable service dossier, not a generic XP total. It records:
- Assignments, squadmates, campaigns, mission participation, and named engagements.
- Confirmed kills, assists, tactical contributions, rescues, retreats, captures, and failures.
- Promotions, awards, reprimands, and exceptional conduct.
- Injuries, time in the infirmary, prosthetics, traits, and recovery.
- Relationships, lost comrades, leadership succession, and meaningful personal milestones.
- Death, retirement, capture, or transfer, without deleting their history.

**Illustrative service entry:** “Participated in the skirmish at Lucifer's Gate. Credited with five confirmed kills. Lost his mech during the engagement. Spent two months in the infirmary and returned to service with a bionic arm.”

Pilots may earn context-appropriate nicknames based on real history (“Lucky,” “Hawkeye,” etc.), and comrades may use them in chatter. This is optional for later iterations.

**Implementation principle — event first, prose second:** authoritative gameplay/strategic events are recorded as structured data with timestamps, location, participants, causes, and outcomes. Dossiers, after-action reports, war chronicles, and statistics are projections of those events, not independently invented text. Store enough cause-and-effect information to explain *why* events happened.

Pilot histories persist after death in a memorial. Mechs may also have serial-numbered records of pilots, battles, repairs, destroyed parts, and eventual loss.

## 6. Mechs and engineering

### 6.1 Anatomy and damageable components

At minimum: **head, torso/chest, left and right arms, left and right legs**, with separable armour and internal structure. Parts can be swapped, destroyed, disabled, or salvaged. The mech's capabilities are functions of the whole assembly, not just a global health bar.

Examples: damaged leg → reduced speed/stability or fall; destroyed arm → mounted/held weapon lost; damaged head → impaired sensors; torso penetrated → reactor/heat/critical systems at risk. A disabled mech may remain a threat and be captured, salvaged, or recovered.

### 6.2 Slots and loadouts

Parts have equipment **slots** with categories, restrictions, and **affinities**, inspired by the design logic of FF7's materia slots but not its exact implementation. Some slots are dedicated to weapons/equipment types; an appropriate item in a matching slot can gain performance, reliability, cooling, or handling benefits. Universal slots allow flexibility with trade-offs.

Part/system stats may include mass, armour, structural integrity, capacity, power draw, heat generation/dissipation, ammo storage, sensor capability, hardpoint arc, and recoil handling. Chassis and parts should be **data-driven** and support loadout validation.

Possible equipment:
- Lasers of several sizes, machine guns, autocannons, flamers, plasma weapons, railguns.
- Short-, medium-, and long-range missile systems, plus siege/artillery weapons.
- Handheld weapons, fixed mounts, and melee equipment.
- Scanners, radar, jammers, electronic countermeasures, communications uplinks.
- Jump jets, optical camouflage, improved cooling, armour, and ammo modules.

Trade-offs matter: heavy armour vs cooling/slots; large guns vs power/recoil/ammo; sensors vs firepower; missile volume vs vulnerability to ammunition explosions.

### 6.3 Heat, ammunition, and critical failures

Weapons and systems generate heat; dissipation varies by configuration and environment. Overheating can limit performance, damage equipment, or trigger shutdown. Standing in a lake or suitable water can improve cooling while changing positioning and visibility.

Potential combat failures: stall, fall, actuator damage, EMP disruption, jammed sensors, weapon failure, ammo cook-off, runaway heat, reactor/core explosion, cockpit fire, pilot injury, and emergency ejection. These should arise from **understandable component states and selected critical events**, not a costly full mechanical simulation.

### 6.4 Three initial chassis (current art/gameplay direction)

| Chassis | Relative scale | Form language | Battlefield role | Design constraint |
| --- | --- | --- | --- | --- |
| **Heavy Support Platform** | **Largest** | Tall, massive, arm-equipped artillery walker, substantial legs/shoulders | Long-range railgun, missiles, heavy artillery; holds the rear | Slow, valuable, vulnerable when outflanked or rushed |
| **Medium Command / Generalist** | **Middle** | Imposing humanoid, powerful arms, flexible modular equipment | Squad leadership, frontline fighting, flexible loadouts | Broad choice rather than maximum specialisation |
| **Light Scout** | **Smallest** | Lean humanoid, quick limbs, sensor/mobility focus | Recon, spotting, flanking, target designation, electronic warfare | Fragile in open direct engagements |

The **support platform is larger than the command mech**; the command mech should still appear lethal and imposing. The light scout is mobile and capable of meaningful equipment customisation, not a disposable unit.

Art references: support has the **armed-Stormsurge conversion** feeling (large frame carrying a serious cannon); command has the **Riptide** sense of presence; scout has the **Crisis Suit** feeling of agile powered armour. Translate the *design intent*, not protected silhouettes or exact hardware. The owner's painted Riptide offers a useful reference for olive military finish, heavy joints, large weapon and convincing battlefield scale.

### 6.5 Anchored siege mode — signature support mechanic

The heavy platform can transition between:
- **Mobile:** slow movement, defensive fire and some less-effective heavy-weapon operation.
- **Anchored / Siege:** physically deploys spikes, outriggers, or ground stabilisers; immobile while deployed; high recoil tolerance, more accurate heavy fire, full artillery/missile capabilities, potentially improved cooling.

Anchoring and unanchoring take time. Soil, rock, and concrete could eventually affect deployment. Damaged anchors may force shutdown of the main gun or emergency disengagement. Shots can create dust, smoke, dramatic signatures, and reveal the platform's position.

Signature loadouts: **saturation missile battery**, **heavy siege cannon**, **long-range anti-armour railgun**. The support platform becomes especially effective when a scout designates targets and a command mech screens its flanks. Its minimum effective range should arise from slow tracking, limited traverse, and setup time—not an arbitrary prohibition on shooting nearby units.

## 7. Battlefield and combat environment

### 7.1 Terrain and destruction

Mountains, forests, towns, cities, lakes, roads, ridges, valleys, and built infrastructure provide meaningful geography and cover. Missiles crater ground; energy weapons mark surfaces; ballistic weapons damage buildings; structures may collapse or explode; fuel may ignite. Craters and collapsed buildings can affect cover, traversability, and paths.

Fire may spread between mechs, buildings, and vegetation. Smoke affects line of sight, target identification, and sensor effectiveness. Weather and terrain influence visibility and mobility. Wildlife (e.g. goats or sheep) can react and flee, adding lived-in atmosphere later.

**Prototype rule:** fake expensive physical spectacle where appropriate, but preserve gameplay consequences (blocked route, obscured vision, burning area, cover removed, heat change). Avoid committing to fully deformable terrain or exhaustive physics early.

### 7.2 Identification, sensors, EW, and radio

Information is a battlefield resource. Units can discover contacts before identifying them; radar, optics, jamming, stealth, and shared target data affect what the player and squads know. Equipment may permit interception of enemy radio transmissions. Scouts can designate targets for long-range support.

### 7.3 Settlements and collateral damage

Civilian cars, buses, people, settlements, and critical facilities can be present. Noncombatants may flee or be harmed by combat. Missions often reward civilian protection and penalise unnecessary collateral damage. Infrastructure loss (power stations, bridges, hospitals, ports) has strategic consequences. Capture of bases may involve suppressing defenders and securing a command post rather than simply destroying everything.

## 8. Radio, portraits, and feedback

Pilots and leaders speak regularly through event-driven portrait/radio messages: order acknowledgement, contact/ID reports, repositioning, fire support, reload/heat warnings, component damage, panic, retreat, ejection, rallying, rescue, and victory cries. Some useful chatter happens between NPCs, not just towards the player.

The purpose is **personality plus actionable information**. Prioritise important calls so radio does not become an incessant wall of noise. Different personalities can express the same event differently. Enemy radio traffic is usually hidden unless intercepted.

First prototype: portraits, subtitles, event tags, and short reusable lines. Full voice acting is an eventual goal, not an entry requirement.

## 9. Other battlefield forces (future expansion)

- **Infantry:** small Epic-scale-style squads (around 4–8 soldiers), each squad commanded as a unit with individual visible troops, local cover/suppression reactions, a squad leader, morale, and collective experience. Vulnerable in the open; dangerous in buildings, woods, trenches, and anti-armour ambushes. May secure buildings, objectives, pilots, and wrecks.
- **Power-armoured troops:** specialised shock/assault infantry.
- **Conventional vehicles:** tanks, artillery, engineering vehicles, transport and support.
- **Aircraft:** strafing, bombing, recon, and dropship insertions.
- **Grav tanks:** compact, low-profile, agile hover vehicles with railguns, missile pods, visible grav technology, networked targeting and EW. They may define a **distinct faction doctrine**, favouring mobility, precision, and coordination against slower, heavily armoured mechs. Grav propulsion failures can cause tilting, hard landings, or immobilisation. This faction identity is promising but not yet canon.

Not every faction needs identical unit classes, and all these forces can use subsets of the same command, damage, sensor, and event systems.

## 10. Headquarters and between-mission systems

The HQ is initially a **persistent strategic hub**, not a base-placement RTS. Potential facilities:

| Facility | Function |
| --- | --- |
| **Infirmary** | Treatment, rehabilitation, injuries, medical availability, prosthetics. |
| **Mech Bay** | Repair, rearm, refit, body-part swapping, machine readiness. |
| **Training Centre** | Pilot skill development, leadership and discipline training. |
| **Operations Centre** | Squad assignments, doctrine presets, available missions, intelligence. |
| **Salvage Yard** | Breakdown/recovery of captured wrecks and components. |
| **Research Lab** | Unlocks advanced parts, electronics, weapons, cooling, reverse engineering. |

Initial four priorities: **Infirmary, Mech Bay, Training Centre, Operations Centre**. Salvage may be handled within Mech Bay before it warrants its own screen.

Time, repair capacity, medical beds, parts, ammunition, and supply can compete. Deploy a wounded veteran, reconfigure with an imperfect salvaged arm, or delay while the war moves on? Make the choice meaningful without excessive admin.

Pilots gain experience; machines gain **history, modifications, repairs, and quirks**, not human XP. A veteran may pilot a new chassis; a rookie may inherit a famous battered machine.

## 11. Planetary campaign and strategic war

### 11.1 Scope and world structure

The long-term target is **two sides, one planet, established geography**, with recognisable regions and persistent locations. The planet need not be simulated at fine detail everywhere: a strategic map tracks regional control, infrastructure, logistics, forces, intelligence, morale, and significant events.

Procedural battles arise from this state, using authored terrain anchors/geographic identity rather than random maps disconnected from the world. Locations can change physically and politically across the campaign.

### 11.2 Choosing missions

Potential mission types: reconnaissance, ambush, supply-route interdiction, raid/sabotage, base assault/capture, defence, escort, rescue/extraction, allied support, infiltration, civilian evacuation, power-station/infrastructure protection, delay, and rearguard withdrawal.

The player has freedom to choose many opportunities but cannot do everything. Missions consume strategic time; unseen allies and enemies conduct other operations. An enemy can reinforce, retreat, move supply routes, exploit gaps, or respond to the player's tactics.

Mission outcomes should be multi-dimensional: **tactical, operational, strategic, humanitarian, personnel, and materiel**. A force may lose ground yet rescue civilians, preserve survivors, and delay an offensive.

### 11.3 Scripted events within a procedural world

Authored story missions, characters, and pivotal events are welcome. Their circumstances respond to war state where feasible: prior depot raids affect enemy ammo; destroyed bridges affect approaches; poor recon affects intelligence; injuries affect available squads. Afterward, the result returns to simulation.

Off-screen events can include weather, political developments, reinforcements, unrest, civilian crises, command decisions, supply problems, intelligence failures, and technological discoveries. Prefer **state-weighted causal events** over random unrelated surprises.

### 11.4 Higher command and other commanders

The player may receive orders to support another commander, infiltrate enemy lines, rescue an encircled unit, defend a civilian power station, evacuate civilians, or retreat to a spaceport for off-world withdrawal. Allied commanders have their own objectives, strengths, failures, and potential persistence. Cooperation and friction create story opportunities.

Higher command can order withdrawal when the war is going badly. This should not force a game-over due to inability to fight to the last person.

### 11.5 War outcomes and persistence

Possible endings or transitions: military victory, negotiated outcome, strategic defeat, organised evacuation, stranded resistance/guerrilla action, occupation, or surrender. A lost battle or planet is not automatically a failed *story*.

The **War Chronicle** records major battles, territorial changes, why offensives were delayed, infrastructure outcomes, commander careers, and civilian impact. The same event feeds pilot dossiers, mech histories, mission summaries, and strategic reporting.

## 12. Art direction

**Working style statement:** Grounded military science-fiction mechs with slightly stylised, highly readable silhouettes and convincing industrial construction.

- Strong silhouette distinction at tactical camera scale.
- Weight, armour plating, actuator mechanics, visible hardpoints and cooling systems.
- Variety: humanoid command/scouts, giant anchored support, later unconventional walkers.
- Military olive, gunmetal, charcoal, camouflage, field repair, scars and practical faction markings; avoid excessively sleek uniformity.
- Shared engineering vocabulary so modular parts look like they belong together.
- Functional design first, surface detail second.
- Restrained exaggeration in guns and proportions, not cartoon super-robot heroics.
- Avoid direct copies of BattleTech, Warhammer/T'au, or other franchises.
- Scale reinforced by infantry, vehicles, buildings, trees, and civilians.

Use an internal art bible with silhouette tests, joint/attachment standards, asset naming, colours/materials, VFX language, and references. No final in-world chassis/faction names are set yet.

## 13. Technical architecture — proposed, not decided

This is a systems decomposition rather than a commitment to an engine.

1. **Simulation data layer:** pilot profiles, chassis/part definitions, equipment configurations, squads, doctrine, world sites, missions and inventories. Prefer data-driven assets.
2. **Command layer:** direct orders and standing policies; a separation between intended orders and actual pilot action.
3. **AI layer:** tactical utility choices + execution behaviours; morale/stress and leader modifiers.
4. **Combat layer:** targeting, LOS/sensors, projectiles, range, heat, armour/components, critical states, damage and ejection.
5. **Environment layer:** terrain/cover, limited destructibles, fire/smoke/water and civilian entities.
6. **Narrative event layer:** typed, persistent events with subjects, location, timestamp, cause and outcome. Derive UI chatter, service records, AARs, memorials, and chronicle.
7. **Strategic layer:** region graph, logistics and supplies, force posture, AI operations, missions and world events. Can resolve most off-screen conflicts abstractly.
8. **Presentation layer:** RTS camera and controls, unit selection, command cards, pilot portraits, health/part status, tactical overlays, HQ screens, reports and audio.

Maintain a distinction between **authoritative game state**, **event/history records**, and **generated narrative text**. Avoid unbounded logging of every bullet; store important events and derived summaries. Deterministic seeds and save/replay tests would help debug surprising outcomes.

## 14. Initial playable prototype (recommended vertical slice)

**Scenario: “The Village”** (placeholder). A friendly mechanised unit approaches a village with an enemy-held command post. The player must disable or drive off defenders, capture the post, and minimise civilian harm. Reconnaissance and long-range fire support should provide meaningful alternatives to charging in.

### In scope

- Three original prototype chassis: medium command, small scout, heavy support.
- A four-mech friendly detachment; a small hostile force with basic tactical AI.
- Standard selection, movement, attack and simple squad orders.
- Basic doctrine: engagement range, target preference, pursuit limit and damage-triggered withdrawal.
- Five pilot stats plus a small number of personality traits and stress/morale states.
- Named pilots, radio text/portraits, acknowledgements, warnings, and at least one meaningful autonomous deviation.
- Head/torso/arms/legs with armour and component damage; weapons can be disabled, mechs can become immobilised, pilots can eject or be wounded.
- First-pass loadout system with interchangeable parts/slots; a small weapon selection (e.g. laser, ballistic gun, missile launcher, heavy railgun).
- A scout spotting/designating targets; a support mech anchoring/unanchoring and firing a powerful long-range weapon.
- One map with cover, water/cooling, limited destructible objects and optional basic smoke/fire.
- Mission outcomes including success, partial success, withdrawal, casualties and salvage.
- Basic after-action report; persistent pilot service entries; lightweight Mech Bay/Infirmary state between missions; save/load.

### Explicitly *not required* for first playable slice

Planet-wide strategic AI; full procedural maps; infantry, air units, grav faction; full voice acting; advanced weather; destructible cities; detailed medical simulation; sophisticated interpersonal relationships; research tree; multi-region campaign; flawless terrain deformation; multiplayer.

### Prototype success criteria

1. RTS control is responsive and readable with four mechs.
2. The scout can discover/designate a target which benefits long-range support.
3. The heavy support can deploy anchors, deliver distinctive ranged fire, and become vulnerable to close pressure.
4. Losing an arm or leg changes what a mech can do and how its pilot behaves.
5. An AI pilot can warn, refuse/delay, retreat or adapt in a clearly explainable circumstance; the player can still understand and respond.
6. A completed mission leaves persistent changes in pilots, machines, inventory, and an inspectable service record after save/reload.
7. Partial failure (e.g. friendly withdrawal or damaged equipment) produces a coherent result rather than an automatic restart.

## 15. Incremental prototype plan

**Milestone 0 — Technical/art spike**
- Choose engine and visual target (3D environment with RTS camera is a strong candidate, not a locked decision).
- Build a greybox map and single humanoid placeholder mech with selectable movement/camera.
- Test modular model/part attachment, basic animation, collision, and performance.
- Test one gun, one target, one damageable component.
- Check external asset provenance if using MechCommander material for local experiments.

**Milestone 1 — Playable firefight**
- Standard selection/move/attack and camera.
- Enemy acquisition, firing, armour, heat, basic damage and victory/withdrawal.
- One useful map and combat feedback.

**Milestone 2 — Three-chassis tactics**
- Command, scout and anchored heavy support implemented with distinct roles.
- Target designation, engagement ranges, simple sensor/LOS, configurable weapons.
- Initial squad selection and standing orders.

**Milestone 3 — Pilots and behaviour**
- Five stats, personality, stress/morale, squad leader order relay.
- Event-driven portraits/chatter.
- Autonomous safety withdrawal, tactical interpretation and rallying.
- Player-facing explanation of unexpected behaviour.

**Milestone 4 — Persistence and HQ**
- Mission debrief, significant event capture, service record projection, saves.
- Injury/infirmary, mech repair/refit, salvage, pilot progression.
- Lightweight repeatable mission cycle.

**Milestone 5 — Small living-war experiment**
- Fixed map of a handful of connected regions.
- 2 sides, 2–4 mission types, supply/control/intelligence variables.
- One scripted event with dynamic conditions.
- War-state update and chronicle entry after each mission.

At each milestone, preserve a small playable build and cut features before compromising the core loop.

## 16. Risks and design safeguards

| Risk | Mitigation |
| --- | --- |
| AI disobedience feels like broken controls | High baseline compliance; visible intentions; warnings and meaningful reasons; adjustable doctrine. |
| Systems overwhelm the player | Default doctrines and loadouts; actionable radio; concise status UI; reveal complexity progressively. |
| Endless feature creep | Vertical slice and explicit out-of-scope list; separate core, next, and future ideas. |
| Procedural war feels arbitrary | Persistent geography, causal simulation variables, clear strategic reports, authored anchors. |
| Damage/destruction overwhelms performance | Selective components, coarse simulation, staged VFX, gameplay-relevant cover states. |
| All factions feel interchangeable | Different unit compositions, technology, logistics and doctrinal strengths. |
| Pilot progression rewards harming characters | Balanced medical consequences; viable voluntary upgrades; no injury-farming loops. |
| Copyright/trademark/asset reuse issues | Original art and names; licence audit; separate third-party references/assets; no presumed public domain. |
| Records drift from what happened | One authoritative event source; record causes and participants; derive prose from facts. |

## 17. Open decisions

These are *deliberately unresolved*, not gaps to silently assume away.

1. Game engine and pipeline (plus terrain/modularity/destruction approach).
2. Camera distance and visual fidelity target: full 3D tactical view, projection and zoom limits.
3. Exact body-part/slot schema and how much cross-chassis part interoperability to permit.
4. AI doctrine UI, manual pilot overrides and the balance between autonomy and control.
5. Weapon categories, ranges, heat/ammo curves, salvage probabilities and damage granularity.
6. Campaign time model and how much player control exists over deadlines and higher-command orders.
7. Planet/faction names, setting, technology rules, military organisation and political stakes.
8. How scripted major events are seeded and constrained by the procedural war.
9. Pilot rank structure, career traits and injury/augmentation balancing.
10. Asset source, art bible, scale, animation standards and final names for the three chassis.
11. Save-game schema, event-log retention rules, replayability and test instrumentation.
12. Whether battles are single continuous maps, generated encounter maps, or hybrid persistent authored areas.

## 18. Next working session: recommended decisions

Before committing to a large codebase, settle **(a)** engine and rendering approach; **(b)** first map/camera and mech scale; **(c)** the minimum pilot/mech/weapon data model; and **(d)** the first combat test: a command mech moves, aims, fires, takes limb damage, and logs that event. The next feature should be the support mech's anchor-to-fire transition, followed by scout target designation.

**Guiding promise:** *You give the orders. Your people try to carry them out. The battlefield decides what happens next.*
