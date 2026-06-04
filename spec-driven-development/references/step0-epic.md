# Step 0 - Epic

## Purpose
Decompose the user's project idea into a structured set of Features. Each Feature becomes its own numbered directory and runs through the full 9-step workflow independently.

This prevents the "giant spec.md" problem - where everything gets crammed into one document and becomes unmanageable.

---

## Two Modes

This step behaves differently depending on whether `epic.md` already exists:

| Situation | Mode | Behaviour |
|-----------|------|-----------|
| `epic.md` does **not** exist | **Init Mode** | Create epic.md from scratch |
| `epic.md` already exists | **Update Mode** | Merge new content into existing epic.md |

Always check for `.specify/epic.md` before doing anything else.

---

## Init Mode - Starting a New Project

### 1. Understand the Full Scope

Ask the user to describe the full vision. Capture:
- The core purpose (what problem does this solve? who is it for?)
- All major capabilities they can think of
- Any known constraints (platform, audience, timeline, tech preferences)

Do not jump to solutions yet - just understand the full picture.

### 2. Identify Features

Break the idea into Features. A Feature is:
- **Independently deliverable** - can be built and tested without other features being complete
- **Meaningful on its own** - a user can experience value from it
- **Reasonably sized** - can be fully specified in one spec.md

**Too big** (split it): "Battle System" covering turn logic + animations + AI + multiplayer
**Right size**: "Turn-Based Battle Core" - just the turn loop and damage calculation
**Too small** (merge it): "Display HP bar" - belongs inside a larger Feature

### 3. Define Feature Boundaries

For each Feature, define:
- **In scope**: what this Feature includes
- **Out of scope**: what is intentionally excluded (reference the Feature that handles it)
- **Dependencies**: which other Features must be complete first

### 4. Sequence the Features

Order by:
1. **Foundation first** - core systems other Features depend on
2. **User-visible value early** - something usable as soon as possible
3. **Risk first** - tackle hard unknowns before they block everything

### 5. Create `epic.md`

Create `.specify/epic.md` using the template below.

---

## Update Mode - Adding to an Existing Epic

### When to Enter Update Mode

- User describes a new capability not yet in the epic
- User realises a Feature is too large and needs splitting
- User wants to merge Features that are too small
- User wants to reprioritise or reorder Features

### Update Process

**A - Read Current State**
Read `epic.md` fully. Note:
- Which Features are [PASS] Complete, [IN PROGRESS] In Progress, or [TODO] Not started
- Current highest Feature number
- Existing dependencies between Features

**B - Analyse the New Input**
Classify each piece of new input the user has described:

| Input Type | Action |
|-----------|--------|
| New capability not in any existing Feature | Add as new Feature(s) |
| Capability belonging to an existing [TODO] Feature | Expand that Feature's scope |
| Capability belonging to a [PASS] or [IN PROGRESS] Feature | Create a new follow-on Feature - never modify completed work |
| Existing Feature that is too large | Split into two or more Features |
| Existing Features that are too small | Merge into one Feature (only if both are [TODO]) |

**C - Assign Numbers**
New Features continue from the current highest number.
Example: if existing Features go up to `007`, new ones start at `008`.
Never renumber existing Features - this would break directory references.

**D - Check Dependencies**
For each new or modified Feature, verify:
- Does the new Feature depend on any existing Feature?
- Does any existing Feature now depend on the new Feature?
- Does splitting a Feature create new dependencies between the resulting pieces?

**E - Update `epic.md`**
- Add new rows to the Feature Map table
- Add new Feature Summary sections
- Update Delivery Plan phases if needed
- Update `## Last Updated` date
- Do NOT change the Status of any existing Feature

---

## `epic.md` Template

```markdown
# Epic: [Project Name]
**Created:** YYYY-MM-DD
**Last Updated:** YYYY-MM-DD
**Status:** Active

## Vision
[2-3 sentences: what is this project and who is it for?]

## Feature Map

| # | Feature ID | Feature Name | Priority | Depends On | Status |
|---|-----------|--------------|----------|------------|--------|
| 1 | 001-player-movement | Player Movement & Map | P0 | - | [TODO] Not started |
| 2 | 002-pokemon-data | Pokemon Data & Roster | P0 | - | [TODO] Not started |
| 3 | 003-battle-core | Turn-Based Battle Core | P0 | 001, 002 | [TODO] Not started |

## Priority Definitions
- **P0** - Core; project cannot function without this
- **P1** - Important; needed for a complete experience
- **P2** - Enhancement; adds depth but not required for v1

## Feature Summaries

### 001 - Player Movement & Map
**In scope:** Top-down tile map, player movement, collision detection, screen transitions, encounter zones
**Out of scope:** NPC dialogue, trainer battles (-> 008)
**Dependencies:** None
**Delivers:** A playable world the player can walk around in

[repeat for each feature]

## Delivery Plan

### Phase 1 - Foundation (P0)
Complete 001, 002, 003 in order.
**Milestone:** [What becomes possible after this phase]

### Phase 2 - Core Experience (P1)
Complete 004, 005, 006, 007.
**Milestone:** [What becomes possible after this phase]

### Phase 3 - Depth & Polish (P2)
Complete 008, 009.
**Milestone:** [What becomes possible after this phase]

## Change Log
| Date | Change | Reason |
|------|--------|--------|
| YYYY-MM-DD | Initial epic created | - |

## Active Feature
**Currently working on:** 001-player-movement
```

---

## Feature Status Definitions

| Status | Meaning |
|--------|---------|
| [TODO] Not started | Not yet begun |
| [IN PROGRESS] In progress | Currently in Steps 1-8 |
| [TESTING] Testing | Currently in Step 9 |
| [PASS] Complete | All 9 steps done, all tests passing |
| [BLOCKED] Blocked | Waiting on a dependency Feature to complete |

---

## Gate

### Init Mode Gate

Show the complete `epic.md`, then output:

```
---
[PASS] Step 0 - Epic created

Output: Output: .specify/epic.md
   Features identified: [N] across [M] phases

Review: Please review the feature breakdown. When ready:
  - "continue" or "next" -> begin Feature 001, starting at Step 1
  - "revise [what]" -> adjust the breakdown before starting
  - "split [feature ID]" -> break a feature into smaller pieces
  - "merge [feature IDs]" -> combine features that are too small
  - "stop" -> pause here; say "continue from Feature 001" to resume
---
```

### Update Mode Gate

Show only the changes made to `epic.md`, then output:

```
---
[PASS] Step 0 - Epic updated

Output: Output: .specify/epic.md (updated)

Added: Added: [list new Features with IDs]
Split:  Split: [list any Features that were split]
Merged: Merged: [list any Features that were merged]
Dependencies: Dependency changes: [list any new or changed dependencies]

WARNING:  Features already [PASS] Complete or [IN PROGRESS] In Progress were NOT modified.

Review: When ready:
  - "continue" -> resume the current active Feature
  - "start [feature ID]" -> jump to a specific Feature
  - "revise [what]" -> adjust further before continuing
  - "stop" -> pause here
---
```

---

## Rules

1. **Never renumber existing Features** - directories already exist; renumbering breaks all references
2. **Never modify [PASS] Complete Features** - if new scope belongs there, create a follow-on Feature instead
3. **Always record changes in the Change Log** - preserve the history of scope decisions
4. **New Features always get the next available number** - do not reuse numbers even if there are gaps
5. **Re-check all dependencies after every update** - adding a Feature can create new dependency chains
