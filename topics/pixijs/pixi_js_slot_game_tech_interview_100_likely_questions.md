# PixiJS Slot Game Tech Interview – 100 Likely Questions

Each question includes a **short directional answer** — not exhaustive, just enough to know *where to dig deeper*.

---

## A. PixiJS Core & Rendering (1–20)

1. **What is a draw call in PixiJS?**  
A GPU call per batch; too many kill FPS.

2. **Why does deep container nesting hurt performance?**  
It breaks batching and increases transform calculations.

3. **Container vs Sprite — cost difference?**  
Sprite is cheaper; Container adds transform overhead.

4. **Why use texture atlases?**  
They reduce texture switches → fewer draw calls.

5. **When does `cacheAsBitmap` help?**  
Static complex visuals reused across frames.

6. **When does `cacheAsBitmap` hurt?**  
Dynamic content or frequently changing scale/alpha.

7. **Graphics vs Sprite performance?**  
Graphics are expensive; sprites are GPU-friendly.

8. **Why are masks expensive?**  
They often trigger extra render passes.

9. **Difference between `alpha` and `visible = false`?**  
Invisible objects skip rendering entirely.

10. **How does Pixi batching work?**  
Same base texture + state = one batch.

11. **What breaks batching?**  
Different textures, blend modes, filters.

12. **Why avoid per-frame object creation?**  
GC spikes cause frame drops.

13. **Ticker vs requestAnimationFrame?**  
Ticker adds priority and shared timing.

14. **Why limit filters usage?**  
They force offscreen rendering.

15. **How to detect overdraw?**  
Visualize layers / analyze draw calls.

16. **Sprite vs AnimatedSprite trade-off?**  
AnimatedSprite is heavier but convenient.

17. **Why reuse textures globally?**  
GPU memory + batching efficiency.

18. **What is texture bleeding?**  
Sampling outside sprite bounds due to atlas padding.

19. **How does resolution affect performance?**  
Higher resolution = more pixels to fill.

20. **What causes memory leaks in Pixi?**  
Not destroying textures, listeners, or references.

---

## B. Performance & Optimization (21–40)

21. **How do you profile a Pixi game?**  
FPS, memory, draw calls, Chrome devtools.

22. **Acceptable draw calls for slots?**  
Usually under ~100 per frame.

23. **Why slots need aggressive optimization?**  
Run on low-end mobile devices.

24. **How to reduce draw calls quickly?**  
Flatten containers, atlas textures.

25. **Why pre-allocate arrays/objects?**  
Avoid GC during gameplay.

26. **What is a GC spike?**  
Garbage collection pause causing frame hitch.

27. **Why avoid closures in hot paths?**  
They allocate memory each frame.

28. **How to optimize animations?**  
Reuse tweens, avoid per-frame logic.

29. **What’s wrong with `setTimeout` in games?**  
Unreliable timing when tab is throttled.

30. **How to handle tab visibility change?**  
Pause ticker, resync state on resume.

31. **Why avoid floating-point drift?**  
Desync between logic and visuals.

32. **How to detect memory leaks?**  
Heap snapshots over time.

33. **Why is object pooling important?**  
Stable memory usage.

34. **What is over-rendering?**  
Rendering objects not visible to player.

35. **How to stop offscreen updates?**  
Visibility checks or lifecycle control.

36. **Why limit event listeners?**  
Leaks + unexpected logic calls.

37. **CPU-bound vs GPU-bound — difference?**  
Logic vs rendering bottleneck.

38. **Why measure on real devices?**  
Emulators lie.

39. **Why mobile Safari is problematic?**  
Memory limits, aggressive throttling.

40. **What’s the first thing you optimize?**  
Draw calls and allocations.

---

## C. Slot Game Architecture (41–60)

41. **What is the base game loop?**  
Idle → spin → resolve → bonus → return.

42. **Why model slots as a state machine?**  
Predictable transitions, fewer bugs.

43. **What is a bonus mode?**  
Separate gameplay state with isolated logic.

44. **Free spins vs base game difference?**  
Different rules, payouts, persistence.

45. **What is persistent state?**  
State saved across sessions.

46. **What must be persisted?**  
Credits, bonus progress, counters.

47. **Why isolate math from visuals?**  
Testability and determinism.

48. **What is deterministic simulation?**  
Same input → same result.

49. **Why replay systems matter?**  
Debugging and compliance.

50. **What breaks determinism?**  
Random calls in animations.

51. **How to sync animation with logic?**  
Events, not timers.

52. **Why avoid logic in tweens?**  
Hard to control and test.

53. **What is a game controller layer?**  
Orchestrates state and systems.

54. **Why avoid monolithic game classes?**  
Impossible to scale.

55. **What is feature encapsulation?**  
Bonus logic isolated from base game.

56. **Why event-driven architecture fits slots?**  
Asynchronous sequences.

57. **Why not ECS everywhere?**  
Overkill for simple slots.

58. **What is rollback safety?**  
Ability to restore previous state.

59. **Why version game state?**  
Backward compatibility.

60. **What causes bonus desync bugs?**  
Race between animation and state.

---

## D. TypeScript & Code Quality (61–80)

61. **Why use discriminated unions for states?**  
Compile-time exhaustiveness checks.

62. **Why avoid numeric enums?**  
Runtime reverse mapping issues.

63. **String union vs enum?**  
Lighter and safer.

64. **How to type server math responses?**  
Exact interfaces, no `any`.

65. **Why strict null checks matter?**  
Prevent runtime crashes.

66. **How to model game events in TS?**  
Typed event maps.

67. **Why avoid inheritance-heavy designs?**  
Rigid and fragile.

68. **Composition vs inheritance?**  
Composable systems scale better.

69. **How to enforce state transitions?**  
Types + explicit state machine.

70. **Why prefer readonly data?**  
Prevent accidental mutation.

71. **How to avoid circular dependencies?**  
Layered architecture.

72. **What is structural typing?**  
Compatibility by shape.

73. **Why avoid massive interfaces?**  
Hard to evolve.

74. **How to type animation configs?**  
Narrow literal types.

75. **Why use const assertions?**  
Preserve literal types.

76. **How to model feature flags?**  
Union-based config objects.

77. **Why avoid `any` in core logic?**  
Silent bugs.

78. **How to enforce immutability?**  
Readonly + cloning.

79. **What’s a safe pub/sub pattern?**  
Explicit subscribe/unsubscribe.

80. **How to prevent listener leaks?**  
Lifecycle-managed disposal.

---

## E. Debugging, Failure & Production (81–100)

81. **Game freezes after tab switch — why?**  
Timers paused, state desynced.

82. **Assets fail to load — fallback?**  
Graceful error screen.

83. **Why preload critical assets?**  
Avoid runtime stalls.

84. **How to log production errors?**  
Centralized logging, no console spam.

85. **What is soft-lock?**  
Game stuck without crash.

86. **How to detect soft-locks?**  
State watchdogs.

87. **Why retries are dangerous?**  
Duplicate rewards.

88. **How to handle network latency?**  
Disable input, show pending state.

89. **Why idempotent actions matter?**  
Safe replays.

90. **How to handle partial bonus completion?**  
Persist intermediate state.

91. **Why test long sessions?**  
Memory leaks appear late.

92. **What breaks on low-memory devices?**  
Textures, filters, audio.

93. **How to recover from corrupted state?**  
Reset with compensation.

94. **Why avoid silent catches?**  
Hidden failures.

95. **How to simulate edge cases?**  
Forced state injection.

96. **What is hotfix safety?**  
Minimal change risk.

97. **Why version assets?**  
Cache invalidation.

98. **How to detect infinite loops?**  
Frame budget guards.

99. **What’s the worst production bug?**  
Incorrect payout.

100. **What defines seniority here?**  
Preventing bugs before they ship.

---

If you can confidently *explain the direction* for most of these, you’re well above average for this role.

