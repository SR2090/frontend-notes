get keyword to define getter. 
- Using it you define a method. Method must return value.
- ![[Pasted image 20250418111914.png]]
- You cannot access the private properties

set keyword to define setter,
- Can be used to validate property value before assigning it actual value.
- Setter must have a mandatory single parameter that will use to assign to the corresponding property.
- ![[Pasted image 20250418112244.png]]
- ![[Pasted image 20250418112256.png]]
- ![[Pasted image 20250418112323.png]]
- We now have a first and last name property that we can now assign.


Why use setter when can define a constructor and provide validation there for value before assigning it.

**Clarifying constructor vs setter usage**

The user asks why use setters when validation can be performed in the constructor. The reason is typically flexibility: setters allow property values to change after object construction, while constructor validation runs only once. Using setters also helps with frameworks and libraries that require property-based validation or object instantiation without constructors. This is critical in cases like data-binding, serialization, or when dealing with mutable vs immutable objects. In languages like Java, setters are essential for DTOs and JavaBeans-based frameworks.

Thought for 11 seconds

### Short answer

Use **constructor validation** for values that must be correct **once, at birth**; use a **setter** (or no‑setter) based on whether the field is allowed to change later. A setter lets you (and frameworks) update the field safely every time it changes, not just the first time.

---

## Why a constructor alone is often not enough

|Need|How a constructor helps|Why a setter is still useful / may be preferable|
|---|---|---|
|**Mutability after creation**|Ensures the _initial_ value is valid.|As soon as the value must change (user edits a form, entity is patched via API, etc.) you need the same validation again. A validated setter gives you that single point of truth.|
|**Framework/deserializer support**|If you _always_ pass arguments, a full constructor is fine.|Many libraries (Hibernate, Jackson, JAXB, Spring, Java‑FX, Jakarta Bean Validation …) instantiate objects with a **no‑arg constructor** and then call setters via reflection. Without setters the object would stay un‑populated or invalid.|
|**Different life‑cycle phases**|Construction and use are one shot.|Some objects are built incrementally (Builder pattern, dependency injection, UI data‑binding). Each step may need its own validation. Private or package‑private setters (or `withX` methods) allow this while still shielding direct field access.|
|**Re‑validation of dependent state**|Simple state is easy to lock down.|When field A’s change affects invariants that involve field B, you want the update logic in A’s setter to keep the whole object consistent.|
|**Logging, events, lazy work**|Constructor can log, but only once.|A setter can hook in extra behaviour—emit an event, update a cache, mark a JPA entity as dirty, recalculate a derived field—every time the value changes.|

---

## Typical patterns in Java (similar ideas apply in C#, TypeScript, etc.)

```java
public final class Person {
    private int age;          // mutable
    private final String ssn; // immutable

    public Person(String ssn, int age) {
        this.ssn = Objects.requireNonNull(ssn, "ssn");
        setAge(age);          // reuse validation logic
    }

    public int getAge() { return age; }

    public void setAge(int age) {
        if (age < 0) throw new IllegalArgumentException("Age cannot be negative");
        this.age = age;
    }
}
```

- **Immutable data** → leave out the setter and make the field `final`. Validation belongs only in the constructor or in a `static factory`/`Builder`.
    
- **Mutable field** → centralise the rule in the setter, and _call the setter from the constructor_ to avoid duplication.
    

---

## When you _don’t_ need setters

- The class is **truly immutable** (value objects, DTOs used only for reads, etc.).
    
- You prefer **constructor or builder injection** everywhere and none of your tooling requires property access.
    
- The field is derived (`getFullName()` from `first` + `last`) or can be recalculated internally.
    

In those cases, skip the setter—immutability simplifies reasoning and thread‑safety.

---

### Take‑away guideline

1. **Can the value ever change after construction?**  
    _No_ → validate once in the constructor (or builder) and omit a setter.  
    _Yes_ → give the field a validated setter and call that setter inside the constructor.
    
2. **Will frameworks need to mutate or hydrate this object?**  
    If so, follow their contract (no‑arg constructor + setters).
    

By answering those two questions per field you’ll decide confidently whether a setter adds real value beyond the constructor.