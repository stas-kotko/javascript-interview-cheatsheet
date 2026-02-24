# Data-Driven Development (DDD)

## ECS and Data-Driven Development (DDD)

ECS is almost inherently data-driven.

Data-driven development means:
	•	Behavior is determined by data, not hardcoded class hierarchies.
	•	Game objects are configured via data (JSON, configs, prefabs).

The systems decide behavior based on the presence of components.

That’s textbook data-driven design.

### Why this matters:
	•	Designers can configure entities without changing code.
	•	You can serialize full game state easily.
	•	Easier balancing and tuning.

### ECS vs “Just Config Files”

Important distinction:
	•	Data-driven OOP = classes still own behavior.
	•	ECS = behavior fully externalized into systems.

ECS pushes DDD much further by structurally separating state and logic.
