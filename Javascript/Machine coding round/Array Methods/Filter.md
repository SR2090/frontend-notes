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


```js
const users = [
  {
    id: 1,
    name: 'Alice',
    age: 28,
    address: {
      city: 'New York',
      zip: '10001'
    },
    hobbies: ['reading', 'cycling']
  },
  {
    id: 2,
    name: 'Bob',
    age: 34,
    address: {
      city: 'Los Angeles',
      zip: '90001'
    },
    hobbies: ['hiking', 'chess']
  },
  {
    id: 3,
    name: 'Charlie',
    age: 22,
    address: {
      city: 'Chicago',
      zip: '60601'
    },
    hobbies: ['gaming', 'music']
  }
];

const result = users.filter(({hobbies}) => hobbies.includes("chess"));
console.log(result);
```