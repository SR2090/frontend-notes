Consider a scenario where you know that you will store an object but do not know about the structure of the type.

It would be convenient if we had something that signifies such an object definition without the need to explicitly set the properties.


```ts
let data: Record<string, string | number>;
data = {
entry1: 1,
entry2: 'some string'
};
```



### **Record Type in TypeScript**

The `Record` type in TypeScript is a **utility type** that allows you to define an object type with a set of keys and the value type for each of those keys. It is particularly useful when you want to create an object whose keys are **known or constrained** but the values are of a specific type.

---

#### **Syntax:**

```typescript
Record<Keys, Type>
```

- **Keys:** Defines the set of allowed keys (often a union of string literals or a generic type).
    
- **Type:** Defines the type of the values associated with those keys.
    

---

#### **Common Use Cases:**

1. **Dynamic Object with Known Key Structure:**
    
    ```typescript
    let userRoles: Record<string, number>;
    userRoles = {
      admin: 1,
      editor: 2,
      viewer: 3,
    };
    ```
    
2. **Object with Specific Keys:**
    
    ```typescript
    type Role = 'admin' | 'editor' | 'viewer';
    let accessLevel: Record<Role, boolean>;
    accessLevel = {
      admin: true,
      editor: false,
      viewer: true,
    };
    ```
    
3. **Storing API Responses:**
    
    ```typescript
    interface User {
      id: number;
      name: string;
    }
    
    const users: Record<string, User> = {
      "user1": { id: 1, name: "Alice" },
      "user2": { id: 2, name: "Bob" },
    };
    ```
    
4. **Flexible Object Mapping:**
    
    ```typescript
    type Point = { x: number; y: number };
    let coordinates: Record<string, Point>;
    coordinates = {
      start: { x: 0, y: 0 },
      end: { x: 100, y: 100 },
    };
    ```
    

---

### **Why Use `Record` Type?**

1. **Ensures Consistency:**
    
    - Forces you to stick to a defined set of keys and value types.
        
2. **Dynamic Property Names:**
    
    - Useful when property names are not known at compile time.
        
3. **Code Clarity:**
    
    - Makes your code more readable by explicitly stating the structure.
        
4. **Type Safety:**
    
    - Reduces errors by enforcing type checks on both keys and values.
        

---

#### **Alternative to Record:**

You can use **index signatures** to achieve a similar outcome:

```typescript
let data: { [key: string]: string | number };
data = {
  entry1: 1,
  entry2: 'some string'
};
```

**Difference:**

- `Record<string, string | number>` and `{ [key: string]: string | number }` are functionally the same.
    
- `Record` is more expressive and often preferred for clarity.
    

---

### **Scenario-Based Example:**

#### **Scenario:**

You are developing a **configuration loader** for a web application. You don't know the exact structure of the configuration keys but know that the values will either be strings or numbers.

```typescript
type Config = Record<string, string | number>;

function loadConfig(): Config {
  return {
    appName: "MyApp",
    port: 3000,
    environment: "production",
  };
}

const config = loadConfig();
console.log(config.appName); // MyApp
console.log(config.port);    // 3000
```

---

### **Key Takeaways:**

- **`Record<K, T>`** is used when:
    
    - You have **dynamic object keys**.
        
    - You know the **value type**.
        
- Use `Record` when you need a **mapping of keys to values** where the keys are dynamic or known as a union.
    
- Provides **better code readability** compared to using an index signature.
    

---

### **Additional Questions:**

1. **What is the difference between `Record<string, any>` and `{ [key: string]: any }`?**
    
2. **Can you use `Record` with nested objects?**
    
3. **How does the `Record` type compare to other utility types like `Partial` and `Pick`?**


![[Pasted image 20250419123732.png]]
