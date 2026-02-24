# Execution thread

JS is a single threaded language

Single sequentional flow of control

Synchronous language with async capabilities

A thread has a *call stack* (execution context stack) and a *memory heap*.

## Heap vs Stack

Call Stack:
- Stores and manages execution contexts, function calls, and local primitive values.
- Stack of functions to be executed
- LIFO, size-limited.
- Global execution context is always at the bottom

Memory Heap:
- Large, unstructured, and dynamic memory region managed by the JS engine.
- Stores objects, arrays, functions, closures - anything that isn’t a small primitive.
- Allocation + cleanup handled by the engine’s garbage collector.

Memory heap is a place to store and write information — data for our app 
(variables, objects, etc..)

### Practical implications for real code

You should care about the heap when:
	•	You keep long-lived references (global stores, singletons, caches)
	•	You create many short-lived objects in hot loops
	•	You work with games, canvas, PixiJS, or real-time apps

Typical mistakes:
	•	Forgotten event listeners
	•	Closures holding large objects
	•	Unbounded caches
	•	Retained DOM references
