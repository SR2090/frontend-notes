
## 🌊 What is Event Bubbling?

> **Event Bubbling** is the process where an event starts from the **target element** and **bubbles up** (propagates) through its ancestors in the DOM tree.

Think of it like **bubbles rising up** through the layers of HTML elements.

---

### 📚 Example

```html
<div id="outer">
  <button id="inner">Click Me</button>
</div>
```

```js
document.getElementById("outer").addEventListener("click", () => {
  console.log("Outer DIV clicked");
});

document.getElementById("inner").addEventListener("click", () => {
  console.log("Button clicked");
});
```

### ✅ Output when you click the button:

```
Button clicked
Outer DIV clicked
```

Why?

- Event first fires on the **`button`**, then **bubbles up** to the `div`.
    

---

## 🧪 Order of Event Bubbling

1. **Target Phase** – where the event is triggered (e.g., the `button`)
    
2. **Bubbling Phase** – moves **upward** from target to parent, grandparent, and so on.
    

---

## ❌ Stopping Event Bubbling

Use:

```js
event.stopPropagation();
```

Example:

```js
document.getElementById("inner").addEventListener("click", (event) => {
  event.stopPropagation();
  console.log("Button clicked without bubbling");
});
```

Now the `outer` `div` won’t log anything when the button is clicked.

---

## 💡 Real-World Use Case

- **Event Delegation**: Use bubbling to attach one handler to a parent element instead of many children.
    

```js
document.getElementById("list").addEventListener("click", function (e) {
  if (e.target.tagName === "LI") {
    console.log("List item clicked:", e.target.textContent);
  }
});
```

---

Let me know if you want a diagram or animation-based example!