# Objects configuration

Object property besides a value have 3 special attributes ("flags"):
- enumerable - listed in loops
- writable - value can be changed ("read-only" flag)
- configurable - deletable, other attributes can be modified

By default, all set to `true`

Get descriptor: `let descriptor = Object.getOwnPropertyDescriptor(obj, prop)`

Set/update descriptor (existed prop will be updated): `Object.defineProperty(obj, propName, descriptor)`


If the flag was not supplied, it's assumed `false`.

To get all property descriptors at once, we can use the method [`Object.getOwnPropertyDescriptors`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptors)

Making a prop *non-configurable* is one-way road. We cannot change it back with `defineProperty()` or some other way. The only attribute change possible: writable true → false


Handy predefined methods:

- [`Object.preventExtension(obj)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)  
Forbids the addition of new properties to the object.

- [`Object.seal(obj)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)  
  - Forbids *adding/removing* properties.
  - Sets `configurable: false` for all existing properties.

- [`Object.freeze(obj)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)  
  - Forbids adding/removing/*changing* of properties.
  - Sets `configurable: false`, `writable: false` for all existing properties.
