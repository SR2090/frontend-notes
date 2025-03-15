
[[#Map method polyfill]]
## Map method polyfill


```js
/**

 * @template T, U

 * @param { (value: T, index: number, array: Array<T>) => U } callbackFn

 * @param {any} [thisArg]

 * @return {Array<U>}

 */

Array.prototype.myMap = function (callbackFn, thisArg) {

  // This arg will set the this value for the value.

  // this is the array on which we are going to execute

  const length = this.length;

  const newArray = new Array(length)

  for(let i = 0; i < length; i++) {

    // for sparse array

    if(Object.hasOwn(this, i)) {

      newArray[i] = callbackFn.call(thisArg, this[i], i, this);

    }

  }

  return newArray;

};
```

### Cases to consider for map 
- sparse arrays 
	- To solve use Object.hasOwn(this, k) it will ensure that the value returned is not undefined.
```js
const result = arr.myMap(function (value, index, array) {
  return value + index + array.length;
});
```
The callback function takes 3 argument which is why we need to provide them with the three values.



## Filter

```js
/**

 * @template T

 * @param { (value: T, index: number, array: Array<T>) => boolean } callbackFn

 * @param {any} [thisArg]

 * @return {Array<T>}

 */

Array.prototype.myFilter = function (callbackFn, thisArg) {

  const length = this.length;

  const result = [];

  for(let i = 0 ; i < length; i++) {

    if(Object.hasOwn(this, i)) {

        if(callbackFn.call(thisArg, this[i], i, this)) {

            result.push(this[i])

        }

    }

  }

  return result;

};
```

Remember the syntax for Object.hasOwn() and it is used to handle sparse arrays. As the keys won't be presented here for sparse arrays hence the function won't be executed.