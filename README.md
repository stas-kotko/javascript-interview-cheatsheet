# Javascript Interview Cheatsheet

### Table of contents

- [Data types](#id-1)
  - [Number](#number)
  - [Symbols](#symbol)
 
- [Objects](#objects)
	- [__this__ keyword](#this-keyword)

- [Functions](#functions)

- [Loops](#loops)
  - [Labels](#labels)
  - [Iteration methods difference](#iteration-methods-difference)

- [Misc](#misc)
	- [Garbage collection](#garbage-collection)
	- [Memory management](#memory-management)

## Data Types {#id-1}

JS is a dynamically/weakly typed language. It has __8 basic data types__: *string, number, bigint, boolean, symbol, undefined, null, object*.

In order to call props and methods of primitives there are so called “obj wrappers”: String, Number, Boolean, Symbol, BigInt. They are created in the moment of accessing the primitive's prop/method, execute, return a value, and are destroyed.

__DO NOT__ use obj wrappers as a constructor!	~~new Number(12)~~


### Number
Number represents integer and floating point numbers, specific num values (Infinity, -Infinity, NaN).

Math operations are always safe – we never get an error. At worst, it will be NaN.

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
Is a primitive type for unique ID. Can be local created as Symbol(descr), or can be global – Symbol.for(descr)

Symbol.for(descr) gets the symbol from from the global register or creates it if it doesn’t exist

Symbol.keyFor(descr) gets the name of the symbol by the symbol itself. It doesn’t work for non-global symbols. 
Symbol.keyFor(x) === x.description

for .. in and Object.keys() skip symbols
Object.assign() copies both string and symbolic props

## Objects
Objects can be created in two ways: with *literal* or with *constructor*.

`Object.assign(dest, …sources)` – copies all enumerable own props and returns a modified target.

### __this__ keyword

## Functions
Each running function, code block, and script have an internal associated object – __Lexical Environment__.
LE consists of two parts:
- __env record__ – an obj that stores all local vars as its props (plus some meta data, like value of this)
- a reference to the __outer Lexical Env__.

LE will be deleted when it’s unreachable (including via [[Environment]])

A variable is just a prop of a special internal object – environment record.

Function declarations are hoisted and when LE is created, function declaration immediately becomes a ready-to-use function.

When a function runs, at the beginning of the call, a new LE is created to store local vars and params of the call.

The outer LE is an object created for EC where the function was created.

__Closure__ is a function that remembers its outer vars and can access them.

> A function bundled together with its lexical environment forms a __closure__ – *MDN*

Arrow functions don’t have __this__ and arguments object. Hence, without this they can’t be used as a constructor and can’t be called with new operator.

__Arrow functions:__
- Don’t have `this`
- Don’t have `arguments`
- Can’t be called with `new` operator
- Don’t have `super`

## Loops
```
while (cond) { … }

do { … } while (cond)

for (start; cond; step) { … }
```

`for` loop can use “inline” var declaration: `for (let i = 0 …`
This var is only visible inside the loop

`for` loop algorithm: 
- start – once per loop
- check the condition
- perform the code in the body
- perform step

`break` keyword exits from the loop immediately passing the control to the next line after the loop.

`continue` stops the current iteration and starts a new one if the condition allows it.

### Labels
```
label: for (...) {
	break label
	// or
	continue label
```
Labels are used for nested loops.

### Iteration methods difference
`Object.getOwnPropertynames(obj)` – returns non-symbol keys.  
`O.getOwnPropertySymbols(o)` – returns symbol keys only.  
`O.keys/values()` – non-symbol keys/values with enumerable flag.  
`for .. in` – loops over non-sym keys with enumerable flag, plus prototype’s keys.  

All of the use internal method [[OwnPropertyKeys]] to get a list of props (“ownKeys” trap in Proxy)


## Misc

### Garbage collection

Garbage collection is a memory management mechanism in JS. Each runtime implements its own GC.
The main concept is reachability. “Reachable” values are those that are accessible or usable somehow. They are guaranteed to be stored in memory.

A base set of inherently reachable values:
The currently executing function, its local variables and parameters.
Other functions on the current chain of nested calls, their local variables and parameters.
Global variables.
Any other value is considered reachable if it’s reachable from a root by a reference or by a chain of references.
The basic garbage collection algorithm is called “mark-and-sweep”.
The following “garbage collection” steps are regularly performed:
The garbage collector takes roots and “marks” (remembers) them.
Then it visits and “marks” all references from them recursively until every reachable (from the roots) references are visited.
All objects except marked ones are removed.

## Memory management

Primitive values are stored in the call stack directly, at the place where they were created.
Reference types are stored in a memory heap.

