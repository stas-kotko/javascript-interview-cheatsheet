# Promises

The `Promise` object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

A Promise is in one of these states:

- _pending_: initial state, neither fulfilled nor rejected, `{ state: 'pending', result: undefined }`
- _fulfilled_: `{ state: 'fulfilled, result: <value> }`
- _rejected_: `{ state: 'rejected, result: <error> }`

The properties `state` and `result` of the Promise object are internal. We can’t directly access them. We can use the methods `.then/.catch/.finally` for that.

The function passed to `new Promise` is called the __executor__. When new Promise is created, the executor runs automatically _immediately_.

Its arguments `resolve` and `reject` are callbacks provided by JavaScript itself.

Handlers (consumers):
- `.then(result, error)`
- `.catch(error)`
- `.finally()`


The code of a promise executor and its handlers has an "invisible" `try..catch` around it. If an exception happens, it gets caught and treated as a rejection. An error will be turned into a rejected promise.

If we throw an exception inside `.catch` , then the control goes to the next closest error handler. If we handle the error and finish normally, it continues to the next closest `.then`.

“Thenable” object – an arbitrary object that has a method `.then`. It will be treated the same way as a promise. The idea is that 3rd-party libraries may implement “promise-compatible” objects of their own. They can have an extended set of methods, but also be compatible with native promises, because they implement `.then` method.

```javascript
new Promise(resolve => resolve())
  .then((res) => {
    return new Thenable(res);
  })
  .then();
```



## promise API

There are __6 static methods__ of `Promise` class:

1. `Promise.all(promises)` – waits for all promises to __resolve__ and returns an array of their results. If any of the given promises rejects, it becomes the error of `Promise.all`, and all other results are ignored.
1. `Promise.allSettled(promises)` – waits for all promises to __settle__ and returns their results as an array of objects with:
    - `status`: `"fulfilled"` or `"rejected"`
    - `value` (if fulfilled) or `reason` (if rejected).
1. `Promise.race(promises)` – waits for the first promise to __settle__, and its result/error becomes the outcome.
1. `Promise.any(promises)` – waits for the first promise to __fulfill__, and its result becomes the outcome. If all of the given promises are rejected, `AggregateError` becomes the error of `Promise.any`.
1. `Promise.resolve(value)` – makes a resolved promise with the given value.
1. `Promise.reject(error)` – makes a rejected promise with the given error.


|           | Fulfilled | Settled         |
|-----------|-----------|-----------------|
| __All__   | `.all()`  | `.allSettled()` | 
| __First__ | `.any()`  | `.race()`       |


## Promisification

“Promisification” is a conversion of a function that accepts a callback into a function that returns a promise.

```javascript
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(null, script);
  script.onerror = () => callback(new Error(`Script load error for ${src}`));

  document.head.append(script);
}
// usage:
// loadScript('path/script.js', (err, script) => {...})

let loadScriptPromise = function(src) {
  return new Promise((resolve, reject) => {
    loadScript(src, (err, script) => {
      if (err) reject(err);
      else resolve(script);
    });
  });
};
// usage:
// loadScriptPromise('path/script.js').then(...)
```
