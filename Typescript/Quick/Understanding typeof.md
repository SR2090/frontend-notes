In js it tells us about the data type of object that it associates itself.

In typescript we can use it in several different ways such as if its a value that can change then it will infer that type to be string.


![[Pasted image 20250419163200.png]]
![[Pasted image 20250419163212.png]]
Since, the value here cannot be changed the inferred type is therefore limited to being constant only.



## Benefit of using typeof keyword

we can omit manually writing object type.
![[Pasted image 20250419163844.png]]
Example if we have the above object and we want to pass this object's type as argument to function parameter then we would need to define a type. Using typeof will prevent us from manually writing this type.
![[Pasted image 20250419164037.png]]

