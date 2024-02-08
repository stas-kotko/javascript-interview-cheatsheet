
# Objects
Objects can be created in two ways: with _literal_ or with _constructor_.

`Object.assign(dest, …sources)` – copies all enumerable own props and returns a modified target.

`structuredClone(obj)` clones the object with all nested props making a a true "deep copy" of the target. Can be used with any _structured-clonable type_.

What can __NOT__ be cloned with `structuredClone()`:
- functions - DataCloneError
- DOM nodes - DataCloneError
- Symbols
- prototype chain
- prop descriptors, getters, setters, and similar metadata-like features


### Constructors

When a constructor function is executed with `new` keyword it performs the following steps:
1. a new empty obj is created and assigned to `this`
1. `this.__proto__ = f.prototype`
1. the function body executes 
1. the value of `this` is returned

```javascript
function User(name) {
  // this = {}                       (1)
  // this.__proto__ = User.prototype (2)
  this.name = name //                (3)
  // return this                     (4)
}
```

### Object iteration

Objects are not iterable by default, so we can't use `for .. of` loop on it. To make it so, we can add `[Symbol.iterator]` field to it. It has to be a function that returns an object with `next()` method - an **iterator**. The `next()` method has to return an obj of type `{done: boolean, value: any}`.

**Iterable** is an object that implements the `[Symbol.iterator]` method.

**Array-like** is an object that have _indexes_ and _length_, so it looks like an array.


## Extended

Things that don't work with `structuredClone()`:  
`Error` and `Function` objects cannot be duplicated by the structured clone algorithm; attempting to do so will throw a DATA_CLONE_ERR exception. Attempting to clone DOM nodes will likewise throw a DATA_CLONE_ERR exception. Certain parameters of objects are not preserved: The lastIndex field of RegExp objects is not preserved. Property descriptors, setters, and getters (as well as similar metadata-like features) are not duplicated. For example, if an object is marked read-only using a property descriptor, it will be read-write in the duplicate, since that's the default condition. The prototype chain does not get walked and duplicated.


---
### Resources
- [Objects: the basics](https://javascript.info/object-basics)
