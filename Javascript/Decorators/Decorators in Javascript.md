Meta programming feature => It means that this is some piece of code that will interact with other code to alter its behavior. 
![[Pasted image 20250419212934.png]]
Example decorator Length is used to add validation logic to that title value.

There are 2 types of decorators:
1. built in decorators
2. experimental decorators.![[Pasted image 20250419213343.png]]
### Types of decorators
The different types are ![[Pasted image 20250419213505.png]]


## What is a decorator ?
- its just a  function with a specific signature
To attach a decorator to a class we need to modify the class its the @Symbol
Ecma Script decorator will require 2 arguments

```ts
function logger(target: any, context: ClassDecoratorContext) {}

  

@logger

class Person {

    name = "Max";

  

    greet() {

        console.log("Hi i am " + this.name)

    }

}
```

target class to which we are going to attach the decorator.
context is the object with information about that thing.![[Pasted image 20250420132440.png]]

### Class Decorator Examples

[[Example Decorators#^classdecoratoroverrideexample | Class based decorator that overrides the parent greet method]]

[[Example Decorators#^a5d7c2| Class based decorator for logging the object that gets created ]]



### Method Decorators^methoddecorators

^82bf3a

![[Pasted image 20250420162336.png]]
Basic method decorator structure.

```ts
function autobind(target: (...args: any[]) => any, ctx: ClassMethodDecoratorContext) {

    console.log("Function Decorator")

    console.log(target);

    console.log(ctx)

}

  

@logger

class Person {

    name = "Max";

    constructor(name?: string) {

        if (name) {

            this.name = name

        }

    }

    @autobind

    greet() {

        console.log("Hi i am " + this.name)

    }

}

  

const Max = new Person()

const jane = new Person("Jane")
```
![[Pasted image 20250420162711.png]]

The problem we are solving with method decorator
consider the following code

```ts
const max = new Person("Max")
const greet = max.greet();
greet()
// undefined and error
```
The reason for this output is the this context is lost. The calling method in greet() is the global object that does not contain name property.
We can solve this by binding the greet method to the this object using in build bind so that it will not break the this mapping.

Example:
```ts
constructor() {
	this.greet = this.greet.bind(this)
}
```

To implement it through decorator we will use built in method called addInitializer![[Pasted image 20250420163638.png]]
In it we will get access to the newly created object using which we can access the method to which we can bind the this. ^functiondecoratorexample

```ts
function autobind(target: (...args: any[]) => any, ctx: ClassMethodDecoratorContext) {

    console.log("Function Decorator")

    console.log(target);

    console.log(ctx)

    ctx.addInitializer(function (this: any) {

        this[ctx.name] = this[ctx.name].bind(this)

    })

}

  

class Person {

    name = "Max";

    constructor(name?: string) {

        if (name) {

            this.name = name

        }

    }

    @autobind

    greet() {

        console.log("Hi i am " + this.name)

    }

}

  

const Max = new Person()

const greetMax = Max.greet;

greetMax();
```

![[Pasted image 20250420164056.png]]



#### Modify the original function
With method decorator we can return a new function replacing the original function which the decorator was applied. We can use this insight to perform additional functionality before executing our method.

Below code examples shows how we replaced the method
```ts
function autobind(target: (...args: any[]) => any, ctx: ClassMethodDecoratorContext) {

    console.log("Function Decorator")

    return function (this: any) {

        console.log("abe")

    }

}

  

class Person {

    name = "Max";

    constructor(name?: string) {

        if (name) {

            this.name = name

        }

    }

    @autobind

    greet() {

        console.log("Hi i am " + this.name)

    }

}

  

const Max = new Person()

const greetMax = Max.greet;

greetMax();
```



## Field Decorators^fieldecorator

^18ea52
When creating ECMA script field decorator the target will be undefined.

