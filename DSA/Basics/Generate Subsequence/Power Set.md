![[Pasted image 20250331170543.png]]

Generate all of them using bit manipulation.

5 => 1 0 1
Bit index numbering goes from right to left
![[Pasted image 20250331170617.png]]
2 1 0 represent the bit indexing

Check if any given ith bit is set or not:

1 0 1
1 0 0


# Basic Concept
Check if any given ith bit is set or not 
![[Pasted image 20250331170931.png]]

You do and operation with a number with a bit set to 1 at that place and the resultant number if it has the one at that position will not be set to zero.

![[Pasted image 20250331171026.png]]

If not then the entire number becomes 0



generating a number with only the ith bit set
![[Pasted image 20250331171100.png]]
=> This is also equivalent to 2<sup>i</sup> 
![[Pasted image 20250331171129.png]]

This equation will determine if the ith bit is set.


# Generate Subsequence
- The number of subsequence generated will be equal to 2<sup>n</sup> where n is the length of the string
- ![[Pasted image 20250331171439.png]]
- ![[Pasted image 20250331171509.png]]


### Steps
1. Outer loop will run 2<sup>n</sup> times. It will also initialize a new sub string.
2. Inner loop will run from right to left idx.
3. In the inner loop check if the bit at the i<sup>th</sup> index is set if so then add it to sub string.
![[Pasted image 20250331171953.png]]


## Complexity
TC O(2<sup>n</sup>  * n)
Space O(1)