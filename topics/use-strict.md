# `"use strict"`

`"use strict"` can be put at the beginning of a function. Doing that enables
strict mode in that function only.

Please make sure that `"use strict"` is at the top of your scripts, otherwise
strict mode may not be enabled.

Only comments may appear above `"use strict"`.

There’s no way to cancel `"use strict"`

“classes” and “modules” enable `"use strict"` automatically.

## Why Strict Mode?

Strict mode makes it easier to write "secure" JavaScript.

Strict mode changes previously accepted "bad syntax" into real errors.

As an example, in normal JavaScript, mistyping a variable name creates a new
global variable. In strict mode, this will throw an error, making it impossible
to accidentally create a global variable.

In normal JavaScript, a developer will not receive any error feedback assigning
values to non-writable properties.

In strict mode, any assignment to a non-writable property, a getter-only
property, a non-existing property, a non-existing variable, or a non-existing
object, will throw an error.

## Not Allowed in Strict Mode

Using a variable, without declaring it, is not allowed

Deleting a variable (or object) is not allowed.

Deleting a function is not allowed.

Duplicating a parameter name is not allowed:

```js
"use strict";
function x(p1, p1) {};   // This will cause an error
```

Writing to a read-only property is not allowed:

```js
"use strict";
const obj = {};
Object.defineProperty(obj, "x", {value:0, writable:false});

obj.x = 3.14;            // This will cause an error
```

Writing to a get-only property is not allowed:

```js
"use strict";
const obj = {get x() {return 0} };

obj.x = 3.14;            // This will cause an error
```

Deleting an undeletable property is not allowed:

```js
"use strict";
delete Object.prototype; // This will cause an error
```

The word eval cannot be used as a variable:

The word arguments cannot be used as a variable:

The `this` keyword refers to the object that called the function. If the object
is not specified, functions in strict mode will return undefined and functions
in normal mode will return the global object (window):


---

### Resources

- https://javascript.info/strict-mode
