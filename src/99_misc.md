## Misc

### Garbage collection

Garbage collection is a memory management mechanism in JS. Each runtime implements its own GC.
The main concept is reachability. “Reachable” values are those that are accessible or usable somehow. They are guaranteed to be stored in memory.

A base set of inherently reachable values:
The currently executing function, its local variables and parameters.
Other functions on the current chain of nested calls, their local variables and parameters.
Global variables.
Any other value is considered reachable if it’s reachable from a root by a reference or by a chain of references.
The basic garbage collection algorithm is called “mark-and-sweep”.
The following “garbage collection” steps are regularly performed:
The garbage collector takes roots and “marks” (remembers) them.
Then it visits and “marks” all references from them recursively until every reachable (from the roots) references are visited.
All objects except marked ones are removed.

## Memory management

Primitive values are stored in the call stack directly, at the place where they were created.
Reference types are stored in a memory heap.
