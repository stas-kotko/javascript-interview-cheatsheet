# Generator functions

Regular functions return only one, single value (or nothing).

Generators can return (“yield”) multiple values, one after another, on-demand. They work great with iterables, allowing to create data streams with ease.

```js
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}
```

When such function is called, it doesn’t run its code. Instead it returns a special object, called “generator object”, to manage the execution.

```js
let generator = generateSequence(); // generator -> [object Generator]
```

The function code execution hasn’t started yet:

The main method of a generator is `next()`. It runs the execution until the nearest `yield <value>` statement. Then the function execution pauses, and the yielded value is returned to the outer code.

The result of `next()` is always an __object with two properties:__

- `value`: the yielded value
- `done`: `true` if the function code has finished, otherwise `false`

```js
let one = generator.next(); // one -> { value: 1, done: false }
```

The next call of `next()` will resume the execution from where it stopped previously - next line after the first yield.

When execution reaches the `return` statement, it finishes the function (`{ value: 3, done: true }`).

Now the generator is done. We should see it from `done: true` as the final result.

New calls to `generator.next()` don’t make sense any more. If we do them, they return the same object: `{done: true}`.


### Generators are iterable

We can loop over their values using `for..of`:

```js
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}

let generator = generateSequence();

for(let value of generator) {
  console.log(value); // 1, then 2
}
```

__It doesn’t show 3!__

It’s because `for..of` iteration ignores the last value, when `done: true`. So, if we want all results to be shown by `for..of`, we must return them with `yield`

```js
function* generateSequence() {
  yield 1;
  yield 2;
  yield 3;
}
```

As generators are iterable, we can call all related functionality, e.g. the spread syntax `...`:

```javascript
let sequence = [...generateSequence()];
console.log(sequence); // 1, 2, 3
```

---

### Resources

- https://javascript.info/generators
- https://javascript.info/async-iterators-generators
