---
tags:
  - arraymethod
  - easymachinecoding
---
[[Filter method]]

The filter method returns a new array.
The filter method iterates over the length of the array it gets from this.length property and executes callbackFn to obtain new shallow copied array which contains those element for which the call back returns true.
Also, the callback function takes 3 argument array element, index, array. The thisArg is the object used to call the callback function.

```js
Array.prototype.myFilter = function (callbackFn, thisArg) {

  const length = this.length;

  const result = [];

  for(let i = 0 ; i < length; i++) {

    const currentElement = this[i];
	// hasOwn will check if the index i exists in the array
    if(Object.hasOwn(this, i) && callbackFn.call(thisArg, currentElement, i, this)) {

         result.push(currentElement)

    }

  }

  return result;
  
};
```