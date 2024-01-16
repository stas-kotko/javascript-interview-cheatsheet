# [F.prototype](https://javascript.info/function-prototype)

If F.prototype is an object, then the new operator uses it to set [[Prototype]] for the new object.

F.prototype is a regular prop, not the prototype of the F function. It stores a value that will be used as a prototype for new created object when we will use `new F()` notation.

> __`F.prototype` only used at `new F()` time__
>
> F.prototype property is only used when new F is called, it assigns [[Prototype]] of the new object.

The default "prototype" is an object with the only property `constructor` that points back to the function itself.

Ways to set object prototype explicitly:
- `Object.setPrototypeOf(obj, prototype)`
- with literal: `{ __proto__: ... }`
- `Object.create(prototype, [descriptors])`
