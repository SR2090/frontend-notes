

Event Capturing
---
title: Describe event capturing in JavaScript and browsers
---

## TL;DR

Event capturing is a lesser-used counterpart to [event bubbling](Event%20Bubbling.md) in the DOM event propagation mechanism. It follows the opposite order, where an event triggers first on the ancestor element and then travels down to the target element.

Event capturing is rarely used as compared to event bubbling, but it can be used in specific scenarios where you need to intercept events at a higher level before they reach the target element. It is disabled by default but can be enabled through an option on `addEventListener()`.

---

## What is event capturing?

Event capturing is a propagation mechanism in the DOM (Document Object Model) where an event, such as a click or a keyboard event, is first triggered at the root of the document and then flows down through the DOM tree to the target element.

Capturing has a higher priority than bubbling, meaning that capturing event handlers are executed before bubbling event handlers, as shown by the phases of event propagation:

- **Capturing phase**: The event moves down towards the target element
- **Target phase**: The event reaches the target element
- **Bubbling phase**: The event bubbles up from the target element

Note that event capturing is disabled by default. To enable it you have to pass the capture option into `addEventListener()`.

## Capturing phase

During the capturing phase, the event starts at the document root and propagates down to the target element. Any event listeners on ancestor elements in this path will be triggered before the target element's handler. But note that event capturing can't happen until the third argument of `addEventListener()` is set to `true` as shown below (default value is `false`).

Here's an example using modern ES2015 syntax to demonstrate event capturing:

```js
// HTML:
// <div id="parent">
//   <button id="child">Click me!</button>
// </div>

const parent = document.getElementById('parent');
const child = document.getElementById('child');

parent.addEventListener(
  'click',
  () => {
    console.log('Parent element clicked (capturing)');
  },
  true, // Set third argument to true for capturing
);

child.addEventListener('click', () => {
  console.log('Child element clicked');
});
```

When you click the "Click me!" button, it will trigger the parent element's capturing handler first, followed by the child element's handler.

## Stopping propagation

Event propagation can be stopped during the capturing phase using the `stopPropagation()` method. This prevents the event from traveling further down the DOM tree.

```js
// HTML:
// <div id="parent">
//   <button id="child">Click me!</button>
// </div>

const parent = document.getElementById('parent');
const child = document.getElementById('child');

parent.addEventListener(
  'click',
  (event) => {
    console.log('Parent element clicked (capturing)');
    event.stopPropagation(); // Stop event propagation
  },
  true,
);

child.addEventListener('click', () => {
  console.log('Child element clicked');
});
```

As a result of stopping event propagation, just the `parent` event listener will now be called when you click the "Click Me!" button, and the `child` event listener will never be called because the event propagation has stopped at the `parent` element.

## Uses of event capturing

Event capturing is rarely used as compared to event bubbling, but it can be used in specific scenarios where you need to intercept events at a higher level before they reach the target element.

- **Stopping event bubbling:** Imagine you have a nested element (like a button) inside a container element. Clicking the button might also trigger a click event on the container. By using enabling event capturing on the container's event listener, you can capture the click event there and prevent it from traveling down to the button, potentially causing unintended behavior.
- **Custom dropdown menus:**: When building custom dropdown menus, you might want to capture clicks outside the menu element to close the menu. Using `capture: true` on the `document` object allows you to listen for clicks anywhere on the page and close the menu if the click happens outside its boundaries.
- **Efficiency in certain scenarios:**: In some situations, event capturing can be slightly more efficient than relying on bubbling. This is because the event doesn't need to propagate through all child elements before reaching the handler. However, the performance difference is usually negligible for most web applications.

## Further reading

- [Event Capturing | MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_capture)
- [Bubbling and Capturing | JavaScript.info](https://javascript.info/bubbling-and-capturing)
- [W3C DOM Level 3 Events Specification](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow)