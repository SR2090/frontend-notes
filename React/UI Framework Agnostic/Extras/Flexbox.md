
## Flex Grow

![[Pasted image 20241207230659.png]]

Flex grow determines how much free space should be used to place the items.
This is useful if the parent container is bigger than the total width of the child container. No free space then nothing to divide

Distribution of the free space that is specified in the first done on the basis of Flex grow value.

![[Pasted image 20241207231042.png]]

Because the flex grow is set to one the components original width of 170 has been overwritten by the browser and is set to 110 which will allow the free space to be equally divided between the elements.

This is ideally useful in situation where we want to grow our elements at different rates from one another.


![[Pasted image 20241207231208.png]]

In this third example A and B will grow to fill up the free space while C will stay at the original width


### Flex Shrink
![[Pasted image 20241207231334.png]]

This screenshot contains the algorithm for determining the shrinking of the flex items
This property specifies how much each child component will shrink if the parent component shrinks.


![[Pasted image 20241207231503.png]]
The combined width of these three children is more than the width of the container hence flexing must be utilized here to determine the width for each of the children.

## Flex Basis 
![[Pasted image 20241207232147.png]]
Between flex basis and width in a flex container flex basis will win.

If flex basis is set to 0 the browser does not consider the width of the content into account for calculating its placement inside the flex container.



## Flex Direction
![[Pasted image 20241207232852.png]]
