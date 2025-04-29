![[Pasted image 20250419152342.png]]

![[Pasted image 20250419153058.png]]

![[Pasted image 20250419153215.png]]

TS able to infer the appropriate types.

![[Pasted image 20250419154128.png]]
Generic Class

![[Pasted image 20250419154139.png]]
Generic Interface

## 🔁 What are Generics in TypeScript?

> **Generics = Reusable, flexible types that work across many data types without losing type safety**

---

### 🧠 Core Idea:

You **pass types like variables**, so functions, interfaces, classes etc. can work with **any type** — yet still enforce type safety.

---

### ✅ Syntax

```ts
function identity<T>(value: T): T {
  return value;
}

identity<number>(5);       // 👈 type T is number
identity<string>("hello"); // 👈 type T is string
```

- `T` is a **generic type parameter**
    
- It can be anything: `T`, `U`, `K`, `V`, etc.
    

---

### 📦 Why Use Generics?

|Feature|Benefit|
|---|---|
|🧠 Reusability|Write one function/interface that works for many types|
|✅ Type safety|Prevents `any` type usage while staying flexible|
|💡 IntelliSense|IDE can infer types based on usage|

---

## 🚀 Scenario-Based Example

### 🧾 Scenario: Reusable Array Wrapper

#### ❌ Without Generics:

```ts
function wrapInArray(value: any): any[] {
  return [value];
}

const result = wrapInArray(10); // ❌ result: any[]
```

#### ✅ With Generics:

```ts
function wrapInArray<T>(value: T): T[] {
  return [value];
}

const result = wrapInArray<number>(10); // ✅ result: number[]
```

Now you get autocomplete, type checks, and it's reusable!

---

### 🧱 Generic Interface Example

```ts
interface ApiResponse<T> {
  data: T;
  success: boolean;
}

const userResponse: ApiResponse<{ name: string }> = {
  data: { name: "Somnath" },
  success: true,
};
```

---

### 🧠 Mnemonic to Remember

> Think of **Generic** as **"Give me type later!"**  
> Like a function but for **types**.

---

### 📌 Common Patterns You Should Know

#### 1. **Generic Constraints**

```ts
function logLength<T extends { length: number }>(arg: T): void {
  console.log(arg.length);
}

logLength("hello"); // ✅ Works
logLength([1, 2, 3]); // ✅ Works
logLength(123); // ❌ Error
```

`T extends Something` → restricts what type `T` can be.

---

#### 2. **Using `keyof` with Generics**

```ts
function getProp<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

getProp({ name: "Roy", age: 28 }, "name"); // ✅ returns string
```

Powerful for accessing object keys with type safety.

---

## ✅ Summary Table

|Concept|Example|Meaning|
|---|---|---|
|Generic Function|`function echo<T>(x: T): T`|Type-safe reusable function|
|Generic Interface|`interface Box<T>`|Parameterize a structure|
|Constraints|`T extends Lengthwise`|Limit what types are allowed|
|`keyof` Usage|`K extends keyof T`|Safe property access|

---

## ❓Interview Questions (with mental cues)

> 🧠 “Why do we use generics in TypeScript?”  
> ✔️ _To create reusable code while maintaining type safety._

> 🧠 “What is `T extends U`?”  
> ✔️ _It restricts the type `T` to only those that extend `U` (i.e., must have the same shape or more)._

> 🧠 “Can you show me a function that returns one of the object’s properties using generics?”  
> ✔️ Use `K extends keyof T` and return `T[K]`.

---

The function that return any[]
You're absolutely right again — ✅ **The code will execute perfectly fine at runtime**.

But here’s the **important distinction**:

---

## ✅ Code Status

|Type|Result|
|---|---|
|**Runtime**|✅ Works fine — `wrapInArray(10)` returns `[10]`|
|**TypeScript (Design Time)**|❌ Loses type info — Type is `any[]`, not `number[]`|

---

## 🔍 So Is It “Wrong”?

- **Not wrong for runtime.**
    
- ✅ Perfectly valid **JavaScript-compatible code**.
    
- ❌ But **"wrong" in the context of TypeScript's type safety goals**.
    

---

### 🔥 Analogy

> It’s like driving a car without seatbelts — the car runs fine, but you're not protected.

- Using `any` disables **type safety**
    
- Using `T` keeps TypeScript helpful (autocomplete, error checking, etc.)
    

---

## 🧠 Remember This

> ✅ **Valid JavaScript**
> 
> ❌ **Poor TypeScript** — because `any` discards the type information that TypeScript was built to preserve

---

## Example: TypeScript Can't Help You with `any[]`

```ts
function wrapInArray(value: any): any[] {
  return [value];
}

const result = wrapInArray(10);
result[0].toUpperCase(); // ❌ No error now, but crashes at runtime!
```

`result[0]` is assumed to be `any`, so you can call `.toUpperCase()`  
But since it's actually a `number`, it crashes.

---

## ✅ With Generic: Safe & Smart

```ts
function wrapInArray<T>(value: T): T[] {
  return [value];
}

const result = wrapInArray(10);
result[0].toUpperCase(); // ❌ TypeScript Error: Property 'toUpperCase' does not exist on type 'number'
```

---

### ✅ TL;DR Summary

- `any`-based code **runs**, but loses type info = less safe
    
- Generics keep the code:
    
    - Reusable
        
    - Type-safe
        
    - Autocompletion-friendly
        
- Prefer generics in utility functions over `any`
    

---

Would you like a visual chart that compares `any` vs `T` for learning?
