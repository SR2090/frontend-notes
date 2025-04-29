
### Recursive Solution
```js
/**

 * @param {Array<*|Array>} value

 * @return {Array}

 */

export default function flatten(value) {

  const result = []

  recursiveFlatten(result, value);

  return result;

}

  

function recursiveFlatten(result, a2F) {

  if(!a2F) return;

  for(let i of a2F) {

    if(Array.isArray(i)) {

      recursiveFlatten(result, i);

    }else{

      result?.push(i);

    }

  }

  return;

}
```


### Iterative

The unshift will spread the contents of the array at the start and the loop will continue iterating from that position which is the first item of the spread out array.


```js
/**

 * @param {Array<*|Array>} value

 * @return {Array}

 */

export default function flatten(value) {

  const res = []

  const copy = value.slice();

  

  while(copy.length) {

    const item = copy.shift();

    if(Array.isArray(item)) {

      copy.unshift(...item);

    }else{

      res.push(item);

    }

  }

  return res;

}
```

Using Reduce
```js
export default function flatten(value) {

  return value.reduce(

    (acc, curr) => acc.concat(Array.isArray(curr) ? flatten(curr) : curr),

    [],

  );

}
```

Modify current
```js
type ArrayValue = any | Array<ArrayValue>;

export default function flatten(value: Array<ArrayValue>): Array<any> {

  while (value.some(Array.isArray)) {

    value = [].concat(...value);

  }

  return value;

}
```