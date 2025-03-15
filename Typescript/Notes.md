

## Index
[[#Benefits of using TS]]
[[#Configuration of typescript Compiler]]
[[#Problems with missing tsconfig]]
[[#Array methods]]
[[#Tuples]]
[[#Enums]]
[[#Functions]]
[[#Objects]]
[[#Union Types]]
[[#Intersection Type]]
[[#Nullable Types]]
## Benefits of using TS
1. Static Typing
2. Code completion
3. Refactoring
4. Shorthand notation



## Static Typing
- The type of variable is know during compile time, for dynamic typing the variable type can change during run time.
![[Pasted image 20250308090525.png]]
For the javascript example there is no way of knowing that the round method will be executed by the string type.


For typescript there is a compilation step involved, the code has to be converted into javascript. This process is called **Transpilation**



## Configuration of typescript Compiler

![[Pasted image 20250308092310.png]]
The compiled js standard, lower will target more browsers.

![[Pasted image 20250308093132.png]]
![[Pasted image 20250308093144.png]]
We can change the root directory using this configuration.
![[Pasted image 20250308093255.png]]
This will decide the output directory where the compiled javascript files will be stored.

![[Pasted image 20250308093326.png]]
This will prevent any ts file from compiling if any error has been detected.

Just using the tsc command will compile all ts files in project

![[Pasted image 20250308094353.png]]
Implicit any inferences will be highlighted by the compiler.

![[Pasted image 20250308100015.png]]
All params must be used by ts function

![[Pasted image 20250308101820.png]]

## Problems with missing tsconfig

![[Pasted image 20250308092908.png]]
![[Pasted image 20250308092928.png]]

![[Pasted image 20250308092937.png]]


## Debug TS 
1. Enable source map. This will determine how each line of typescript code map to the javascript code.


### Built in Types
![[Pasted image 20250308094143.png]]
Automatic type inference based on value of the variable


Level is any and it defeats the purpose of using ts due to it being assigned any value.

## Array 

![[Pasted image 20250308094740.png]]

## Tuples
Tuple array with 2 values![[Pasted image 20250308094728.png]]

## Enums
![[Pasted image 20250308094906.png]]
Ts compiler will automatically increment and assign the values.
For strings we need to specify the values ourselves.![[Pasted image 20250308094951.png]]

![[Pasted image 20250308095044.png]]
using const will make ts compiler generate more optimized code.

## Functions
Check taxYear for undefined

![[Pasted image 20250308101954.png]]
![[Pasted image 20250308103541.png]]

## Objects
![[Pasted image 20250308102245.png]]
Defining the structure
![[Pasted image 20250308102328.png]]



## Union Types
Any one of the defined types

## Intersection Type
Both of the defined types at the same time.
![[Pasted image 20250308102722.png]]




## Literal
![[Pasted image 20250308102930.png]]


## Nullable Types
![[Pasted image 20250308103221.png]]

![[Pasted image 20250308103252.png]]

Customer can be null or undefined so optional chaining operator similar to js.


