
## Functions

Each running function, code block, and script have an internal associated object – __Lexical Environment__.
LE consists of two parts:
- __env record__ – an obj that stores all local vars as its props (plus some meta data, like value of this)
- a reference to the __outer Lexical Env__.

LE will be deleted when it’s unreachable (including via [[Environment]])

A variable is just a prop of a special internal object – environment record.

Function declarations are hoisted and when LE is created, function declaration immediately becomes a ready-to-use function.

When a function runs, at the beginning of the call, a new LE is created to store local vars and params of the call.

The outer LE is an object created for EC where the function was created.

__Closure__ is a function that remembers its outer vars and can access them.

> A function bundled together with its lexical environment forms a __closure__ – *MDN*

Arrow functions don’t have __this__ and arguments object. Hence, without this they can’t be used as a constructor and can’t be called with new operator.

__Arrow functions:__
- Don’t have `this`
- Don’t have `arguments`
- Can’t be called with `new` operator
- Don’t have `super`
