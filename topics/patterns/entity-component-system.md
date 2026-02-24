# Entity Component System (ECS) 

ECS is an architectural pattern primarily used in game development that separates data from behavior,

- Entity – just an ID (no logic).
- Component – pure data (no behavior).
- System – logic that operates on entities having specific component sets.
 
Core idea: _Behavior lives in systems. State lives in components. Entities are identifiers._

## Why ECS exists (vs OOP)

Traditional OOP in games:
- Deep inheritance trees (Player extends Character extends Sprite).
- Hard to compose behaviors dynamically.
- Tight coupling between state and behavior.

ECS:
- Add/remove features by attaching/removing components.
- Data is separated from logic.
- Systems are reusable and independent.

Trade-offs:
- More boilerplate.
- Harder mental model initially.
- Indirection can hurt debugging.
- Great for large-scale simulations; overkill for small projects.


## System

Systems iterate over entities that have required components.

Systems run in deterministic order. Ordering matters:
- Physics before rendering.
- Input before physics.

Ideally, systems are Pure Functions

## Resources

A resource is global singleton-like data not tied to a specific entity.

Examples:
- Delta time
- Game settings
- Input state
- Score
- Asset manager
- RNG seed

Instead of attaching these to entities, you store them in a shared container.

Systems receive resources


## ECS in Real Game Dev

Where it shines
- Many similar objects (bullets, enemies, particles).
- Dynamic composition (power-ups, status effects).
- Performance-sensitive updates.
- Multiplayer deterministic simulations.

Where it’s overkill
- Small UI-driven games.
- Simple slot games (unless engine-level reuse needed).
- When object graph is small and stable.

## When Should You Use ECS?

Use it if:
- You’re building reusable engine infrastructure.
- You expect dynamic composition of behavior.
- You want scalable architecture for many entities.

Avoid it if:
- Your game is mostly UI and state machines.
- You have <50 active objects.
- You don’t need high simulation flexibility.


## Related concepts

### Composition over Inheritance

Instead of:
```typescript
class BossEnemy extends FlyingEnemy
```

You compose:
- Health
- Fly
- BossAI
- PhaseController

ECS is extreme composition.

### Data-Oriented Design (DOD)

Very closely related.

DOD focuses on:
- Memory layout
- Cache locality
- Linear iteration

Modern ECS (Unity DOTS, bitecs) is often DOD-first.

Difference:
- ECS = architectural pattern.
- DOD = performance philosophy.

They often overlap but are not identical.


### Dependency Injection (DI)

In OOP:
- Objects depend on services.

In ECS:
- Systems depend on component stores.
- World object acts as service container.

It’s a different flavor of dependency inversion.
