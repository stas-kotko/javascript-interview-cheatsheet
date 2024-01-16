# Web Workers

## Brief

> Web Worker is a JavaScript script executed from an HTML page that runs in the background, independently of scripts that may also have been executed from the same HTML page.

Web Workers allow you to do things like fire up long-running scripts to handle computationally intensive tasks, but without blocking the UI or other scripts to handle user interactions.

Workers utilize thread-like message passing to achieve parallelism. They're perfect for keeping  UI refresh, performant, and responsive for users.

Messages passed between the main page and workers are copied, not shared.

Most browsers implement the structured cloning algorithm, which allows you to pass more complex types in/out of Workers such as File, Blob, ArrayBuffer, and JSON objects.
 
Web Workers run in an isolated thread. As a result, the code that they execute needs to be contained in a __separate file.__

Types:
- Dedicated Workers
- Shared Workers
- Service Workers

### Example


```javascript
// main script

const worker = new Worker('doWork.js');

worker.addEventListener('message', event => {
  console.log('Worker said: ', event.data);
}, false);

worker.postMessage('Hello World'); // Send data to our worker.
```

```javascript
// doWork.js

self.addEventListener('message', event => {
  self.postMessage(event.data);
}, false);
```


### Loading external scripts

You can load external script files or libraries into a worker with the importScripts() function.

```javascript
importScripts('script1.js');
importScripts('script2.js');
// or
importScripts('script1.js', 'script2.js');
```

## Extended

### Worker types

- __Dedicated workers__ are workers that are utilized by a single script. This context is represented by a DedicatedWorkerGlobalScope object.
- __Shared workers__ are workers that can be utilized by multiple scripts running in different windows, IFrames, etc., as long as they are in the same domain as the worker. They are a little more complex than dedicated workers — scripts must communicate via an active port.
- __Service Workers__ essentially act as proxy servers that sit between web applications, the browser, and the network (when available). They are intended, among other things, to enable the creation of effective offline experiences, intercept network requests and take appropriate action based on whether the network is available, and update assets residing on the server. They will also allow access to push notifications and background sync APIs.

### Worker scope

Workers run in a different global context than the current window! While Window is not directly available to workers

In the context of a worker, both `self` and `this` reference the global scope for the worker. Thus, you can use workers methods (like `postMessage`) just like that, as it was a function, because in context of workers it's a method of the global object.

### Features available to workers

Due to their multithreaded behavior, Web Workers only has access to a subset of JavaScript's features:

- The navigator object
- The location object (read-only)
- XMLHttpRequest
- setTimeout()/clearTimeout() and setInterval()/clearInterval()
- The Application Cache
- Importing external scripts using the importScripts() method
- Spawning other web workers

Workers do __NOT__ have access to:

- The DOM (it's not thread-safe)
- The window object
- The document object
- The parent object

### Subworkers
Workers have the ability to spawn child workers. This is great for further breaking up large tasks at runtime. However, subworkers come with a few caveats:

Subworkers must be hosted within the same origin as the parent page.
URIs within subworkers are resolved relative to their parent worker's location (as opposed to the main page).
Keep in mind most browsers spawn separate processes for each worker. Before you go spawning a worker farm, be cautious about hogging too many of the user's system resources. One reason for this is that messages passed between main pages and workers are copied, not shared. See Communicating with a Worker via Message Passing.

### Use cases
So what kind app would utilize web workers? Here are a few more ideas to get your brain churning:

- Prefetching and/or caching data for later use.
- Code syntax highlighting or other real-time text formatting.
- Spell checker.
- Analyzing video or audio data.
- Background I/O or polling of webservices.
- Processing large arrays or humungous JSON responses.
- Image filtering in canvas.
- Updating many rows of a local web database.

---

#### Sources:

- [The Basics of Web Workers](https://web.dev/articles/workers-basics)
- [Web Workers API | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)
