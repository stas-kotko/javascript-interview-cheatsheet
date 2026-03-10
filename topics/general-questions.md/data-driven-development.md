# Data-Driven Development (DDD)

Data-Driven Development (DDD) is a broad software development paradigm that emphasizes **defining behavior and logic based on data**, rather than hardcoding everything in code. It’s especially useful when you want flexibility, reusability, or the ability to tweak behaviors without recompiling.

## ECS and Data-Driven Development (DDD)

ECS is almost inherently data-driven.

Data-driven development means:
- Behavior is determined by data, not hardcoded class hierarchies.
- Game objects are configured via data (JSON, configs, prefabs).

The systems decide behavior based on the presence of components.

That’s textbook data-driven design.

### Why this matters:
- Designers can configure entities without changing code.
- You can serialize full game state easily.
- Easier balancing and tuning.

### ECS vs “Just Config Files”

Important distinction:
- Data-driven OOP = classes still own behavior.
- ECS = behavior fully externalized into systems.

ECS pushes DDD much further by structurally separating state and logic.

## Relation to Data-Oriented Design (DOD)

Data-Oriented Design is a **performance-focused methodology**. Instead of thinking in terms of objects and inheritance, DOD encourages you to:
- Think in terms of data layout: how it’s accessed and stored in memory
- Optimize for cache locality, SIMD, batching, etc.
- Separate data from behavior to allow better parallelism and predictability

How it’s related to DDD:
- Both separate data from logic in a way
- DOD wants structured, tight data layouts for performance
- DDD structures systems around externalized data for flexibility
- When combined, you can get tunable systems (DDD) that are cache-efficient (DOD)
