# Desecration PRD v1.0

A modern, darkly funny, third person wizard battle game inspired by *Sacrifice*, built in Unity, starting with the smallest playable proof of fun and architected carefully enough that multiplayer can come later.

This document is frozen as v1.0. Do not expand scope until the first fun test exists.

---

# Important Constraint

Do not let the AI start with lore, menus, campaign, five gods, real multiplayer, complex AI, polished graphics, deep progression, object pooling, an event bus, or unnecessary architecture.

The first sacred milestone is this:

**One ugly arena. One Rot god. One wizard. Two or three creatures. Two spells plus one spectacle spell. Spirits. Altars. A scripted rival. Win condition.**

The prototype succeeds only if this is fun while ugly.

Everything else waits.

---

# Locked Decisions

| Area | Decision |
|---|---|
| Engine | Unity |
| Language | C# |
| Input | Unity New Input System |
| First God | Rot |
| Visual Style | Modern stylised dark fantasy using free or low cost assets |
| Camera | Adjustable, like Sacrifice: close enough for duelling, pulled back enough for tactical awareness |
| Controls | WASD movement, mouse camera and aiming, hotkeys for spells and commands |
| Terrain Deformation | Visual only in the first slice: decal, particles, scorch or crater illusion, camera shake |
| Creature Movement | Unity NavMeshAgent for the prototype |
| Command Targeting | Crosshair raycast from the wizard camera |
| Board | GitHub Issues as source of truth, GitHub Projects as board view |
| Working Title | Desecration |
| AI Workflow | Claude builds, Codex reviews, Shaun gates risky changes |

---

# Product Brief

## Core Fantasy

You are a deranged wizard chosen by a grotesque god. You run across a cursed battlefield, cast brutal spells, summon warped creatures, harvest fallen spirits, corrupt enemy altars, and scar the land while your god laughs at your suffering.

## First Prototype Goal

The first build must answer one question:

**Is this fun when it is ugly?**

Not polished. Not balanced. Not finished. Fun.

## First Playable Target

The first milestone is:

1. Run around as a wizard.
2. Cast a basic Rot attack spell.
3. Kill neutral creatures.
4. Harvest Spirits.
5. Return Spirits to your altar.
6. Spend Spirits to summon creatures.
7. Use simple creature commands: follow me and attack my crosshair target.
8. Fight a scripted rival force.
9. Use one big Rot spectacle spell that visually scars the ground.
10. Corrupt the enemy altar and win.

This is the smallest version that proves the loop.

---

# Prototype Definition of Done

This is the contract for the whole prototype.

The prototype is done when:

1. Moving around feels responsive.
2. Rot Bolt feels punchy.
3. Hits have feedback: impact VFX, sound, camera shake, optional hit stop, and readable damage.
4. Killing creatures creates useful Spirits.
5. Returning Spirits to the altar feels like a meaningful risk.
6. Summoning a creature feels immediately useful.
7. Commands are simple but effective.
8. The scripted rival creates pressure.
9. The Rot god spell makes the player grin.
10. The enemy altar can be corrupted and the match can be won.

## Kill Switch

If the first fun test is complete and Shaun does not want to play again, stop.

Do not add multiplayer, more gods, campaign, more creatures, progression, polish, or better art to rescue it.

Instead, diagnose the failure in this order:

1. Movement and camera feel.
2. Rot Bolt and combat feedback.
3. Spirit collection and return tension.
4. Creature usefulness.
5. Rival pressure.
6. Altar corruption clarity.
7. God spell spectacle.

Only continue if the problem can be stated clearly and fixed with one focused iteration.

If the problem is “the core loop is not fun,” shelve or radically redesign the project before investing more time.

---

# What Changed From v0.2

1. The Ground Remembers is now a standard VFX and gameplay spectacle issue, not a technical terrain issue.
2. The terrain risk is explicitly scope creep into real terrain deformation.
3. Spirit Economy Config is specified as one ScriptableObject with public fields and no custom editor.
4. Simple command targeting is defined as a crosshair raycast.
5. NavMesh setup is now a dedicated Phase 0 issue.
6. Object pooling and event bus architecture are explicitly forbidden before approval.
7. Prototype Definition of Done is now a contract.
8. A kill switch was added to prevent sunk cost escalation.

---

# Visual and Asset Plan

For now, the visual style should be:

**Stylised dark fantasy, colourful, grotesque, readable, and cheap to assemble.**

Do not chase realistic AAA yet. Realistic AAA with free assets usually looks inconsistent. Stylised visuals let the project hide rough edges and move faster.

## Starting Asset Sources

Use these sources first:

1. Kenney for general prototype assets.
2. Quaternius for free low poly 3D models.
3. Quaternius animation packs where licensing is confirmed per pack.
4. Mixamo for humanoid rigging and animation, used inside the game only.
5. Freesound for placeholder SFX, only with per asset license tracking.
6. Unity Asset Store free assets for terrain, particles, shaders, prototype creatures, UI, and effects.

## Asset Register Rule

Every third party asset gets logged from day one.

Track:

1. Asset name
2. Source
3. Author
4. License
5. URL
6. Whether it can ship commercially
7. Replacement needed later: yes or no
8. Notes or restrictions

## Enforced Asset License Rule

Every imported asset under:

```text
Assets/ThirdParty
```

must have a nearby license file:

```text
.asset-license.md
```

The validation script should live under:

```text
Assets/Tools/AssetLicenseValidator
```

The validator should fail CI or emit a clear warning if a third party asset folder has no license file.

---

# First God

## Vessara, God of Rot

Vessara should be disgusting, cheerful, cruel, and weirdly affectionate.

Personality:

> She loves decay because decay is honest. Everything proud eventually leaks.

## Core Mechanics

1. Poison.
2. Disease.
3. Insects.
4. Corpse use.
5. Weakening enemies.
6. Swarming.
7. Healing from rot.

## First Creature Roster

### Pusling

Small harasser. Fast, weak, annoying. Good for harvesting Spirits.

### Bloat Brute

Slow melee tank. High health. Can receive a death burst later, but not required for first fun test.

### Spore Spitter

Ranged creature. Fires arcing poison globs.

For the absolute first playable test, implement Pusling and Bloat Brute first. Spore Spitter can wait until the first loop works.

## First Spell Roster

### Rot Bolt

Basic projectile. Deals damage and applies a short decay effect.

### Carrion Bloom

Area spell. Poison cloud on the ground. Can be delayed until after the core loop works.

### The Ground Remembers

Huge Rot god spell. The land appears to cave in, green rot erupts, enemies are damaged or slowed, and the ground is visually scarred.

For the first slice, **The Ground Remembers does not edit real Unity terrain heightmaps.**

It uses:

1. dark ground decal
2. particle burst
3. temporary mesh or projected scar
4. camera shake
5. area damage
6. optional slow effect

Real terrain deformation is a later milestone.

---

# Spirit Economy v0

These are placeholder values. They must be data driven and tunable without code changes.

| Entity or Action | Spirit Value |
|---|---:|
| Neutral weak creature drops | 1 Spirit |
| Neutral tough creature drops | 2 Spirits |
| Enemy Pusling drops | 1 Spirit |
| Enemy Bloat Brute drops | 2 Spirits |
| Pusling summon cost | 1 Spirit |
| Bloat Brute summon cost | 3 Spirits |
| Spore Spitter summon cost | 2 Spirits |
| Max carried Spirits by Pusling | 1 Spirit |
| Max carried Spirits by wizard | 3 Spirits |
| Spirit return time | 3 to 6 seconds depending on distance |
| Altar corruption required | 10 corruption points |
| Pusling corruption rate | 1 point every 3 seconds |
| Bloat Brute corruption rate | 1 point every 2 seconds |

## Economy Design Goal

The player should be forced to choose:

1. spend Spirits now to build pressure
2. save Spirits for stronger creatures
3. risk moving forward to collect more
4. defend harvesters returning to altar
5. interrupt enemy corruption

---

# System Architecture

Build these as separate systems from the start:

1. Player controller
2. Camera controller
3. Spell system
4. Combat feedback system
5. Creature system
6. Simple command system
7. Spirit system
8. Altar system
9. God loadout system
10. Scripted rival system
11. Terrain impact presentation system
12. Match state system
13. Presentation hooks for VFX, SFX, camera shake, and UI

## Core Principle

**Gameplay events first, visuals second.**

Example flow:

1. Spell hits ground.
2. Spell impact result is calculated.
3. Damage system applies damage.
4. Terrain impact presentation appears.
5. Particles play.
6. Sound plays.
7. Camera shakes.

This keeps multiplayer possible later because the simulation can eventually be separated from the visual spectacle.

Important: do not introduce a generic event bus yet. Use direct references, UnityEvents, or small local C# events where they are immediately useful. A central event bus is deferred until the project actually needs it.

---

# Suggested Unity Folder Structure

```text
Assets/
  Game/
    Core/
    Player/
    Camera/
    Combat/
    Spells/
    Creatures/
    Spirits/
    Altars/
    Gods/
    AI/
    Terrain/
    UI/
    Audio/
    VFX/
    Prototype/
  ThirdParty/
  Art/
  Audio/
  Scenes/
  Tools/
```

---

# GitHub Setup

Use both:

1. GitHub Issues for individual tasks.
2. GitHub Projects for the board.

## Board Columns

1. Backlog
2. Ready for AI
3. In Progress
4. Needs Human Review
5. QA
6. Done

## Issue Labels

1. `phase prototype`
2. `phase vertical-slice`
3. `area player`
4. `area spells`
5. `area creatures`
6. `area spirits`
7. `area altar`
8. `area ai`
9. `area terrain`
10. `area camera`
11. `area ui`
12. `area audio`
13. `area architecture`
14. `area combat-feel`
15. `risk high`
16. `agent ready`
17. `needs review`
18. `blocked`

---

# Issue Template

Use this for every AI task:

```md
# Goal

# Context

# Requirements

# Acceptance Criteria

# Implementation Notes

# Test Plan

# Definition of Done

# Risks

# Follow up Issues
```

---

# Agent Rules

Claude builds.

Codex reviews.

Shaun gates risky changes.

## For Each Issue

1. Claude creates a branch.
2. Claude implements only that issue.
3. Claude does not broaden scope.
4. Claude writes or updates tests where practical.
5. Claude opens a PR.
6. Codex reviews for architecture, bugs, overengineering, dependency creep, and missed acceptance criteria.
7. Shaun approves only after it runs in Unity.

## Claude Must Not Do Without Approval

1. Add new dependencies.
2. Create new top level systems.
3. Add networking.
4. Add inventory.
5. Add dialogue systems.
6. Add save/load.
7. Add procedural generation.
8. Add campaign systems.
9. Add object pooling.
10. Add a generic event bus.
11. Refactor unrelated code.
12. Import paid assets.
13. Change input framework.
14. Change terrain approach.
15. Change AI architecture.
16. Replace the folder architecture.

Agents love scaffolding. This project does not need scaffolding. It needs a fun loop.

---

# Revised Issue Backlog

The v0.3 backlog is built to reach the first fun test quickly and reduce agent ambiguity.

---

# Phase 0: Project Foundation

## 1. Create Unity Project for Desecration

Labels: `phase prototype`, `area architecture`, `agent ready`

Goal: Create the Unity project and repository foundation.

Acceptance criteria:

1. Unity project opens cleanly.
2. Git ignore is correct for Unity.
3. Unity New Input System is installed and enabled.
4. Main prototype scene exists.
5. Project runs with no console errors.

## 2. Create Base Folder Structure

Labels: `phase prototype`, `area architecture`, `agent ready`

Acceptance criteria:

1. Folder structure matches the PRD.
2. No unrelated systems are created.
3. Empty README files or placeholders exist only where useful.

## 3. Add Asset License Register and Validator

Labels: `phase prototype`, `area architecture`, `agent ready`

Acceptance criteria:

1. Asset register file exists.
2. Third party asset folders require `.asset-license.md`.
3. Validation script lives under `Assets/Tools/AssetLicenseValidator`.
4. Validation script reports missing license files.
5. Unknown license assets are marked unsafe.
6. Unsafe assets are not used in public builds.

## 4. Create Prototype Arena Scene

Labels: `phase prototype`, `area terrain`, `agent ready`

Acceptance criteria:

1. Arena has player altar.
2. Arena has enemy altar.
3. Arena has three neutral spawn zones.
4. Arena has basic terrain or floor height variation.
5. Arena has clear navigation paths.
6. Lighting gives dark fantasy mood.
7. Scene is ugly but playable.

## 5. Set Up Prototype NavMesh

Labels: `phase prototype`, `area terrain`, `area creatures`, `agent ready`

Acceptance criteria:

1. Prototype arena has a baked NavMesh.
2. NavMesh covers the main playable area.
3. NavMesh avoids obvious blocked areas.
4. One test NavMeshAgent can move from player altar to enemy altar.
5. No dynamic NavMesh rebuilding is implemented.

Implementation notes:

1. Use Unity NavMeshAgent for prototype creatures.
2. Do not implement custom pathfinding.
3. Do not implement dynamic terrain aware pathfinding.
4. Do not rebuild the NavMesh at runtime.

---

# Phase 1: Player, Camera, and Feel Baseline

## 6. Implement Third Person Wizard Movement

Labels: `area player`, `agent ready`

Acceptance criteria:

1. WASD movement works.
2. Movement is camera relative.
3. Wizard rotates cleanly.
4. Movement feels responsive.
5. Controller handles uneven ground.

## 7. Implement Adjustable Tactical Camera

Labels: `area camera`, `agent ready`

Acceptance criteria:

1. Camera can sit close behind the wizard.
2. Camera can zoom out for battlefield control.
3. Mouse controls orbit or aim.
4. Camera avoids clipping through terrain.
5. Camera settings are adjustable in inspector.

## 8. Add Basic Wizard Health and Death

Labels: `area player`, `agent ready`

Acceptance criteria:

1. Wizard has health.
2. Wizard can take damage.
3. Wizard can die.
4. Wizard respawns at altar for prototype.
5. Debug UI shows health.

---

# Phase 2: Combat and Spell Feel

## 9. Create Spell Definition System

Labels: `area spells`, `area architecture`, `agent ready`

Acceptance criteria:

1. Spells are data driven.
2. Spell has name, cost, cooldown, cast time, targeting type.
3. Spell can trigger gameplay effects.
4. Spell can trigger VFX and SFX hooks.
5. No generic event bus is created.

## 10. Implement Rot Bolt

Labels: `area spells`, `agent ready`

Acceptance criteria:

1. Player casts projectile.
2. Projectile travels toward aim direction.
3. Projectile damages valid targets.
4. Projectile applies short decay effect.
5. Cooldown works.

## 11. Add Combat Feel Pass

Labels: `area combat-feel`, `area spells`, `agent ready`

Acceptance criteria:

1. Rot Bolt has visible impact.
2. Hit target reacts clearly.
3. Camera shake is available for spell impacts.
4. Floating damage numbers or hit markers exist.
5. Short hit stop or impact pause is evaluated.
6. Spell feels punchy even with placeholder art.

## 12. Implement The Ground Remembers as Visual Spectacle

Labels: `area spells`, `area terrain`, `agent ready`

Acceptance criteria:

1. Spell has dramatic windup.
2. Spell damages enemies in radius.
3. Spell creates visual ground scar using decal, mesh, or projected effect.
4. Spell plays large particles.
5. Spell triggers camera shake.
6. Spell does not edit real terrain heightmaps.
7. Spell does not require NavMesh rebuilding.

Implementation notes:

1. This is a standard VFX and gameplay spectacle issue.
2. The only real risk is scope creep.
3. If implementation touches `Terrain.terrainData`, stop and open a review.
4. If implementation touches runtime NavMesh rebuilding, stop and open a review.
5. If implementation requires a new terrain system, stop and open a review.

---

# Phase 3: Spirits, Economy, and First Summons

## 13. Define Spirit Economy Config

Labels: `area spirits`, `area architecture`, `agent ready`

Acceptance criteria:

1. Spirit values are stored in one ScriptableObject asset.
2. The ScriptableObject uses public fields or serialized fields.
3. No custom inspector is created.
4. No custom editor tooling is created.
5. Creature summon costs are data driven.
6. Spirit drop values are data driven.
7. Altar corruption values are data driven.
8. Shaun can tune values in the Unity inspector without code changes.

## 14. Implement Spirit Drops

Labels: `area spirits`, `agent ready`

Acceptance criteria:

1. Dead creatures drop Spirit.
2. Spirit can be unclaimed.
3. Spirit can be claimed by player team.
4. Spirit has visible placeholder object.

## 15. Implement Spirit Return to Altar

Labels: `area spirits`, `area altar`, `agent ready`

Acceptance criteria:

1. Claimed Spirit can return to altar.
2. Altar stores Spirit count.
3. Spirit count updates UI.
4. Returned Spirit can be spent.

## 16. Implement Summon System

Labels: `area creatures`, `area spells`, `agent ready`

Acceptance criteria:

1. Player can summon creature at valid location.
2. Summon costs Spirit.
3. Creature belongs to player team.
4. Summon VFX plays.
5. Invalid summon location is rejected.

## 17. Implement Pusling

Labels: `area creatures`, `agent ready`

Acceptance criteria:

1. Pusling uses NavMeshAgent.
2. Pusling can move.
3. Pusling can attack.
4. Pusling is weak but fast.
5. Pusling can carry or return one Spirit.

## 18. Implement Bloat Brute

Labels: `area creatures`, `agent ready`

Acceptance criteria:

1. Bloat Brute uses NavMeshAgent.
2. Bloat Brute moves slowly.
3. Bloat Brute attacks in melee.
4. Bloat Brute has high health.
5. Bloat Brute is useful as a front line unit.

---

# Phase 4: Simple Commands and Win Loop

## 19. Implement Crosshair Targeting

Labels: `area player`, `area creatures`, `agent ready`

Acceptance criteria:

1. A raycast from the camera crosshair can identify valid enemy targets.
2. Current target is highlighted or indicated.
3. If no enemy is under the crosshair, current target is cleared or ignored.
4. This system is used by creature attack commands.
5. No RTS selection UI is created.

## 20. Implement Simple Creature Commands

Labels: `area creatures`, `area player`, `agent ready`

Acceptance criteria:

1. Owned creatures follow the wizard by default.
2. Player can command creatures to attack the current crosshair target.
3. Player can command creatures to return or follow.
4. No RTS selection UI is required yet.
5. Command feedback is visible.

## 21. Implement Altar System

Labels: `area altar`, `agent ready`

Acceptance criteria:

1. Player altar exists.
2. Enemy altar exists.
3. Altars track team ownership.
4. Altars store Spirits.
5. Altars act as respawn anchors.

## 22. Implement Altar Corruption Ritual

Labels: `area altar`, `area creatures`, `agent ready`

Acceptance criteria:

1. Creature can start corruption ritual at enemy altar.
2. Corruption progresses over time.
3. Ritual can be interrupted.
4. UI shows corruption progress.
5. Full corruption triggers win.

---

# Phase 5: Scripted Rival, Not Real AI

## 23. Add Neutral Creatures

Labels: `area ai`, `area creatures`, `agent ready`

Acceptance criteria:

1. Neutral creatures use NavMeshAgent.
2. Neutral creatures spawn in arena.
3. Neutral creatures wander using NavMeshAgent.
4. Neutral creatures fight back.
5. Neutral creatures drop Spirit on death.

## 24. Implement Scripted Rival Force

Labels: `area ai`, `agent ready`

Decision: the first rival is the enemy altar, not a visible rival wizard.

Acceptance criteria:

1. Enemy altar periodically spawns enemy creatures.
2. Enemy creatures move toward player altar.
3. Enemy altar triggers one basic Rot style spell on a timer or proximity trigger.
4. Rival creates pressure without complex AI.
5. Behaviour is predictable and debuggable.

Implementation notes:

1. Do not create behaviour trees.
2. Do not create utility AI.
3. Do not create GOAP.
4. Do not create a full enemy wizard brain.
5. Do not create a visible rival wizard yet.
6. Use timed spawns, simple movement goals, and one scripted altar spell.

## 25. Implement Match Win and Loss

Labels: `area architecture`, `area ui`, `agent ready`

Acceptance criteria:

1. Player wins when enemy altar is corrupted.
2. Player loses when own altar is corrupted.
3. Result message appears.
4. Match can restart.

---

# Phase 6: Minimal Personality

## 26. Add Prototype HUD

Labels: `area ui`, `agent ready`

Acceptance criteria:

1. Health is visible.
2. Spirit count is visible.
3. Spell cooldowns are visible.
4. Current command mode is visible.
5. Altar corruption is visible.

## 27. Add Vessara Commentary System

Labels: `area ui`, `area audio`, `agent ready`

Acceptance criteria:

1. Vessara can display text barks.
2. Barks trigger on summon.
3. Barks trigger on death.
4. Barks trigger on victory.
5. Lines are data driven.

Example Vessara lines:

1. “Oh good, something has burst.”
2. “Do not mourn them. They are more useful leaking.”
3. “Rot is just honesty with a smell.”
4. “Bring me the shiny little spirit thing.”
5. “Their altar looks far too clean.”

---

# Deferred Until After First Fun Test

These are deliberately not in the first prototype:

1. Full enemy wizard AI.
2. Behaviour trees.
3. Utility AI.
4. GOAP.
5. Real terrain heightmap deformation.
6. Dynamic NavMesh rebuilding.
7. Multiplayer.
8. Multiple gods.
9. Campaign progression.
10. Save/load.
11. Dialogue system.
12. Complex RTS selection UI.
13. Polished menus.
14. Paid assets.
15. Voice acting.
16. Procedural maps.
17. Inventory.
18. Equipment.
19. Skill trees.
20. Object pooling.
21. Generic event bus.
22. Custom inspectors.
23. Custom editor tooling unless specifically approved.

---

# First Fun Test Statement

The first fun test is complete when Shaun can say:

> I can run around, cast Rot Bolt, kill things, grab Spirits, summon Puslings and Bloat Brutes, command them to attack my target, survive a rival assault, fire off a gross Rot god spell, corrupt the enemy altar, and win. It is ugly, but I want to play again.

That is the milestone.

Once that works, Desecration has legs.
