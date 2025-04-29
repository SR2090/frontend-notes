```js
const originalPush = Array.prototype.push
Array.prototype.push = function (...args) {
    const result = originalPush.apply(this, args);
    if(this.onPush) {
        // if method is defined the call it with the arguments push was called
        this.onPush(args)
    }
    return result;
}

Array.prototype.setOnPushCb = function (callBackFunction) {
    if(typeof callBackFunction === "function") {
        this.onPush = callBackFunction
    }else{
        throw new Error("This is not a valid function")
    }
}

const array = []
array.setOnPushCb((item) => console.log(item));
array.push(1,2,3)
array.push(96)
console.log(array)
```

Why choose apply instead of call ?
apply should be used when the arguments provided are dynamic.
