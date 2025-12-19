# Understanding the Event Loop in Node.js

<!-- omit from toc -->

## Table of Contents

- [Core Concepts](#core-concepts)
- [Event Loop Mechanics](#event-loop-mechanics)
- [Code Examples](#code-examples)
- [Common Patterns](#common-patterns)
- [Problem Solutions](#problem-solutions)
- [Key Points](#key-points)

## Core Concepts

- **Event Loop**: The mechanism that allows Node.js to perform non-blocking I/O operations
- **Single-threaded nature**: JavaScript runs on a single thread but uses the event loop for asynchronous operations
- **Non-blocking I/O**: Operations that don't halt the main thread while waiting for completion
  ![Event Loop Phases](assets/event-loop-phases.png)

## Event Loop Mechanics

- **Call Stack**: Where synchronous code executes
- **Callback Queue**: Where callback functions wait to be executed
- **Microtask Queue**: Higher priority queue for promises and process.nextTick
- **Event loop phases**: Timer, I/O callbacks, idle/prepare, poll, check, close callbacks

## Code Examples

```javascript
// Demonstrating event loop order
console.log('Start');

setTimeout(() => {
    console.log('Timer callback');
}, 0);

Promise.resolve().then(() => {
    console.log('Promise callback');
});

console.log('End');

// Output:
// Start
// End
// Promise callback
// Timer callback
```

## Common Patterns

- **Before (Blocking)**: Using synchronous operations that halt execution
- **After (Non-blocking)**: Using asynchronous operations with callbacks or promises
- **Best Practices**: Understanding when operations are blocking vs non-blocking

## Problem Solutions

- **Blocking Operations**: Replace with async alternatives (fs.readFile vs fs.readFileSync)
- **Understanding Timing**: Microtasks execute before macrotasks
- **Performance**: Avoid blocking the event loop with heavy computations

## Key Points

- **Main takeaway**: Event loop enables Node.js to be fast and scalable despite being single-threaded
- **When to use**: All I/O operations should be asynchronous in Node.js applications
- **Common pitfalls**: Blocking the event loop with synchronous operations or heavy CPU tasks
- **Performance impact**: Proper async patterns keep applications responsive

## Links/References

- Video: event-loop-fundamentals (15:30)
- Previous: [JavaScript Fundamentals]
- Next: [Callback Patterns]
- Related: [Process and Threads]

---

**Created**: August 26, 2025  
**Last Modified**: August 26, 2025
