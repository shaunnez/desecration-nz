# Agent Instructions for Desecration

This repo is for Desecration, a Unity prototype inspired by Sacrifice.

The source of truth is:

docs/desecration-prd.md

## Prime Rule

Do not expand scope.

Build one GitHub issue at a time. Do not implement future issues early.

## Required Workflow

1. Read docs/desecration-prd.md.
2. Read the current GitHub issue.
3. Implement only the current issue.
4. Do not add unrelated systems.
5. Do not refactor unrelated code.
6. Do not add dependencies without approval.
7. Keep changes small and reviewable.
8. Update documentation only when the issue requires it.

## Do Not Build Without Approval

- multiplayer
- object pooling
- generic event bus
- inventory
- save/load
- dialogue system
- procedural generation
- campaign system
- real terrain deformation
- runtime NavMesh rebuilding
- behaviour trees
- utility AI
- GOAP
- custom editor tooling
- custom inspectors
- paid asset imports
- new top level architecture

## Unity Rules

- Use Unity New Input System.
- Use C#.
- Use NavMeshAgent for prototype creature movement.
- Do not use custom pathfinding.
- Do not edit real terrain heightmaps for the first slice.
- Keep the first prototype ugly but playable.

## Definition of Done

A task is done only when:

1. Acceptance criteria are met.
2. Unity opens without console errors.
3. The relevant scene runs.
4. No unrelated systems were added.
5. The change is small enough to review.
