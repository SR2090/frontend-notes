Below is an overview of 10 built‐in TypeScript types that you’ll often see used in React projects, along with simple examples for each.

---

### 1. **string**

Used for text data.

```tsx
const Greeting: React.FC = () => {
  const message: string = "Hello, React!";
  return <h1>{message}</h1>;
};
```

---

### 2. **number**

Used for numeric values.

```tsx
const Counter: React.FC = () => {
  const initialCount: number = 0;
  return <div>Count: {initialCount}</div>;
};
```

---

### 3. **boolean**

Used for true/false flags.

```tsx
const ToggleMessage: React.FC = () => {
  const isVisible: boolean = true;
  return <div>{isVisible ? "Visible" : "Hidden"}</div>;
};
```

---

### 4. **any**

Allows any type of value (use sparingly to keep type safety).

```tsx
const AnyComponent: React.FC = () => {
  const data: any = { id: 1, name: "Alice" };
  return <div>{data.name}</div>;
};
```

---

### 5. **unknown**

A safer alternative to `any` that forces type checking before use.

```tsx
const UnknownComponent: React.FC = () => {
  let value: unknown = "This is a string";
  if (typeof value === "string") {
    return <div>{value.toUpperCase()}</div>;
  }
  return <div>Not a string</div>;
};
```

---

### 6. **void**

Often used as the return type for functions that don’t return a value—like event handlers.

```tsx
const ClickHandler: React.FC = () => {
  const handleClick = (): void => {
    console.log("Button clicked!");
  };

  return <button onClick={handleClick}>Click me</button>;
};
```

---

### 7. **null**

Represents an intentional absence of any object value.

```tsx
const NullExample: React.FC = () => {
  const noValue: null = null;
  return <div>{noValue === null ? "No value available" : noValue}</div>;
};
```

---

### 8. **undefined**

Represents a variable that hasn’t been assigned a value.

```tsx
const UndefinedExample: React.FC = () => {
  let maybe: undefined = undefined;
  return <div>{maybe === undefined ? "Value is undefined" : maybe}</div>;
};
```

---

### 9. **object**

Used to denote non-primitive types.

```tsx
const ObjectExample: React.FC = () => {
  const user: object = { name: "Bob", age: 25 };
  // You might need to further type this when accessing properties.
  return <div>User object provided.</div>;
};
```

---

### 10. **never**

Indicates values that never occur (for example, functions that throw an error or infinite loops).

```tsx
const throwError = (message: string): never => {
  throw new Error(message);
};

const NeverExample: React.FC = () => {
  // Uncommenting the line below will throw an error
  // throwError("This is an error message!");
  return <div>never is used for functions that never return.</div>;
};
```

---

These examples illustrate how each built‐in type can be utilized in a React project using TypeScript. Using these types correctly helps ensure that your code is both robust and type-safe.



Vanilla JS only have types, we do not use explict type assignments.
## Type definition sytax
The type name always goes after the variable name
 