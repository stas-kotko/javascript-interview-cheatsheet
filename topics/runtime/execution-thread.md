# Execution thread

JS is a single threaded language

Single sequentional flow of control

Synchronous language with async capabilities

A thread has a *call stack* (execution context stack) and a *memory heap*.

The call stack:
- stack of functions to be executed
- manages execution context
- LIFO
- Global execution context is always at the bottom


Memory heap is a place to store and write information — data for our app 
(variables, objects, etc..)
