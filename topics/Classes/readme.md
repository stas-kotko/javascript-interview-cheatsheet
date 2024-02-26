# Classes

`class` syntax creates a function. Code from `constructor` goes to the func body. Methods go to the `F.prototype`.

__Not just a syntactic shugar:__
1. functions created with `class` labeled by `[[IsClassConstructor]]: true`  
   Hence, we can not use them without `new`
1. Class methods are not enumerable by default
1. All code inside the class constructor is _always_ in "use strict"


Class fields - props for an individual objects, not for the prototype. Fields declared with "=", not with the ":"

```js
class User {
  field = 42
  
  constructor(name) { /*...*/ }

  method() { /*...*/ }
}
```

### Extension

`class Child extends Parent` creates two `[[Prototype]]` references:
1. `Child` prototypally inherits from `Parent`
1. `Child.prototype` prototypally inherits from `Parent.prototype`

As a result, inheritance works for both regular and static methods.

Built-in classes have no static inheritance: despite the fact such objects as Date or Array inherits from Object, they don't have its statics (like `Array.keys` or `Date.getOwnProperty`)

---

`class Rabbit extends Animal` means that `Rabbit.prototype.[[Prototype]] === Animal.prototype`

`Child.prototype.__proto__ === Parent.prototype`

If we didn't specify the constructor on extension, then it will be generated automatically:

`constructor(...args) { super(...args) }`

> Constructor in inherited classes __must__ call `super()` and do it __before using `this`__.

In JavaScript, there’s a distinction between a constructor function of an inheriting class (so-called “derived constructor”) and other functions. A derived constructor has a special internal property `[[ConstructorKind]]:"derived"`. That’s a special internal label.

That label affects its behavior with `new`.

When a regular function is executed with `new`, it creates an empty object and assigns it to `this`.
But when a derived constructor runs, it doesn’t do this. It expects the parent constructor to do this job.
So a derived constructor must call `super` in order to execute its parent (base) constructor, otherwise the object for `this` won’t be created. And we’ll get an error.
