---
tags:
  - worker
  - multithreading
---

JS is single threaded and cannot handle multiple long running things at the same time as the main thread will appear blocked.

### Explanation:

JavaScript is traditionally **single-threaded**, meaning it can only execute one task at a time on the **main thread**, which handles everything, including user interactions (e.g., clicking, scrolling), DOM updates (rendering the UI), and running JavaScript code.

When JavaScript performs heavy or long-running tasks (e.g., complex calculations or data processing), it **blocks** the main thread, causing the UI to freeze or become unresponsive. Even though **asynchronous operations** (e.g., `setTimeout`, `fetch`, Promises) don't immediately block the UI, the callbacks they trigger still run on the main thread, which can still cause delays in rendering or responding to user actions.

To solve this problem, **Web Workers** allow JavaScript to become **multi-threaded** by offloading tasks to a **background thread**. This way, you can execute computationally expensive operations without blocking the main thread, keeping the UI responsive.

### Why Asynchronous Operations Can Still Block the DOM:

Even with asynchronous operations (like fetching data from an API), the task may not block the UI initially, but when the callback is executed (after the async task completes), it still runs on the main thread. If that callback contains heavy logic, it will temporarily block the main thread again. Web Workers solve this by running such tasks on a completely different thread.

Workers in JavaScript are a way to run scripts in background threads, separate from the main execution thread of a web page.


Types of worker
[[Web worker]]
[[Service Worker]]