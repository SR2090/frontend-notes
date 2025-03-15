
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