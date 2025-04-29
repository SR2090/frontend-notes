There are only two limitations:

1. The references can’t go in circles. JavaScript will throw an error if we try to assign `__proto__` in a circle.
2. The value of `__proto__` can be either an object or `null`. Other types are ignored.
![[Pasted image 20250409015521.png]]


![[Pasted image 20250409015934.png]]

The walk method is rabbit has not introduced a new method into this object. Its definition will be used.
![[Pasted image 20250409020007.png]]


For Accessor methods the case is different:
![[Pasted image 20250409020140.png]]

## Please remember
methods are shared, but the object state is not.
This means that prototype does not inherit the object state, this will always refer to the object that is present before the dot notation.
![[Pasted image 20250409021136.png]]
The line 21 is modifying the rabbit object state which is independent of the animal state.![[Pasted image 20250409021455.png]]

Inheritance only shares the method not the memory.


![[Pasted image 20250409021741.png]]

![[Pasted image 20250409021752.png]]
Object.hasOwnProperty will exclude the inherited properties of the object.

![[Pasted image 20250409021810.png]]

if enumerable is set to false then those method will not be displayed.
![[Pasted image 20250409021933.png]]


## Questions
![[Pasted image 20250409023006.png]]


![[Pasted image 20250409023019.png]]

![[Pasted image 20250409023026.png]]

