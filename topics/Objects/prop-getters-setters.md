# 🔗[Property getters and setters](https://javascript.info/property-accessors)

There are two kinds of object properties:
- data props - regular ones
- accesor props - getters/setters

They are essentially functions that execute on getting and setting a value, but look like regular properties to an external code.

```js
let obj = {
  get propName() {
    // getter, the code executed on getting obj.propName
  },

  set propName(value) {
    // setter, the code executed on setting obj.propName = value
  }
};
```

### Accessor descriptors

Descriptors for accessor properties are different from those for data properties.

For accessor properties, there is no value or writable, but instead there are get and set functions.

That is, an accessor descriptor may have:

- `get` – a function without arguments, that works when a property is read,
- `set` – a function with one argument, that is called when the property is set,
- `enumerable` – same as for data properties,
- `configurable` – same as for data properties.

