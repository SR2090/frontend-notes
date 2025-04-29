[] is a placeholder for dynamic properties where we are not aware of the number of properties that we can have in an object.

we define the name placeholder and type for the key name in the object within the square brackets.

![[Pasted image 20250419123226.png]]

We can now dynamically add properties to this key.

Here's a crisp and **revision-friendly explanation** of **Index Types** in TypeScript with examples and key takeaways:

---

## 🔎 What is an Index Type in TypeScript?

**Index types** let you define **objects with dynamic keys**, where the key and value types are **constrained**.

It’s useful when you don’t know the exact property names ahead of time, but you know the shape of the keys and values.

---

### 🔑 Syntax

```ts
type MyType = {
  [key: string]: number;
};
```

This means:  
**Any key of type `string` → must have value of type `number`**

---

### 📦 Example

```ts
const salaries: { [employee: string]: number } = {
  Alice: 50000,
  Bob: 60000,
  Charlie: 55000,
};

console.log(salaries["Bob"]); // ✅ 60000
```

Here:

- Key can be any string like `"Alice"`, `"Bob"` etc.
    
- Value **must be** a number
    

---

### 📘 Use Case: Dynamic Objects

```ts
type ErrorMessages = {
  [field: string]: string;
};

const formErrors: ErrorMessages = {
  email: "Invalid email",
  password: "Password too short",
};
```

Perfect when form field names are not fixed.

---

### ❗Important Notes

|Feature|Explanation|
|---|---|
|`string` as key|Allows any string keys|
|`number` as key|Actually means indexable with numbers (`array-like`)|
|Key + specific props|You can mix specific keys and indexed types|

```ts
type Mix = {
  status: string;
  [prop: string]: string;
};
```

---

### ❓Why Use Index Types?

- 💡 To define _dictionary-like objects_
    
- ✅ To ensure all values conform to a type
    
- 🔄 Useful for mapping keys dynamically
    

---

### 🧠 Bonus: `keyof` with Index Types

```ts
type Person = { name: string; age: number };
type PersonKeys = keyof Person; // "name" | "age"
```

You can now write:

```ts
function getProperty(obj: Person, key: PersonKeys) {
  return obj[key];
}
```

✅ This is part of **indexed access types** with `keyof`.

---

### 📌 Summary

- Index types are for objects with **dynamic keys**
    
- Syntax: `{ [key: string]: Type }`
    
- Helps create **type-safe dictionaries**
    
- Combine with `keyof` for more advanced patterns
    

---

### 🔁 Quick Quiz

**Q:** What does this mean?

```ts
type T = { [key: string]: boolean };
```

**A:** Any string key must map to a boolean value.

**Q:** Can you access a value safely from an index type?

```ts
const t: T = { a: true };
t["b"] // ✅ boolean (true/false)
```

Let me know if you want a mini-cheat sheet for all object typing styles like `Record`, `Partial`, index types etc.

