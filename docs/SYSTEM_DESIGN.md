# Gameplay systems and engineering design

This document explains the architecture described in the individual report, game manual and final presentation. It is an engineering account of the course project, not a claim that a new build or test suite was executed.

## Inventory model and interaction

The individual report describes KnapsackMgr as the data repository, item and slot classes as interaction/data adapters, and the inventory panel as presentation. The player collects items, stacks repeated items, sees quantity labels, drags items between slots, reads hover information and selects a use action.

The separation between model state and UI hierarchy is central to persistence. A visible slot is not itself the complete item model; item identity, quantity and placement need to agree. The presentation describes obtaining an available slot's parent index to avoid overlapping item UI.

The material documents an MVC design and names its classes, but does not expose a formal schema for every item type or a measured inventory complexity bound. Those details are not invented here.

## Save/load boundaries

The reported JSON snapshot includes scene information, player/NPC locations, object IDs and state, item visibility and inventory presentation information. Saving collects runtime state; loading parses it and assigns state back to objects and interfaces. Reset clears prior saved progress. A per-scene singleton manager supports automatic saving.

Important consistency questions for this design are whether collected objects stay hidden after loading, inventory contents agree with world visibility, NPC positions are restored, and task progression resumes correctly. These are derived acceptance criteria, not passing tests newly asserted by this repository.

Versioned save schemas, atomic file replacement, checksums, migration handling and encrypted persistence are not established by the supplied project materials.

## Task progression

Objectives are disclosed after preceding stages are completed. The task panel therefore represents progression state rather than merely a static list. The individual report describes three task sections, while final scene documentation includes multiple locations and transitions. Chapter naming changed during development.

A coherent load operation should reconstruct scene, completed objectives and the currently actionable goal. The documents establish the design relationship; there is no new runtime verification in this showcase.

## Accounts and personal contribution

Username/password registration and login use a MySQL database. The report describes account lookups and restrictions on incorrect inputs. Face recognition was a collaborative feature, with partial ideas supplied by Ashley Liu. No production security, password-hashing implementation or authentication accuracy metric is inferred.

Historical cloud addresses, database access details and account records are omitted. A public runnable account service is not included.

## Character and combat coordination

The presentation describes IUserInput, KeyBoardInput, MyKey and gamepad interaction as input handling; ActorController translates input into movement and animation conditions. StateManager, BattleManager and WeaponManager contribute action, hit and weapon-collider state to ActorManager.

This decomposition separates input interpretation, action constraints and combat outcomes. The team presentation explains restrictions during jumps and rolls and multiple attacks. These are team-level features; this document does not attribute the complete combat architecture to Ashley Liu.

## Engineering reflection

The design report contains functional requirements, acceptance cases and risk analysis. The presentation discusses baked lighting, mesh batching, texture compression, collision work and object pooling. These are documented techniques, not controlled profiling results.

Useful future verification would include save/load invariants, quest transition tests, duplicate item handling, missing-object behavior, login error cases and repeatable Unity Profiler captures. Those are proposed checks and are not included in the historical results.

