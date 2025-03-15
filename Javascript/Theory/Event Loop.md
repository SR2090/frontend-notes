![[Pasted image 20250124101645.png]]

  

![[Pasted image 20250124101709.png]]

  

![[Pasted image 20250124101716.png]]

  
  

JavaScript is a synchronous single threaded language it has one call stack, can only do one thing at a time. The call stack is present inside the js engine

all the JS code is executed in this call stack

![[Pasted image 20250130083010.png]]

  

A global execution context is created This execution context is pushed inside the call stack

  

This functions executes the code in the file line by line

![[Pasted image 20250130083217.png]]

  

![[Pasted image 20250130083306.png]]

The global execution context gets pushed into the call stack then it starts getting executed line by line after encountering a function let's say a in this case that function execution is pushed into the call stack

Since he is now in the call stack it will be popped and executed and we will see a in the console

  

Once we reach the end of the function then the a function is popped out of the call stack

  
  

![[Pasted image 20250130083451.png]]

  
  

After the execution of the a method the control moves to the next console log statement which gets executed and shown on the console![[Pasted image 20250130083524.png]]

  

After executing the last console log statement there is nothing to execute anymore hence the global execution context will be popped out of the stack

  
  
  

### How does js performs async operation

![[Pasted image 20250130084124.png]]

  
  

The call stack is present within the browser and the browser provides it with various functionality such as the timer the page that is being rendered local storage url Bluetooth and the location

  

![[Pasted image 20250130084211.png]]

  

The web apis are provided by the browser, can be accessed using the window object. We get access to it inside the call stack due to global object(window).

  

## SetTimeout

![[Pasted image 20250130085124.png]]

  

The GEC is pushed into the call stack where it gets executed line by line.

After printing out Start into the stack we move to the next line.

It encounters the web api set timeout. A timer method is executed in the backend, the method in the meanwhile is pushed on the **call back queue**.

Once the timer has elapsed the event loop pops the method call out of the queue and moves it to the call stack.

![[Pasted image 20250130091223.png]]

  

It pushes the execution context of cb inside the call stack and then executes the entire method. It does this when the timer expires.

![[Pasted image 20250130091437.png]]

  

## Case of add Eventlistener

![[Pasted image 20250130092441.png]]

  

When you attach an event listener to a DOM element, the browser registers a callback function for that event (like a click) on that specific element. When the user interacts with the element—for example, by clicking it—the callback function is added to the callback queue. The event loop continuously monitors the call stack and, once it’s empty, moves the callback from the queue to the call stack for immediate execution. If the user clicks the element multiple times, each click results in the callback being queued up, ensuring that all interactions are eventually processed in order.

  
  

## For fetching

  

![[Pasted image 20250222160247.png]]

  

When performing asynchronous operations like fetching data, JavaScript leverages promises. Here’s how it works:

  

- **setTimeout Callbacks:** When you use a function like `setTimeout`, its callback is added to the regular callback queue after the specified delay.

- **Promise Callbacks:** In contrast, promise callbacks (e.g., those from a `.then()` method) are placed in a separate microtask queue.

- **Event Loop Priority:** The event loop continuously checks the call stack. When the call stack is empty, it processes all tasks in the microtask queue before moving on to the callback queue. This means promise callbacks are executed before callbacks from functions like `setTimeout`.

  

This design ensures that promise-based asynchronous operations are handled with higher priority, leading to more efficient and predictable execution.

  

![[Pasted image 20250222160647.png]]

  

![[Pasted image 20250222160924.png]]

  
  

## What comes under the microtask queue ?

- All call back functions that comes through promises can come under the micro task queue.

- Mutation Observer

  - Keeps on checking for mutation on the DOM tree. Corresponding to any change it will execute call back function.

  - Callback functions from setTimeout, DOM Api interaction go inside call back queue.

  - The callback queue will only get time for execution only if all the corresponding task in the micro task queue are executed.

  - This may lead to starvation of the call back queue.

  
  


---

title: What is the event loop in JavaScript runtimes?

subtitle: What is the difference between call stack and task queue?

---

  

## TL;DR

  

The event loop is concept within the JavaScript runtime environment regarding how asynchronous operations are executed within JavaScript engines. It works as such:

  

1. The JavaScript engine starts executing scripts, placing synchronous operations on the call stack.

2. When an asynchronous operation is encountered (e.g., `setTimeout()`, HTTP request), it is offloaded to the respective Web API or Node.js API to handle the operation in the background.

3. Once the asynchronous operation completes, its callback function is placed in the respective queues – task queues (also known as macrotask queues / callback queues) or microtask queues. We will refer to "task queue" as "macrotask queue" from here on to better differentiate from the microtask queue.

4. The event loop continuously monitors the call stack and executes items on the call stack. If/when the call stack is empty:

   1. Microtask queue is processed. Microtasks include promise callbacks (`then`, `catch`, `finally`), `MutationObserver` callbacks, and calls to `queueMicrotask()`. The event loop takes the first callback from the microtask queue and pushes it to the call stack for execution. This repeats until the microtask queue is empty.

   2. Macrotask queue is processed. Macrotasks include web APIs like `setTimeout()`, HTTP requests, user interface event handlers like clicks, scrolls, etc. The event loop dequeues the first callback from the macrotask queue and pushes it onto the call stack for execution. However, after a macrotask queue callback is processed, the event loop does not proceed with the next macrotask yet! The event loop first checks the microtask queue. Checking the microtask queue is necessary as microtasks have higher priority than macrotask queue callbacks. The macrotask queue callback that was just executed could have added more microtasks!

      1. If the microtask queue is non-empty, process them as per the previous step.

      2. If the microtask queue is empty, the next macrotask queue callback is processed. This repeats until the macrotask queue is empty.

5. This process continues indefinitely, allowing the JavaScript engine to handle both synchronous and asynchronous operations efficiently without blocking the call stack.

  

The unfortunate truth is that it is extremely hard to explain the event loop well using only text. We recommend checking out one of the following excellent videos explaining the event loop:

  

- [JavaScript Visualized - Event Loop, Web APIs, (Micro)task Queue](https://www.youtube.com/watch?v=eiC58R16hb8) (2024): Lydia Hallie is a popular educator on JavaScript and this is the best recent videos explaining the event loop. There's also an [accompanying blog post](https://www.lydiahallie.com/blog/event-loop) for those who prefer detailed text-based explanations.

- [In the Loop](https://www.youtube.com/watch?v=cCOL7MC4Pl0) (2018): Jake Archibald previously from the Chrome team provides a visual demonstration of the event loop during JSConf 2018, accounting for different types of tasks.

- [What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ) (2014): Philip Robert's gave this epic talk at JSConf 2014 and it is one of the most viewed JavaScript videos on YouTube.

  

We recommend watching [Lydia's video](https://www.youtube.com/watch?v=eiC58R16hb8) as it is the most modern and concise explanation standing at only 13 minutes long whereas the other videos are at least 30 minutes long. Her video is sufficient for the purpose of interviews.

  

---

  

## Event loop in JavaScript

  

The event loop is the heart of JavaScript's asynchronous operation. It is a mechanism that handles the execution of code, allowing for asynchronous operations and ensuring that the single-threaded nature of JavaScript engines does not block the execution of the program.

  

### Parts of the event loop

  

To understand it better we need to understand about all the parts of the system. These components are part of the event loop:

  

#### Call stack

  

Call stack keeps track of the functions being executed in a program. When a function is called, it is added to the top of the call stack. When the function completes, it is removed from the call stack. This allows the program to keep track of where it is in the execution of a function and return to the correct location when the function completes. As the name suggests it is a Stack data structure which follows last-in-first-out.

  

#### Web APIs/Node.js APIs

  

Asynchronous operations like `setTimeout()`, HTTP requests, file I/O, etc., are handled by Web APIs (in the browser) or C++ APIs (in Node.js). These APIs are not part of the JavaScript engine and run on separate threads, allowing them to execute concurrently without blocking the call stack.

  

#### Task queue / Macrotask queue / Callback queue

  

The task queue, also known as the macrotask queue / callback queue / event queue, is a queue that holds tasks that need to be executed. These tasks are typically asynchronous operations, such as callbacks passed to web APIs (`setTimeout()`, `setInterval()`, HTTP requests, etc.), and user interface event handlers like clicks, scrolls, etc.

  

#### Microtasks queue

  

Microtasks are tasks that have a higher priority than macrotasks and are executed immediately after the currently executing script is completed and before the next macrotask is executed. Microtasks are usually used for more immediate, lightweight operations that should be executed as soon as possible after the current operation completes. There is a dedicated microtask queue for microtasks. Microtasks include promises callbacks (`then()`, `catch()`, and `finally()`), `await` statements, `queueMicrotask()`, and `MutationObserver` callbacks.

  

### Event loop order

  

1. The JavaScript engine starts executing scripts, placing synchronous operations on the call stack.

2. When an asynchronous operation is encountered (e.g., `setTimeout()`, HTTP request), it is offloaded to the respective Web API or Node.js API to handle the operation in the background.

3. Once the asynchronous operation completes, its callback function is placed in the respective queues – task queues (also known as macrotask queues / callback queues) or microtask queues. We will refer to "task queue" as "macrotask queue" from here on to better differentiate from the microtask queue.

4. The event loop continuously monitors the call stack and executes items on the call stack. If/when the call stack is empty:

   1. Microtask queue is processed. The event loop takes the first callback from the microtask queue and pushes it to the call stack for execution. This repeats until the microtask queue is empty.

   2. Macrotask queue is processed. The event loop dequeues the first callback from the macrotask queue and pushes it onto the call stack for execution. However, after a macrotask queue callback is processed, the event loop does not proceed with the next macrotask yet! The event loop first checks the microtask queue. Checking the microtask queue is necessary as microtasks have higher priority than macrotask queue callbacks. The macrotask queue callback that was just executed could have added more microtasks!

      1. If the microtask queue is non-empty, process them as per the previous step.

      2. If the microtask queue is empty, the next macrotask queue callback is processed. This repeats until the macrotask queue is empty.

5. This process continues indefinitely, allowing the JavaScript engine to handle both synchronous and asynchronous operations efficiently without blocking the call stack.

  

### Example

  

The following code logs some statements using a combination of normal execution, macrotasks, and microtasks.

  

```js

console.log('Start');

  

setTimeout(() => {

  console.log('Timeout 1');

}, 0);

  

Promise.resolve().then(() => {

  console.log('Promise 1');

});

  

setTimeout(() => {

  console.log('Timeout 2');

}, 0);

  

console.log('End');

  

// Console output:

// Start

// End

// Promise 1

// Timeout 1

// Timeout 2

```

  

Explanation of the output:

  

1. `Start` and `End` are logged first because they are part of the initial script.

2. `Promise 1` is logged next because promises are microtasks and microtasks are executed immediately after the items on the call stack.

3. `Timeout 1` and `Timeout 2` are logged last because they are macrotasks and are processed after the microtasks.

  

## Further reading and resources

  

- [The event loop - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop)

- [The Node.js Event Loop](https://nodejs.org/en/learn/asynchronous-work/event-loop-timers-and-nexttick)

- [Event loop: microtasks and macrotasks](https://javascript.info/event-loop)

- [JavaScript Visualized: Event Loop by Lydia Hallie](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif)

- ["JavaScript Visualized - Event Loop, Web APIs, (Micro)task Queue" by Lydia Hallie](https://www.lydiahallie.com/blog/event-loop)

- ["What the heck is the event loop anyway?" by Philip Robert](https://2014.jsconf.eu/speakers/philip-roberts-what-the-heck-is-the-event-loop-anyway.html)

- ["In The Loop" by Jake Archibald](https://www.youtube.com/watch?v=cCOL7MC4Pl0)