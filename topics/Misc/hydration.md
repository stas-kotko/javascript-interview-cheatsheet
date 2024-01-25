# Hydration

In web development, __hydration__ or __rehydration__ is a technique in which client-side JavaScript converts a static HTML web page, delivered either through static hosting or server-side rendering, into a dynamic web page by _attaching event handlers_ to the HTML elements. Because the HTML is pre-rendered on a server, this allows for a fast "first contentful paint" (when useful data is first displayed to the user), but there is a period of time afterward where the page appears to be fully loaded and interactive, but is not until the client-side JavaScript is executed and event handlers have been attached.

Frameworks that use hydration include Next.js and Nuxt.js.

React v16.0 introduced a "hydrate" function, which hydrates an element, in its API.
