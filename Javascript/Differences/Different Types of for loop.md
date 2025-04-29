---
tags:
  - justlearn
  - for-loops
---
## **For Loops in JavaScript**

JavaScript provides different types of loops for iterating over data structures. Below are the most commonly used ones, their differences, and a mnemonic to remember them.

---

### **1. Traditional `for` Loop**

Used for iterating over numeric sequences or when you need explicit control over the iteration.

```js
for (let i = 0; i < 5; i++) {
  console.log(i); // Outputs: 0, 1, 2, 3, 4
}
```

- **Use case:** When you need full control over the loop (start, condition, step).
- **Works on:** Arrays and numeric sequences.
- **Allows modification?** Yes.

---

### **2. `for...of` Loop**

Used for iterating over values of **iterable objects** (Arrays, Strings, Sets, Maps).

```js
const arr = [10, 20, 30];
for (const num of arr) {
  console.log(num); // Outputs: 10, 20, 30
}
```

- **Use case:** When iterating over arrays or other iterable objects.
- **Works on:** Arrays, Strings, Maps, Sets.
- **Allows modification?** No, directly modifying elements doesn’t affect the original array.

---

### **3. `for...in` Loop**

Used for iterating over **keys (property names)** of an object.

```js
const obj = { name: "Alice", age: 25 };
for (const key in obj) {
  console.log(key, obj[key]); 
  // Outputs: name Alice, age 25
}
```

- **Use case:** Iterating over object properties.
- **Works on:** Objects (but also iterates over arrays' indices, which is not recommended).
- **Allows modification?** Yes, but use `Object.keys()` instead for better reliability.

---

### **4. `forEach()` Method**

Used for iterating over arrays, but with a callback function.

```js
const arr = [5, 10, 15];
arr.forEach((num) => console.log(num)); 
// Outputs: 5, 10, 15
```

- **Use case:** Iterating over an array when modifying elements is **not required**.
- **Works on:** Arrays.
- **Allows modification?** No (does not support `break` or `continue`).

---

## **Key Differences Between the Loops**

|Loop Type|Works On|Iterates Over|Can Modify?|Supports `break` & `continue`?|
|---|---|---|---|---|
|`for`|Arrays, Numbers|Indexes|✅ Yes|✅ Yes|
|`for...of`|Arrays, Strings, Sets, Maps|Values|❌ No|✅ Yes|
|`for...in`|Objects (also Arrays but not recommended)|Keys|✅ Yes|✅ Yes|
|`forEach`|Arrays|Values|❌ No|❌ No (cannot break/continue)|

---

## **Mnemonic to Remember the Differences**

### **"FOPI" – For, Of, Properties, Iterate"**

- **F** → `for` loop (Full control)
- **O** → `for...of` (Over values)
- **P** → `for...in` (Properties of an object)
- **I** → `forEach` (Iterate through array with function)

This helps in quickly recalling the purpose of each loop. 🚀