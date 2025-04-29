![[Pasted image 20250419111452.png]]

The loadData can get any type of object and depending on the type we have to perform appropriate action.

There are different of type guards in ts example: #tspattern
![[Pasted image 20250419111753.png]]

![[Pasted image 20250419111911.png]]




### Type Guard using js specfic keywrod InstanceOf
#tspattern
![[Pasted image 20250419112701.png]]


![[Pasted image 20250419112738.png]]

![[Pasted image 20250419112842.png]]


#tspattern
### Creating type checking as separate method
![[Pasted image 20250419113329.png]]
The return type of this function is a predicate under the hood it is a boolean value.
This allows for type inference as boolean value will not contain the path that will contained by FileSource object.

## 🔍 Outsourcing TypeScript Type Checking to a Separate Function with a Type Predicate

### ✅ What’s the Goal?

Move the type checking logic **out of your main code** into a **reusable function**, and **return a _type predicate_** instead of a plain boolean.

---

### 🧠 Why Not Just Return a Boolean?

Because a type predicate allows **TypeScript to narrow the type** based on the function's return value.  
Whereas a `boolean` return doesn't help TypeScript infer types.

---

### 🧩 Syntax Overview

```ts
function isString(value: unknown): value is string {
  return typeof value === "string";
}
```

Here, `value is string` is a **type predicate** (not just `boolean`).  
It tells TypeScript: “If this function returns true, then treat `value` as `string` from now on.”

---

### 🧪 Example Use Case

#### ✅ Before: Inline Type Checking

```ts
function logIfString(val: unknown) {
  if (typeof val === "string") {
    console.log(val.toUpperCase());
  }
}
```

#### ✅ After: Outsourced Type Predicate Function

```ts
function isString(val: unknown): val is string {
  return typeof val === "string";
}

function logIfString(val: unknown) {
  if (isString(val)) {
    // val is now known as string
    console.log(val.toUpperCase());
  }
}
```

---

### 💡 Real-world Scenario

Suppose you're parsing API data:

```ts
type User = { name: string; age: number };

function isUser(obj: any): obj is User {
  return (
    obj &&
    typeof obj.name === "string" &&
    typeof obj.age === "number"
  );
}

const data: unknown = fetchUserFromAPI();

if (isUser(data)) {
  console.log(data.name.toUpperCase()); // ✅ Safe access
} else {
  console.error("Invalid user data");
}
```

---

### ✅ Benefits

|Advantage|Description|
|---|---|
|✅ Type Safety|You narrow down the type after checking.|
|🔁 Reusability|Centralized type-checking logic.|
|🧹 Clean Code|Avoid repeating `typeof` checks everywhere.|

---

### 🤔 Extra: What if You Use `boolean` Instead?

```ts
function isString(val: unknown): boolean {
  return typeof val === "string";
}

function log(val: unknown) {
  if (isString(val)) {
    // ❌ val is still `unknown` — TS can't infer type
    val.toUpperCase(); // ❌ Error!
  }
}
```

---

### 📌 Summary Points

- Use `val is Type` in return type → It’s a **type predicate**
    
- Helps **narrow types** inside conditions
    
- Enables **reusable and clean type-checking**
    

---

### ❓Interview-style Quick Questions

**Q1:** What is the return type of a function that narrows types in TS?  
👉 `value is SomeType` (a _type predicate_)

**Q2:** Why use a type predicate instead of `boolean`?  
👉 To enable **type narrowing** inside `if` statements.

**Q3:** Can you use type predicates with custom types?  
👉 ✅ Yes! Works great for complex interfaces.

---

Would you like a cheat sheet of common `isType()` helpers (like `isString`, `isNumber`, etc.) too?