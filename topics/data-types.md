# Data Types

## Basic types

JS is a dynamically/weakly typed language. It has __8 basic data types__:
*string, number, bigint, boolean, symbol, undefined, null, object*.

In order to call props and methods of primitives there are so called “obj wrappers”:
`String`, `Number`, `Boolean`, `Symbol`, `BigInt`. They are created in the moment
of accessing the primitive's prop/method, execute, return a value, and are destroyed.

__DO NOT__ use obj wrappers as a constructor!	~~new Number(12)~~


### Number

Number represents integer and floating point numbers, specific num values
(`Infinity`, `-Infinity`, `NaN`).

Math operations are always safe – we never get an error. At worst, it will be `NaN`.

Forms of numbers:

| Name						| Example
|-----------------|----------
| Regular         | 1234
| With separator  | 1_000_000
| Zeroes counted	| 2.4e8
| Hexadecimal			| 0xff
| Binary					| 0b1101011
| Octal						| 0o377


### Symbol

Is a primitive type for unique ID. Can be local created as `Symbol(descr)`, or
can be global – `Symbol.for(descr)`

`Symbol.for(descr)` gets the symbol from from the global register or creates it
if it doesn’t exist

`Symbol.keyFor(descr)` gets the name of the symbol by the symbol itself. It
doesn’t work for non-global symbols.

`Symbol.keyFor(x) === x.description`

`for .. in` and `Object.keys()` skip symbols

`Object.assign()` copies both string and symbolic props

## Derived types

### Map

Map object holds ordered key-value pairs and can use any type of value as a key.

Props: size

Methods: set, get, has, delete, clear, keys, values, entries, forEach

Map to object: `Object.fromEntries(map)`

Object to Map: `new Map(Object.entries(obj))`

### Set

Set is a collection without keys, where each value may occur only once.

Props: size.

Methods: add, delete, has, clear, keys, values, entries, forEach

### WeakMap, WeakSet

These can be used as an additional storage for objectys that already exist.
Objects store there while they are reachable from somewhere else.

`WeakMap` methods: set, get, has, delete

`WeakSet` methods: add, has, delete

- They __CAN NOT__ store primitives
- They are __NOT__ iterable
- They __DON'T__ have `size` or `keys`

Their main advantages are that they have weak reference to objects, so they can
easily be removed by garbage collector.

`WeakMap` and `WeakSet` are used as “secondary” data structures in addition to
the “primary” object storage. Once the object is removed from the primary storage,
if it is only found as the key of WeakMap or in a WeakSet, it will be cleaned up
automatically.
