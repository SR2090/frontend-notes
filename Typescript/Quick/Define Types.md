![[Pasted image 20241005093614.png]]Use small first letter otherwise the type will corresponding to the object.

Complex Types strings
![[Pasted image 20241005093859.png]]

### Default Type
![[Pasted image 20241005093952.png]]
Any is the default type and allows any type to be assigned like in vanilla javascript.



### Object Type Definition:
- Specific to Ts allows us to define the type definition for an object. In line 35 the definition contains field with boolean.
 ![[Pasted image 20241005094150.png]]
- Building on it further if i want to create an array of person objects then i can use [] symbol with it.
- ![[Pasted image 20241005094312.png]]
#### Type inference
- If no type is specified then ts tries to infer the type meaning that we will be require to write less code.
- ![[Pasted image 20241005130828.png]]
- It's redundant as ts is already aware of it being string.


### Union Type
- Allow more than one type for the variable
- ![[Pasted image 20241005152023.png]]
- ![[Pasted image 20241005152035.png]]
- 