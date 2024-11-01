![[Pasted image 20240929144539.png]]
- **`Object.create()` does not copy properties**:
    
    - `Object.create()` creates a new object with the specified object as its prototype. However, it does **not** copy the properties from the prototype to the new object. Instead, the properties are accessible via **prototype chain lookup**.
    - The object created (`personEnchanced`) doesn't have its own properties initially, so logging it shows an empty object `{}`.
- **Prototype properties are not shown directly**:
    
    - When you log `personEnchanced`, only its own properties are displayed, not the properties inherited from its prototype (`personPrototype`). The prototype properties are not part of the object's own properties, so they aren't shown in the direct output of the object.

## `Object.create()` Method

This method allows you to create a new object using an existing object as a prototype. The new object inherits properties and methods from the prototype object. It can be used when you need to create a new object with a specific prototype.

// Object.create() Method

const personPrototype = {

  greet() {

    console.log(

      `Hello, my name is ${this.name} and I'm ${this.age} years old.`,

    );

  },

};

const person = Object.create(personPrototype);

person.name = 'John';

person.age = 30;

person.greet(); // Output: Hello, my name is John and I'm 30 years old.

An object with a prototype can be created by doing `Object.create(null)`.Actually, an object created with Object.create(null) does not have a prototype. This means it doesn't inherit properties or methods from Object.prototype, making it a "pure" object with no inherited behavior.

Here’s an example:

javascript
Copy code
const obj = Object.create(null);

console.log(obj); // Output: {}

console.log(obj.toString); // Output: undefined
console.log(obj.hasOwnProperty); // Output: undefined
In contrast, objects created using {} or new Object() inherit from Object.prototype:

javascript
Copy code
const obj1 = {};
console.log(obj1.toString); // Output: function toString() { [native code] }

const obj2 = new Object();
console.log(obj2.toString); // Output: function toString() { [native code] }
Since Object.create(null) doesn't inherit from Object.prototype, it's often used when you want to create a truly "plain" object, such as for use as a dictionary/map where prototype properties like toString or hasOwnProperty might interfere with your data.