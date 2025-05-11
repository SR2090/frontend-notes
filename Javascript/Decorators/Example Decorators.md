Class Decorator that overrides its parent method ^classdecoratoroverrideexample

```ts
function logger<T extends new (...args: any[]) => {}>(targetObject: T, context: ClassDecoratorContext) {

    console.log("Logger decorator");

    console.log(targetObject);

    console.log(context);

  

    return class extends targetObject {

        greet() {

            console.log("proniknut")

        }

    } as T

}

  

@logger

class Person {

    name = "Max";

  

    greet() {

        console.log("Hi i am " + this.name)

    }

}

  

const Max = new Person()

console.log(Max.greet())
```


Class based decorator for logging the object that gets created ^a5d7c2
```ts
function logger<T extends new (...args: any[]) => {}>(targetObject: T, context: ClassDecoratorContext) {

    console.log("Logger decorator");

    console.log(targetObject);

    console.log(context);

  

    return class extends targetObject {

        constructor(...args: any[]) {

            super(...args)

            console.log(this)

        }

    }

}

  

@logger

class Person {

    name = "Max";

    constructor(name?: string) {

        if (name) {

            this.name = name

        }

    }

    greet() {

        console.log("Hi i am " + this.name)

    }

}

  

const Max = new Person()

const jane = new Person("Jane")
```

![[Pasted image 20250420140254.png]]
class_1 represent anonymous class name that has been assigned by the JS engine



## Function Decorator example
[[Decorators in JavaScript#^functiondecoratorexample| Function decorator example to implement autobind]]