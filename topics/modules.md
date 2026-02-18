# Modules

_What is a module?_

A module is just a file. One script is one module. As simple as that.

Modules can load each other and use special directives `export` and `import` to interchange functionality, call functions of one module from another one.

As modules support special keywords and features, we must tell the browser that a script should be treated as a module, by using the attribute `<script type="module">`.

### Core module features

- Always `“use strict”`
- Module-level scope (In the browser, if we talk about HTML pages, independent top-level scope also exists for each `<script type="module">`.)
- A module code is evaluated only the first time when imported. Exports are generated, and then they are shared between importers, so if something changes the exported object, other importers will see that.
- `import.meta`: contains the information about the current module. Its content depends on the environment. In the browser, it contains the URL of the script, or a current webpage URL if inside HTML
- In a module, `this` is undefined
- Browser-specific features
  - Module scripts are deferred, same effect as `defer` attribute:
    1. downloading external module scripts `<script type="module" src="...">` doesn’t block HTML processing, they load in parallel with other resources.
    1. module scripts wait until the HTML document is fully ready (even if they are tiny and load faster than HTML), and then run. Module scripts always “see” the fully loaded HTML-page, including HTML elements below them.
    1. relative order of scripts is maintained: scripts that go first in the document, execute first. 
  - `async` works on inline scripts. For non-module scripts, the async attribute only works on external scripts. Async scripts run immediately when ready, independently of other scripts or the HTML document. For module scripts, it works on inline scripts as well.
  - External scripts that have `type="module"` are different in two aspects:
    1. External scripts with the same src run only once
    1. External scripts that are fetched from another origin (e.g. another site) require CORS headers  
  
## Dynamic imports

__The `import()` expression__

The `import(module)` expression loads the module and __returns a promise__ that resolves into a module object that contains all its exports. It can be called from any place in the code.

```js
let module = await import(modulePath)

// or

import(modulePath)
  .then(obj => '<module object>' )
  .catch(err => '<loading error, e.g. if no such module>')
```

> Note:
> 
> Although `import()` looks like a function call, it’s a special syntax that just happens to use parentheses (similar to `require()` in NodeJS or `super()` in classes).
>
> So we can’t copy import to a variable or use call/apply with it. It’s not a function.
