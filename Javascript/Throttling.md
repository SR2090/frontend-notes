```js
/**

 * @callback func

 * @param {number} wait

 * @return {Function}

 */

export default function throttle(func, wait) {

  let shouldThrottle = false;

  return function(...args) {

    if(shouldThrottle){

      return;

    }

    shouldThrottle = true;

    setTimeout(() => {

      shouldThrottle = false;

    }, wait);

    func.apply(this,args)  

  }

}
```

![[Pasted image 20250315135119.png]]

![[Pasted image 20250315135225.png]]

![[Pasted image 20250315135235.png]]

