# Execution context

Phases:

- _memory creation phase:_ 
  - create global object
  - create `this`

- execution phase
  - execute code line by line
  - create a new execution context for each function call


When you run any JS code, a special environment is created to handle the transformation and execution of the code. This is called _Execution Context_. It contains the currently running code and everything that aids in its execution.

There are a global EC and a function's EC

EC goes through two phases every time it's created

__NB!__ EC is NOT the same as Lexical Environment

_Execution Context_ is an internal JS construct that tracks execution of a module/function. The JS engine maintains execution context stack or a __call stack__, which contains these contexts.

_Lexical environment_ is an internal JS engine construct that holds identifier-variable mapping (identifier refers to the name of var/func)

For every Execution Context:
1. a corresponding lexical environment is created
1. if any function is created in that Execution Context, a reference to that new created LE is stored in the internal property `[[Environment]]` of that new created function. So every function tracks the LE related to the EC it was created in.
