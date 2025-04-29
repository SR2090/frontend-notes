Below is an explanation of what is happening when you run this code, why it behaves that way, and some fundamental concepts involved—specifically dealing with **variable scoping** and **asynchronous callbacks**.

```js
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log("value is " + i);
  });
}
```

---

## Step-by-Step Explanation

1. **The `for` Loop Execution**  
    The loop runs from `i = 0` up to `i < 10`. That is, the loop executes its body 10 times, incrementing `i` by 1 each iteration.
    
2. **What Happens Inside the `for` Loop**  
    Inside the loop, you call `setTimeout(...)`. This schedules a callback (the function you pass to `setTimeout`) to be executed in the future (after a certain delay, which defaults to 0 milliseconds if not specified).
    
3. **The Key Point: `var` Scoping**  
    When using `var`, the variable `i` is function-scoped (or global-scoped if not in a function). It means **there is only one `i` variable** being used throughout the entire loop. By the time the callbacks actually run, the loop has already completed, and `i` will have the value **10**.
    
4. **Callback Execution Timing**  
    The callbacks are added to the **event queue** and will only run once the main thread (the loop and any code after it) has finished executing. Therefore, every callback uses the final value of `i` after the loop—by which time `i` is 10.
    

Hence, the output will be:

```
value is 10
value is 10
value is 10
value is 10
value is 10
value is 10
value is 10
value is 10
value is 10
value is 10
```

(10 times “value is 10”)

---

## Visualizing the Process

1. **Loop iteration**
    
    - **Iteration 1:** i = 0 -> Schedules a callback: “later, log `value is i`”
    - **Iteration 2:** i = 1 -> Schedules a callback: “later, log `value is i`”
    - ...
    - **Iteration 10:** i = 9 -> Schedules a callback: “later, log `value is i`”
    - Then i becomes 10, loop condition `i < 10` fails, loop stops.
2. **After the loop**
    
    - Now `i` is 10.
    - The `setTimeout` callbacks start to run (in some order, typically in the same order they were scheduled).
    - Each callback references the single, final `i`, which is 10.

---

## Why Does This Happen?

- **`var` declarations are function-scoped**, meaning the variable `i` is declared once in the function (or global scope if not inside a function). All callbacks share that same `i`.
- Each scheduled function is not called immediately. When they finally run, they see the _current value_ of `i`, which is 10.

---

## How to Log 0 to 9 Instead

To capture each value of `i` at the time we schedule the callback, we need a new variable (or a closure) per iteration. There are two common ways to fix this:

### 1. Using `let` Instead of `var`

`let` is _block-scoped_. That means each iteration of the loop gets its own new `i`:

```js
for (let i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log("value is " + i);
  });
}
```

Now, when the callback runs, it references the `i` that was in scope during that particular iteration, so you get:

```
value is 0
value is 1
value is 2
...
value is 9
```

### 2. Using an IIFE (Immediately Invoked Function Expression) with `var`

Before ES6 and `let`, a classic pattern was to create a **new scope** by wrapping the callback code in a function that is immediately invoked. For example:

```js
for (var i = 0; i < 10; i++) {
  (function(currentValue) {
    setTimeout(function() {
      console.log("value is " + currentValue);
    });
  })(i);
}
```

Here, `currentValue` is a parameter to the immediately invoked function. At each iteration, `currentValue` takes on the value of `i` at that moment. Thus, each callback closes over that specific number.

---

## Summary and Key Points

1. **`var` is Function-Scoped**  
    In this scenario, `i` refers to one single variable. When the loop ends, `i` is 10, so all callbacks see `i = 10`.
    
2. **Callbacks Run Later**  
    The functions inside `setTimeout` run asynchronously, after the loop completes, so you get the final value of `i`.
    
3. **How to Fix It**
    
    - Use `let` for block-scoping: `for (let i = 0; ...) { ... }`
    - Or create closures using IIFEs or other patterns to preserve the current iteration value.
4. **Best Practice**  
    In modern JavaScript, using `let` (or `const` where suitable) is preferred over `var` to avoid these scoping confusions.
    

---

**Hence, the reason you see `"value is 10"` printed 10 times is because the variable `i` gets hoisted and updated on each loop iteration, and the final value at the time the callbacks run is `10`.**


![[Pasted image 20250302133141.png]]


###### 17. What's the output?

```javascript
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = 'Lydia';
const age = 21;

getPersonInfo`${person} is ${age} years old`;
```

- A: `"Lydia"` `21` `["", " is ", " years old"]`
- B: `["", " is ", " years old"]` `"Lydia"` `21`
- C: `"Lydia"` `["", " is ", " years old"]` `21`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

If you use tagged template literals, the value of the first argument is always an array of the string values. The remaining arguments get the values of the passed expressions!

</p>
</details>


This syntax is called a **tagged template literal** in JavaScript. It allows you to process template literals using a function.

### **Breaking It Down**

```js
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = 'Lydia';
const age = 21;

getPersonInfo`${person} is ${age} years old`;
```

### **1. Understanding Tagged Template Literals**

- The **backticks (` `` `)** indicate a **template literal**.
- When you prefix a template literal with a function (`getPersonInfo` in this case), it **does not** execute the function normally.
- Instead, JavaScript **parses** the template and passes it to the function in a structured way.

### **2. What is Passed to `getPersonInfo`?**

The function **does not** receive the full string like a normal function call.

#### **It receives:**

1. An **array of string literals** (`one`)
2. The **interpolated expressions** (`two`, `three`, etc.) as separate arguments.

So, internally:

```js
getPersonInfo(["", " is ", " years old"], "Lydia", 21);
```

#### **Breaking it down:**

- `one` → `["", " is ", " years old"]` → An array of string segments.
- `two` → `"Lydia"` → First interpolated value (`${person}`).
- `three` → `21` → Second interpolated value (`${age}`).

### **3. Console Output**

```txt
[ '', ' is ', ' years old' ]
Lydia
21
```

### **Why Use Tagged Template Literals?**

Tagged template literals are useful for:

- **Custom String Processing** (e.g., formatting)
- **Escaping HTML for security (XSS protection)**
- **Internationalization (i18n)**
- **Styled Components in React**

### **Example: Formatting a Sentence**

```js
function format(strings, ...values) {
  return strings.reduce((result, str, i) => result + str + (values[i] ? `[${values[i]}]` : ""), "");
}

const name = "Alice";
const age = 25;

console.log(format`${name} is ${age} years old`);
// Output: "Alice is [25] years old"
```

Would you like an example use case in a real-world scenario? 🚀





### **Real-World Use Cases of Tagged Template Literals**

#### **1. Preventing XSS Attacks (HTML Escaping)**

One of the most practical use cases is **sanitizing user input** to prevent **Cross-Site Scripting (XSS) attacks** when inserting user content into HTML.

##### **Example: Escaping HTML**

```js
function escapeHTML(strings, ...values) {
  const escape = (str) =>
    str.replace(/&/g, "&amp;")
       .replace(/</g, "&lt;")
       .replace(/>/g, "&gt;")
       .replace(/"/g, "&quot;")
       .replace(/'/g, "&#039;");
  
  return strings.reduce((result, str, i) => 
    result + str + (values[i] ? escape(String(values[i])) : ""), "");
}

const userInput = `<script>alert("Hacked!");</script>`;
const safeHTML = escapeHTML`User said: ${userInput}`;

console.log(safeHTML);
// Output: User said: &lt;script&gt;alert(&quot;Hacked!&quot;);&lt;/script&gt;
```

🔹 This ensures **any malicious script won’t execute**, making the website more secure.

---

#### **2. Styled Components in React**

Tagged template literals are widely used in **Styled Components** (a popular CSS-in-JS library for React).

##### **Example: Dynamic Styles with Styled Components**

```js
import styled from 'styled-components';

const Button = styled.button`
  background-color: ${(props) => (props.primary ? "blue" : "gray")};
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
`;

function App() {
  return <Button primary>Click Me</Button>;
}

export default App;
```

🔹 The function processes the **CSS template** and **injects dynamic values**.

---

#### **3. Custom Logging (Adding Timestamps)**

A **custom logger** can enhance debugging by tagging log messages with timestamps.

##### **Example: Logging Messages with Time**

```js
function logWithTimestamp(strings, ...values) {
  const timestamp = new Date().toLocaleTimeString();
  return `[${timestamp}] ` + strings.reduce((result, str, i) => result + str + (values[i] || ""), "");
}

const user = "Alice";
console.log(logWithTimestamp`User ${user} logged in.`);
// Output: [12:30:45 PM] User Alice logged in.
```

🔹 Helps in **better tracking** of logs in large applications.

---

#### **4. Formatting Numbers (Currency, Decimal Places)**

You can create a tagged template literal to format currency values dynamically.

##### **Example: Currency Formatter**

```js
function currency(strings, ...values) {
  return strings.reduce((result, str, i) =>
    result + str + (values[i] ? `$${parseFloat(values[i]).toFixed(2)}` : ""), "");
}

const price = 49.99;
console.log(currency`Total price is ${price}.`);
// Output: "Total price is $49.99."
```

🔹 Ensures consistent number formatting across your app.

---

#### **5. Internationalization (i18n) - Dynamic Language Translations**

Tagged template literals can be used to dynamically **translate text** based on the user’s selected language.

##### **Example: i18n Translations**

```js
const translations = {
  en: { welcome: "Hello", name: "Your name is" },
  fr: { welcome: "Bonjour", name: "Votre nom est" },
};

function i18n(strings, ...values) {
  const lang = "fr"; // Change this dynamically based on user preference
  return strings.reduce((result, str, i) =>
    result + str + (values[i] ? translations[lang][values[i]] || values[i] : ""), "");
}

console.log(i18n`${"welcome"}! ${"name"} John.`);
// Output: "Bonjour! Votre nom est John."
```

🔹 Makes applications **multi-lingual** without needing **if-else conditions**.

---

### **Summary**

Tagged template literals allow you to: ✅ **Process template literals dynamically**  
✅ **Sanitize user input to prevent XSS attacks**  
✅ **Use CSS-in-JS for styling in React**  
✅ **Format logs, numbers, and currency dynamically**  
✅ **Enable multilingual support without boilerplate code**

Would you like an advanced example, like creating your own **templating engine** using this? 🚀




###### 19. What's the output?

```javascript
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

- A: `"number"`
- B: `"array"`
- C: `"object"`
- D: `"NaN"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The rest parameter (`...args`) lets us "collect" all remaining arguments into an array. An array is an object, so `typeof args` returns `"object"`

</p>
</details>



###### 22. How long is cool_secret accessible?

```javascript
sessionStorage.setItem('cool_secret', 123);
```

- A: Forever, the data doesn't get lost.
- B: When the user closes the tab.
- C: When the user closes the entire browser, not only the tab.
- D: When the user shuts off their computer.

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The data stored in `sessionStorage` is removed after closing the _tab_.

If you used `localStorage`, the data would've been there forever, unless for example `localStorage.clear()` is invoked.

</p>
</details>


###### 28. What's the output?

```javascript
String.prototype.giveLydiaPizza = () => {
  return 'Just give Lydia pizza already!';
};

const name = 'Lydia';

console.log(name.giveLydiaPizza())
```

- A: `"Just give Lydia pizza already!"`
- B: `TypeError: not a function`
- C: `SyntaxError`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

`String` is a built-in constructor, that we can add properties to. I just added a method to its prototype. Primitive strings are automatically converted into a string object, generated by the string prototype function. So, all strings (string objects) have access to that method!

</p>
</details>

---



###### 29. What's the output?

```javascript
const a = {};
const b = { key: 'b' };
const c = { key: 'c' };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

- A: `123`
- B: `456`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Object keys are automatically converted into strings. We are trying to set an object as a key to object `a`, with the value of `123`.

However, when we stringify an object, it becomes `"[object Object]"`. So what we are saying here, is that `a["[object Object]"] = 123`. Then, we can try to do the same again. `c` is another object that we are implicitly stringifying. So then, `a["[object Object]"] = 456`.

Then, we log `a[b]`, which is actually `a["[object Object]"]`. We just set that to `456`, so it returns `456`.

</p>
</details>

---



###### 32. When you click the paragraph, what's the logged output?

```html
<div onclick="console.log('div')">
  <p onclick="console.log('p')">
    Click here!
  </p>
</div>
```

- A: `p` `div`
- B: `div` `p`
- C: `p`
- D: `div`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

If we click `p`, we see two logs: `p` and `div`. During event propagation, there are 3 phases: capturing, targeting, and bubbling. By default, event handlers are executed in the bubbling phase (unless you set `useCapture` to `true`). It goes from the deepest nested element outwards.

</p>
</details>

---




###### 34. What's the output?

```javascript
function sayHi() {
  return (() => 0)();
}

console.log(typeof sayHi());
```

- A: `"object"`
- B: `"number"`
- C: `"function"`
- D: `"undefined"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The `sayHi` function returns the returned value of the immediately invoked function expression (IIFE). This function returned `0`, which is type `"number"`.
	
FYI: `typeof` can return the following list of values: `undefined`, `boolean`, `number`, `bigint`, `string`, `symbol`, `function` and `object`. Note that `typeof null` returns `"object"`.

</p>
</details>

---


###### 37. What's the output?

```javascript
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers);
```

- A: `[1, 2, 3, null x 7, 11]`
- B: `[1, 2, 3, 11]`
- C: `[1, 2, 3, empty x 7, 11]`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

When you set a value to an element in an array that exceeds the length of the array, JavaScript creates something called "empty slots". These actually have the value of `undefined`, but you will see something like:

`[1, 2, 3, empty x 7, 11]`

depending on where you run it (it's different for every browser, node, etc.)

</p>
</details>

---



###### 38. What's the output?

```javascript
(() => {
  let x, y;
  try {
    throw new Error();
  } catch (x) {
    (x = 1), (y = 2);
    console.log(x);
  }
  console.log(x);
  console.log(y);
})();
```

- A: `1` `undefined` `2`
- B: `undefined` `undefined` `undefined`
- C: `1` `1` `2`
- D: `1` `undefined` `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The `catch` block receives the argument `x`. This is not the same `x` as the variable when we pass arguments. This variable `x` is block-scoped.

Later, we set this block-scoped variable equal to `1`, and set the value of the variable `y`. Now, we log the block-scoped variable `x`, which is equal to `1`.

Outside of the `catch` block, `x` is still `undefined`, and `y` is `2`. When we want to `console.log(x)` outside of the `catch` block, it returns `undefined`, and `y` returns `2`.

</p>
</details>

---



###### 44. What's the output?

```javascript
function* generator(i) {
  yield i;
  yield i * 2;
}

const gen = generator(10);

console.log(gen.next().value);
console.log(gen.next().value);
```

- A: `[0, 10], [10, 20]`
- B: `20, 20`
- C: `10, 20`
- D: `0, 10 and 10, 20`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Regular functions cannot be stopped mid-way after invocation. However, a generator function can be "stopped" midway, and later continue from where it stopped. Every time a generator function encounters a `yield` keyword, the function yields the value specified after it. Note that the generator function in that case doesn’t _return_ the value, it _yields_ the value.

First, we initialize the generator function with `i` equal to `10`. We invoke the generator function using the `next()` method. The first time we invoke the generator function, `i` is equal to `10`. It encounters the first `yield` keyword: it yields the value of `i`. The generator is now "paused", and `10` gets logged.

Then, we invoke the function again with the `next()` method. It starts to continue where it stopped previously, still with `i` equal to `10`. Now, it encounters the next `yield` keyword, and yields `i * 2`. `i` is equal to `10`, so it returns `10 * 2`, which is `20`. This results in `10, 20`.

</p>
</details>

---



###### 46. What's the output?

```javascript
let person = { name: 'Lydia' };
const members = [person];
person = null;

console.log(members);
```

- A: `null`
- B: `[null]`
- C: `[{}]`
- D: `[{ name: "Lydia" }]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

First, we declare a variable `person` with the value of an object that has a `name` property.

<img src="https://i.imgur.com/TML1MbS.png" width="200">

Then, we declare a variable called `members`. We set the first element of that array equal to the value of the `person` variable. Objects interact by _reference_ when setting them equal to each other. When you assign a reference from one variable to another, you make a _copy_ of that reference. (note that they don't have the _same_ reference!)

<img src="https://i.imgur.com/FSG5K3F.png" width="300">

Then, we set the variable `person` equal to `null`.

<img src="https://i.imgur.com/sYjcsMT.png" width="300">

We are only modifying the value of the `person` variable, and not the first element in the array, since that element has a different (copied) reference to the object. The first element in `members` still holds its reference to the original object. When we log the `members` array, the first element still holds the value of the object, which gets logged.

</p>
</details>

---

###### 49. What's the value of `num`?

```javascript
const num = parseInt('7*6', 10);
```

- A: `42`
- B: `"42"`
- C: `7`
- D: `NaN`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Only the first number in the string is returned. Based on the _radix_ (the second argument in order to specify what type of number we want to parse it to: base 10, hexadecimal, octal, binary, etc.), the `parseInt` checks whether the characters in the string are valid. Once it encounters a character that isn't a valid number in the radix, it stops parsing and ignores the following characters.

`*` is not a valid number. It only parses `"7"` into the decimal `7`. `num` now holds the value of `7`.

</p>
</details>

---

###### 50. What's the output?

```javascript
[1, 2, 3].map(num => {
  if (typeof num === 'number') return;
  return num * 2;
});
```

- A: `[]`
- B: `[null, null, null]`
- C: `[undefined, undefined, undefined]`
- D: `[ 3 x empty ]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

When mapping over the array, the value of `num` is equal to the element it’s currently looping over. In this case, the elements are numbers, so the condition of the if statement `typeof num === "number"` returns `true`. The map function creates a new array and inserts the values returned from the function.

However, we don’t return a value. When we don’t return a value from the function, the function returns `undefined`. For every element in the array, the function block gets called, so for each element we return `undefined`.

</p>
</details>

---


###### 51. What's the output?

```javascript
function getInfo(member, year) {
  member.name = 'Lydia';
  year = '1998';
}

const person = { name: 'Sarah' };
const birthYear = '1997';

getInfo(person, birthYear);

console.log(person, birthYear);
```

- A: `{ name: "Lydia" }, "1997"`
- B: `{ name: "Sarah" }, "1998"`
- C: `{ name: "Lydia" }, "1998"`
- D: `{ name: "Sarah" }, "1997"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Arguments are passed by _value_, unless their value is an object, then they're passed by _reference_. `birthYear` is passed by value, since it's a string, not an object. When we pass arguments by value, a _copy_ of that value is created (see question 46).

The variable `birthYear` has a reference to the value `"1997"`. The argument `year` also has a reference to the value `"1997"`, but it's not the same value as `birthYear` has a reference to. When we update the value of `year` by setting `year` equal to `"1998"`, we are only updating the value of `year`. `birthYear` is still equal to `"1997"`.

The value of `person` is an object. The argument `member` has a (copied) reference to the _same_ object. When we modify a property of the object `member` has a reference to, the value of `person` will also be modified, since they both have a reference to the same object. `person`'s `name` property is now equal to the value `"Lydia"`

</p>
</details>

---


###### 52. What's the output?

```javascript
function greeting() {
  throw 'Hello world!';
}

function sayHi() {
  try {
    const data = greeting();
    console.log('It worked!', data);
  } catch (e) {
    console.log('Oh no an error:', e);
  }
}

sayHi();
```

- A: `It worked! Hello world!`
- B: `Oh no an error: undefined`
- C: `SyntaxError: can only throw Error objects`
- D: `Oh no an error: Hello world!`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

With the `throw` statement, we can create custom errors. With this statement, you can throw exceptions. An exception can be a <b>string</b>, a <b>number</b>, a <b>boolean</b> or an <b>object</b>. In this case, our exception is the string `'Hello world!'`.

With the `catch` statement, we can specify what to do if an exception is thrown in the `try` block. An exception is thrown: the string `'Hello world!'`. `e` is now equal to that string, which we log. This results in `'Oh an error: Hello world!'`.

</p>
</details>

---



###### 53. What's the output?

```javascript
function Car() {
  this.make = 'Lamborghini';
  return { make: 'Maserati' };
}

const myCar = new Car();
console.log(myCar.make);
```

- A: `"Lamborghini"`
- B: `"Maserati"`
- C: `ReferenceError`
- D: `TypeError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

When a constructor function is called with the `new` keyword, it creates an object and sets the `this` keyword to refer to that object. By default, if the constructor function doesn't explicitly return anything, it will return the newly created object.

In this case, the constructor function `Car` explicitly returns a new object with `make` set to `"Maserati"`, which overrides the default behavior. Therefore, when `new Car()` is called, the _returned_ object is assigned to `myCar`, resulting in the output being `"Maserati"` when `myCar.make` is accessed.

</p>
</details>

---



###### 54. What's the output?

```javascript
(() => {
  let x = (y = 10);
})();

console.log(typeof x);
console.log(typeof y);
```

- A: `"undefined", "number"`
- B: `"number", "number"`
- C: `"object", "number"`
- D: `"number", "undefined"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

`let x = (y = 10);` is actually shorthand for:

```javascript
y = 10;
let x = y;
```

When we set `y` equal to `10`, we actually add a property `y` to the global object (`window` in the browser, `global` in Node). In a browser, `window.y` is now equal to `10`.

Then, we declare a variable `x` with the value of `y`, which is `10`. Variables declared with the `let` keyword are _block scoped_, they are only defined within the block they're declared in; the immediately invoked function expression (IIFE) in this case. When we use the `typeof` operator, the operand `x` is not defined: we are trying to access `x` outside of the block it's declared in. This means that `x` is not defined. Values who haven't been assigned a value or declared are of type `"undefined"`. `console.log(typeof x)` returns `"undefined"`.

However, we created a global variable `y` when setting `y` equal to `10`. This value is accessible anywhere in our code. `y` is defined, and holds a value of type `"number"`. `console.log(typeof y)` returns `"number"`.

</p>
</details>

---


###### 55. What's the output?

```javascript
class Dog {
  constructor(name) {
    this.name = name;
  }
}

Dog.prototype.bark = function() {
  console.log(`Woof I am ${this.name}`);
};

const pet = new Dog('Mara');

pet.bark();

delete Dog.prototype.bark;

pet.bark();
```

- A: `"Woof I am Mara"`, `TypeError`
- B: `"Woof I am Mara"`, `"Woof I am Mara"`
- C: `"Woof I am Mara"`, `undefined`
- D: `TypeError`, `TypeError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We can delete properties from objects using the `delete` keyword, also on the prototype. By deleting a property on the prototype, it is not available anymore in the prototype chain. In this case, the `bark` function is not available anymore on the prototype after `delete Dog.prototype.bark`, yet we still try to access it.

When we try to invoke something that is not a function, a `TypeError` is thrown. In this case `TypeError: pet.bark is not a function`, since `pet.bark` is `undefined`.

</p>
</details>

---

###### 58. What's the output?

```javascript
const name = 'Lydia';
age = 21;

console.log(delete name);
console.log(delete age);
```

- A: `false`, `true`
- B: `"Lydia"`, `21`
- C: `true`, `true`
- D: `undefined`, `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The `delete` operator returns a boolean value: `true` on a successful deletion, else it'll return `false`. However, variables declared with the `var`, `const`, or `let` keywords cannot be deleted using the `delete` operator.

The `name` variable was declared with a `const` keyword, so its deletion is not successful: `false` is returned. When we set `age` equal to `21`, we actually added a property called `age` to the global object. You can successfully delete properties from objects this way, also the global object, so `delete age` returns `true`.

</p>
</details>

---

```js
const obj = {
    name: "JavaScript",
    greet: function() {
        setTimeout(function() {
            console.log(this.name); // 'this' refers to window, not obj
        }, 1000);
    }
};

obj.greet(); // Undefined in strict mode, or logs window.name (if set)
```

The this here inside the method will always be the global object. 

