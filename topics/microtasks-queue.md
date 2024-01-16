# Microtasks queue

The ECMA standard specifies an internal queue `PromiseJobs`, more often referred to as the “microtask queue” (V8 term).

Microtask queue is an engine's internal mechanism for managing asynch operations.

According tothe ECMA spec, MQ:
- is FIFO
- execution of a task is initiated only when nothing else is running

Promise handling is always asynchronous, as all promise actions pass through the internal “promise jobs” queue, also called “microtask queue” (V8 term).

So `.then/catch/finally` handlers are always called after the current code is finished.
