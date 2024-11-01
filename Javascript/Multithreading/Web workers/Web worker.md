---
tags:
  - webworker
  - worker
---
Web worker provides us with a way to run background tasks apart from the main thread. The task runs on a different thread than the main execution thread. It allows for long running computationally expensive task, preventing the user interface from becoming un responsive or janky.

### Steps
1. Create a new worker using the Webworker constructor.
2. postMessage  communicate with the worker
3. onmessage get back the respose from the worker.
4. onerror get back the value from the worker.
### Good Practice
- Check if worker is available.
### Code Example:

```html
<!DOCTYPE html>

<html lang="en">

  <head>

    <meta charset="UTF-8" />

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Web Worker Example</title>

  </head>

  <body>

    <h1>Web Worker Sum Calculation</h1>

  

    <label for="numberInput">Enter a number:</label>

    <input type="number" id="numberInput" value="1000000" />

    <button id="startCalculation">Calculate Sum</button>

  

    <p id="result">Sum:</p>

  

    <script src="main.js"></script>

  </body>

</html>
```

```js
// Check if the browser supports workers

if (window.Worker) {

  // Create a new Worker

  const myWorker = new Worker("worker.js");

  const inputElement = document.getElementById("numberInput");

  const buttonElement = document.getElementById("startCalculation");

  

  buttonElement.addEventListener("click", (event) => {

    // Post a message to the worker

    myWorker.postMessage(parseInt(inputElement?.value));

  });

  

  // Listen for messages from the worker

  myWorker.onmessage = function (event) {

    document.getElementById("result").textContent = `Sum: ${event.data}`;

  };

  

  // Error handling

  myWorker.onerror = function (error) {

    document.getElementById("result").textContent = `Error has occured`;

    console.log(error);

  };

}
```

```js
// Listen for messages from the main script

onmessage = function (event) {

  console.log("Value from Main Worker", event.data);

  

  const n = event.data;

  let sum = 0;

  for (let i = 1; i <= n; i++) {

    sum += i;

  }

  // Send the result back to the main thread

  self.postMessage(sum);

};
```