# Prototypal inheritance

In JavaScript, objects have a special hidden property `[[Prototype]]` (as named in the specification), that is either `null` or references another object. That object is called “a prototype”

When we read a property from object, and it’s missing, JavaScript automatically takes it from the prototype. In programming, this is called “prototypal inheritance”

`__proto__` is a getter/setter for `[[Prototype]]`

The `__proto__` property is outdated and exists only for historical reasons. Modern JavaScript suggests that we should use `Object.getPrototypeOf/.setPrototypeOf` functions instead that get/set the prototype.

```js
Object.getPrototypeOf(obj)
Object.setPrototypeOf(obj, prototype)
```

No matter where the method is found: in an object or its prototype. In a method call, `this` is always the object before the dot.

The `for..in` loop iterates over inherited properties too.

--- 

### Resources

- [Object.getPrototypeOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf)
- [Object.setPrototypeOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf)
