# Garbage collection

Garbage collection is a __memory management mechanism__ in JS. Each runtime implements
its own GC.

The main concept is __reachability__. “Reachable” values are those that are accessible
or usable somehow. They are guaranteed to be stored in memory.

A base set of inherently reachable values:
- The currently executing function, its local variables and parameters.
- Other functions on the current chain of nested calls, their local variables  
  and parameters.
- Global variables.
- Any other value is considered reachable if it’s reachable from a root by a  
  reference or by a chain of references.

The basic garbage collection algorithm is called __"mark-and-sweep"__.

The following “garbage collection” steps are regularly performed:
- The garbage collector takes roots and “marks” (remembers) them.
- Then it visits and “marks” all references from them recursively until every reachable (from the roots) references are visited.
- All objects except marked ones are removed.
