# Node.js-theory
Node.js Architecture (High-Level Overview)

Node.js is built to run JavaScript outside the browser using a non-blocking, event-driven architecture. Its main goal is to handle many operations efficiently with a single main thread. It achieves this using the V8 engine, core APIs, native bindings, the event loop, and libuv.

JavaScript Engine (V8)

V8 is the JavaScript engine developed by Google and used by Node.js.

It converts JavaScript code into machine code so the system can execute it quickly.

V8 handles memory management, garbage collection, and execution of synchronous JavaScript.

Node.js relies on V8 to run JavaScript efficiently, but V8 alone cannot handle file systems, networking, or timers.

Node.js Core APIs

Node.js core APIs provide features that browsers do not offer.

Examples include file system access, networking, timers, streams, and process management.

These APIs look like JavaScript functions but internally rely on native C and C++ code.

They allow JavaScript to interact with the operating system.

Native Bindings

Native bindings act as a bridge between JavaScript and low-level system code.

They connect JavaScript APIs to C and C++ implementations.

When you call APIs like fs.readFile, native bindings forward the request to system-level code.

This is how JavaScript communicates with the OS efficiently.

Event Loop

The event loop is the heart of Node.js.

It allows Node.js to perform non-blocking operations using a single main thread.

Instead of waiting for tasks to finish, Node.js registers callbacks and continues execution.

The event loop continuously checks queues and executes callbacks when tasks are ready.

libuv
What is libuv?

libuv is a C library used by Node.js to handle asynchronous operations.

It provides the event loop implementation.

It manages threads, timers, file system operations, and networking.

Why Node.js needs libuv

JavaScript itself cannot handle low-level OS operations.

libuv makes Node.js cross-platform and handles async behavior consistently across systems.

Responsibilities of libuv

Managing the event loop

Handling asynchronous I/O

Managing the thread pool

Scheduling timers and callbacks

Thread Pool
What is a thread pool?

A thread pool is a group of background threads used to execute blocking operations.

Node.js uses a default pool of four threads.

These threads run tasks in parallel without blocking the main thread.

Why Node.js uses a thread pool

Some operations cannot be truly non-blocking at the OS level.

Using background threads prevents the main event loop from freezing.

Operations handled by the thread pool

File system operations

Cryptography tasks

DNS lookup

Compression and decompression

Worker Threads
What are worker threads?

Worker threads allow JavaScript code to run in parallel.

Each worker thread has its own event loop and memory.

They are used for CPU-intensive JavaScript tasks.

Why worker threads are needed

Heavy computations can block the main thread.

Worker threads allow parallel execution of JavaScript logic.

Difference between thread pool and worker threads

Thread pool handles background system tasks automatically.

Worker threads are manually created for CPU-heavy JavaScript work.

Thread pool is managed by libuv, worker threads are managed by developers.

Event Loop Queues
Macro Task Queue

Contains tasks scheduled by APIs like timers and I/O callbacks.

Examples include setTimeout, setInterval, file system callbacks, and network requests.

Micro Task Queue

Contains tasks that must execute immediately after the current operation.

Examples include Promise.then, Promise.catch, and queueMicrotask.

Execution Priority

Micro task queue always executes before the macro task queue.

After every phase of the event loop, micro tasks are cleared completely.
