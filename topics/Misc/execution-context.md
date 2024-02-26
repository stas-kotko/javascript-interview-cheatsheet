# Execution context

When you run any JS code, a special environment is created to handle the transformation and execution of the code. This is called *Execution Context*. It contains the currently running code and everything that aids in its execution.

**Execution Context** is an internal JS construct that tracks execution of a module/function. The JS engine maintains execution context stack or a *call stack*, which contains these contexts.

Execution Context goes through *two phases* every time it's created:
- Memory creation phase
  - create global object
  - create `this`

- Execution phase
  - execute code line by line
  - create a new execution context for each function call

Execution Context can be global or local (functional)


**NB!** Execution Context is *NOT* the same as Lexical Environment

**Lexical environment** is an internal JS engine construct that holds identifier-variable mapping (identifier refers to the name of var/func)

For every Execution Context:
1. a corresponding lexical environment is created
1. if any function is created in that Execution Context, a reference to that new created LE is stored in the internal property `[[Environment]]` of that new created function. So every function tracks the LE related to the EC it was created in.
