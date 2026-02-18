
# Functions

Each running function, code block, and script have an internal
associated object – **Lexical Environment**.

When a function runs, at the beginning of the call,
a new LE is created to store local vars and params of the call.

LE consists of two parts:

- **env record** – an obj that stores all local vars as its props  
  (plus some meta data, like value of `this`)
- a reference to the **outer Lexical Env**.

LE will be deleted when it’s unreachable (including via `[[Environment]]`)

A variable is just a prop of a special internal object – _environment record._

Function declarations are hoisted and when LE is created,
function declaration immediately becomes a ready-to-use function.

When a function is created, the Lexical Environment where it happened
is assigned to function's internal property `[[Environment]]`. This way the func
knows where it was created and have access to its LE constantly.
This can not be changed.

The outer Lexical Environment is an object created for Execution Context where
the function was created.

**Closure** is a function that remembers its outer Lexical Environment and can
access them.

> A function bundled together with the Lexical Environment
> where it was created forms a **closure** – _MDN_

## Arrow functions

- Don’t have `this`, taken from the outer scope
- Don’t have `arguments`, taken from the outer scope
- Hence, without `this` can’t be called with `new` operator and
- Don’t have `super`
