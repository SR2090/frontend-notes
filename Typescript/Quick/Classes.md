Adding property to classes is different in TS when compared to JS
We define them as class properties like in Java instead of in the constructor.


The constructor gets called when we call the method using new keyword.

Sample class definition defined by having 2 properties
![[Pasted image 20250418013603.png]]





Vanilla JS equivalent
![[Pasted image 20250418013656.png]]


### Alternative way to create classes
This way will omit the need to write class properties separately.

To define class properties implicitly use the public keyword in argument of your constructor.

Apart from creating the property for the class it will also assign the value that we pass as argument to the constructor. Even initial value can also be provided.

![[Pasted image 20250418014438.png]]


```js
const max = new User("")
```



### Access Modifier

Public and private are the two modifiers.
With private direct assignment to properties is not possible however such is the not the case for public.
![[Pasted image 20250418015401.png]]

These keyword determine how properties can be accessed outside of a class



#rememberjavascript
In javascript we can define private property using # symbol before the property name.
![[Pasted image 20250418015514.png]]

By default the properties are public. Omitting the property access modifier is not recommended otherwise typescript will lose the required boiler plate code it adds.