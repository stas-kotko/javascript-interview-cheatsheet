# Scripts: async, defer

When the browser loads HTML and comes across a `<script>...</script>` tag, it can’t continue building the DOM. It must execute the script right now. The same happens for external scripts` <script src="..."></script>`: the browser must wait for the script to download, execute the downloaded script, and only then can it process the rest of the page.

That leads to two important issues:

1. Scripts can’t see DOM elements below them, so they can’t interact with them.
1. Bulky script at the top of the page “blocks the page”. 

## `defer`

The `defer` attribute tells the browser not to wait for the script. Instead, the browser will continue to process the HTML, build DOM. The script loads “in the background”, and then runs when the DOM is fully built.

- `defer` never block the page.
- `defer` always execute when the DOM is ready (but before `DOMContentLoaded`[^1] event).
- Always keep their relative order (just like regular scripts).
- Browsers download deferred scripts in parallel

> Note!
>
> The `defer` attribute is only for external scripts. The `defer` attribute is ignored if the `<script>` tag has no `src`.

> Note!
>
> `DOMContentLoaded` event only triggers when the script is _downloaded_ and _executed._

## `async`

The `async` attribute means that a script is completely independent

- non-blocking (like `defer`)
- doesn't care about order
- runs right away when ready

In other words, async scripts load in the background and run when ready. The DOM and other scripts don’t wait for them, and they don’t wait for anything. A fully independent script that runs when loaded.

> Note!
>
> The `async` attribute is only for external scripts
> Just like `defer`, the `async` attribute is ignored if the `<script>` tag has no `src`


## Dynamic scripts

We can create a script and append it to the document dynamically using JavaScript:

```js
let script = document.createElement('script');
script.src = "/article/script-async-defer/long.js";
document.body.append(script); // (*)
```

The script starts loading as soon as it’s appended to the document (*).

__Dynamic scripts behave as “async” by default.__

This can be changed if we explicitly set `script.async=false`. Then scripts will be executed in the document order, just like `defer`.

## Summary

![legend](https://www.growingwiththeweb.com/images/2014/02/26/legend.svg)

__`<script>`__

![script](https://www.growingwiththeweb.com/images/2014/02/26/script.svg)

__`<script async>`__

![script async](https://www.growingwiththeweb.com/images/2014/02/26/script-async.svg)

__`<script defer>`__

![script defer](https://www.growingwiththeweb.com/images/2014/02/26/script-defer.svg)


|                                            | `async`     | `defer` |
|--------------------------------------------|-------------|---------|
| Non-blocking                               | ✅         | ✅      |
| Cares about order                          | ❌         | ✅      |
| Ignored if the `<script>` tag has no `src` | ✅         | ✅      |
| Script runs                                | When loaded | When the DOM is fully built (but before `DOMContentLoaded` event) |


In practice, `defer` is used for scripts that need the whole DOM and/or their relative execution order is important.

And `async` is used for independent scripts, like counters or ads. And their relative execution order does not matter.

---

### Resources

- https://javascript.info/script-async-defer
- https://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html
- https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event

[^1]: https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event
