# Misc

## Garbage collection

Garbage collection is a memory management mechanism in JS. Each runtime implements its own GC. 

The main concept is reachability. “Reachable” values are those that are accessible or usable somehow. They are guaranteed to be stored in memory.

A base set of inherently reachable values:
- The currently executing function, its local variables and parameters.
- Other functions on the current chain of nested calls, their local variables and parameters.
- Global variables.
- Any other value is considered reachable if it’s reachable from a root by a reference or by a chain of references.

The basic garbage collection algorithm is called “mark-and-sweep”.

The following “garbage collection” steps are regularly performed:
- The garbage collector takes roots and “marks” (remembers) them.
- Then it visits and “marks” all references from them recursively until every reachable (from the roots) references are visited.
- All objects except marked ones are removed.


## Memory management

Primitive values are stored in the call stack directly, at the place where they were created.
Reference types are stored in a memory heap.


## Hydration

In web development, __hydration__ or __rehydration__ is a technique in which client-side JavaScript converts a static HTML web page, delivered either through static hosting or server-side rendering, into a dynamic web page by _attaching event handlers_ to the HTML elements. Because the HTML is pre-rendered on a server, this allows for a fast "first contentful paint" (when useful data is first displayed to the user), but there is a period of time afterward where the page appears to be fully loaded and interactive, but is not until the client-side JavaScript is executed and event handlers have been attached.

Frameworks that use hydration include Next.js and Nuxt.js.

React v16.0 introduced a "hydrate" function, which hydrates an element, in its API.
