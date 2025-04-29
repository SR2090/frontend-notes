Named Constant
## Basic (Just needed to know)
![[Pasted image 20250407124508.png]]
If you do not specify the values then we can use 0, 1, 2 etc instead of the Role.Guest



## In more detail
### **Enums in TypeScript**

Enums are a feature in TypeScript that allows you to define a set of named constants. They are a way to give **more friendly names** to sets of numeric or string values.

---

#### **Types of Enums:**

1. **Numeric Enums**
    
2. **String Enums**
    
3. **Heterogeneous Enums**
    
4. **Const Enums**
    
5. **Computed Enums**
    

---

### **1. Numeric Enums:**

The default type of enums where each member is assigned a numeric value.

#### **Syntax:**

```typescript
enum Status {
  Pending,     // 0
  InProgress,  // 1
  Completed    // 2
}

console.log(Status.Pending);    // Output: 0
console.log(Status[1]);         // Output: InProgress
```

**Auto-incremented Values:**

- The first value defaults to `0`.
    
- Subsequent values increment automatically.
    

**Custom Start Value:**

```typescript
enum Level {
  Low = 5,
  Medium,      // 6
  High         // 7
}
console.log(Level.Medium);      // Output: 6
```

---

### **2. String Enums:**

Enums where each member is explicitly assigned a string value.

#### **Syntax:**

```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT"
}

console.log(Direction.Up);     // Output: UP
console.log(Direction["Left"]); // Output: LEFT
```

**Use Case:**

- When you need **meaningful names** rather than numeric values.
    
- Commonly used for API responses or states.
    

---

### **3. Heterogeneous Enums:**

Mixing numeric and string values within the same enum. Generally not recommended for maintainability.

#### **Syntax:**

```typescript
enum Mixed {
  No = 0,
  Yes = "YES"
}

console.log(Mixed.No);   // Output: 0
console.log(Mixed.Yes);  // Output: YES
```

---

### **4. Const Enums:**

Enums that are **inlined** during compilation, reducing the size of the generated code. Use `const` before `enum`.

#### **Syntax:**

```typescript
const enum Color {
  Red,
  Green,
  Blue
}

let myColor: Color = Color.Green;
console.log(myColor);   // Output: 1 (at compile time)
```

**Advantages:**

- **Performance:** Values are inlined, no enum object at runtime.
    
- **Use Case:** When enum values are **not dynamically referenced**.
    

---

### **5. Computed Enums:**

Enums where values are computed based on expressions.

#### **Syntax:**

```typescript
enum FileAccess {
  None,                  // 0
  Read = 1 << 1,         // 2
  Write = 1 << 2,        // 4
  ReadWrite = Read | Write,  // 6
  All = 7                // Explicitly set
}

console.log(FileAccess.ReadWrite);  // Output: 6
```

**Use Case:**

- Useful when you need **bitwise operations**.
    
- Example: Defining **permission sets**.
    

---

### **Reverse Mapping:**

Available only for numeric enums.

#### **Example:**

```typescript
enum Animal {
  Dog = 1,
  Cat,
  Bird
}

console.log(Animal[2]);  // Output: Cat
console.log(Animal.Dog); // Output: 1
```

**Note:**

- String enums do **not support reverse mapping**.
    

---

### **Enum Usage Scenarios:**

1. **Status Indicators:**
    
    ```typescript
    enum TaskStatus {
      NotStarted,
      InProgress,
      Done
    }
    
    function printStatus(status: TaskStatus) {
      if (status === TaskStatus.Done) {
        console.log("Task is completed.");
      }
    }
    
    printStatus(TaskStatus.Done); // Output: Task is completed.
    ```
    
2. **User Roles:**
    
    ```typescript
    enum UserRole {
      Admin = "ADMIN",
      User = "USER",
      Guest = "GUEST"
    }
    
    function checkAccess(role: UserRole) {
      if (role === UserRole.Admin) {
        console.log("Full access granted.");
      } else {
        console.log("Limited access.");
      }
    }
    
    checkAccess(UserRole.Admin); // Output: Full access granted.
    ```
    
3. **Direction Handling:**
    
    ```typescript
    enum Direction {
      North,
      East,
      South,
      West
    }
    
    function move(dir: Direction) {
      switch (dir) {
        case Direction.North:
          console.log("Moving North");
          break;
        case Direction.East:
          console.log("Moving East");
          break;
        case Direction.South:
          console.log("Moving South");
          break;
        case Direction.West:
          console.log("Moving West");
          break;
      }
    }
    
    move(Direction.South); // Output: Moving South
    ```
    

---

### **Key Takeaways:**

- **Enums are ideal** for defining a set of **named constants**.
    
- **Numeric Enums:** Auto-incremented values starting from `0`.
    
- **String Enums:** Explicitly define string values.
    
- **Heterogeneous Enums:** Combination of numbers and strings (not recommended).
    
- **Const Enums:** Inline values to save memory.
    
- **Computed Enums:** Combine or calculate values.
    

---

### **Additional Questions:**

1. **What is the difference between `const enum` and a regular enum?**
    
2. **How can you use enums for bitwise operations effectively?**
    
3. **What are the benefits and drawbacks of using string enums over numeric enums?**
    
4. **Can you extend an existing enum in TypeScript?**
    
5. **What is the impact of reverse mapping on performance?**


