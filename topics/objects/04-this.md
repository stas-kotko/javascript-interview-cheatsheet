# `this` keyword

`this` is a keyword that references another value (usually an object) that represents __current execution context.__

The current execution context can be a _global object_ or when used inside a function it references an object calling that function  

`this` is evaluated during the runtime depending on the context

`this` is the object that is executing the current function - "object before the dot". It's a binding that the language creates for you when the function body is evaluated. The value of `this` always changes based on how a function is called. 

The value of `this` depends on in which context it appears: function, class, or global.


## Details

### Callback

When a function is passed as a __callback__, the value of `this` depends on how the callback is called, which is determined by the implementor of the API. Callbacks are _typically_ called with a `this` value of `undefined` (calling it directly without attaching it to any object), which means if the function is non–strict, the value of `this` is the _global object_.

### Arrow funcs

In __arrow functions__, `this` retains the value of the enclosing lexical context's `this`. In other words, when evaluating an arrow function's body, the language does not create a new `this` binding.

Arrow functions create a closure over the `this` value of its surrounding scope, which means arrow functions behave as if they are "auto-bound" — no matter how it's invoked, `this` is bound to what it was when the function was created. The same applies to arrow functions created inside other functions: their this remains that of the enclosing lexical context.

Furthermore, when invoking arrow functions using `call()`, `bind()`, or `apply()`, the `thisArg` parameter is ignored. You can still pass other arguments using these methods, though.

### Constructors

When a function is used as a constructor (with the new keyword), its this is bound to the new object being constructed, no matter which object the constructor function is accessed on. The value of this becomes the value of the new expression unless the constructor returns another non–primitive value


## `bind()`, `call()`, `apply()`

Calling `f.bind(someObject)` creates a new function with the same body and scope as `f`, but the value of `this` is permanently bound to the first argument of `bind`, regardless of how the function is being called.

```js
function f() {
  return this.a;
}

const g = f.bind({ a: "azerty" });
console.log(g()); // azerty

const h = g.bind({ a: "yoo" }); // bind only works once!
console.log(h()); // azerty

const o = { a: 37, f, g, h };
console.log(o.a, o.f(), o.g(), o.h()); // 37 37 azerty azerty
```

#### `.call()` vs `.apply()`

Built-in function method `func.call(context, …args)` that allows to call a function explicitly setting `this`.

Instead of `func.call(this, ...arguments)` we could use `func.apply(this, args)`.

The only syntax difference between `call` and `apply` is that `call` expects *a list of arguments*, while `apply` takes *an array-like object* with them.

> NB! Rremember the difference:
> - _**c**_ is for _**c**omma_, used in _**c**all_ 
> - _**a**_ is for _**a**rray_, used in _**a**pply_

---

### Resources

- [this | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
