# Document events

## Bubbling

Almost all doc events (click, mouseover...) _bubbles_ up from the element on which the event happened (clicked elm === `event.target`) straight up to the `html` element. This event can be captured and handled on its way.

- `event.target` - element which produced the event.
- `event.currentTarget` - element on which _handler_ has fired.


To capture the event on its way _down_ we must turn on special flag: 
```js
addEventListener(... , { capture: true })
```

Listeners on the same element run in the set order.

- `event.stopPropagation()` prevents bubbling
- `event.stopImmediatePropagation()` does the same + prevents other handlers from firing on the same element


## Event delegation

Instead of assigning a handler to each element, we can put a single handler on their common ancestor: 

`event.target.closest('div')`


## HTML page lifecycle

- `DOMContentLoaded` - DOM is ready, resources are not
- `load` - resources (imgs, styles) are ready
- `beforeunload` - user is about to leaving the page
- `unload` - user is leaving the page

