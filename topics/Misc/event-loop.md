# Event loop

Browser JavaScript execution flow, as well as in Node.js, is based on an event loop.

Event loop is a process (mechanism) that coordinates asynchronous operation
in a single threaded runtime.

It has one very simple job: it looks at the stack and it looks at the queue.
If the stack is empty, it takes the firts task in the queue and push it onto the
stack. Now the stack has what to do and event loop wait until the stack is empty
again to start from the beginning.

The event loop is what allows *Node.js* to perform non-blocking I/O operations —
despite the fact that JavaScript is single-threaded — by offloading operations
to the system kernel whenever possible. - [The Node.js Event Loop](https://nodejs.org/en/guides/event-loop-timers-and-nexttick/)

## General algorithm

1. Dequeue and run the oldest task from the macrotask queue (e.g. “script”).
1. Execute all microtasks:
    - While the microtask queue is not empty:
      - Dequeue and run the oldest microtask.
1. (in browser) Render changes if any.
1. If the macrotask queue is empty, wait till a macrotask appears.
1. Go to step 1.


| Macrotask examples         | Microtask examples |
|----------------------------|--------------------|
| scripts                    | Promises           |
| `setTimeout`               | `await`            |
| `mousemove`, `click` event | `queueMicrotask()` |


Immediately after every *macrotask*, the engine executes all tasks
from *microtask* queue, prior to running any
other macrotasks or rendering or anything else.

Event loop takes tasks from the queue and put them to the call stack.
Each task in the queue executes every time the new iteration
(tick) of the queue begins.

If we’d like to execute a function asynchronously (after the current code),
but *before* changes are rendered or new events handled,
we can schedule it with `queueMicrotask()`

For long heavy calculations that shouldn’t block the event loop,
we can use [Web Workers](../webworkers.md).
That’s a way to run code in another, parallel thread.

### Microtasks queue

The ECMA standard specifies an internal queue `PromiseJobs`,
more often referred to as the “microtask queue” (V8 term).

Microtask queue is an engine's internal mechanism for managing asynch operations.

*Microtasks* come solely from our code!

According to the ECMA spec, MQ:
- is FIFO
- execution of a task is initiated only when nothing else is running

Promise handling is always asynchronous, as all promise actions pass
through the internal “promise jobs” queue, also called “microtask queue” (V8 term).

So `.then/.catch/.finally` handlers are always called after the current code is finished.


---

### Resources

- https://nodejs.org/en/guides/event-loop-timers-and-nexttick/
