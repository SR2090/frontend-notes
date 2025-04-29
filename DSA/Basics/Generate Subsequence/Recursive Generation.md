Intuition: Take / Not take at any given idx

```js
/**

 * @param {number[]} nums

 * @return {number[][]}

 */

const recursive = (idx, ds, nums, result) =>  {

    // Base case

    if(idx >= nums.length) {

        result.push([...ds]);

        return;

    }

    // Take

    ds.push(nums[idx]);

    recursive(idx + 1, ds, nums, result);

    ds.pop()

  

    // Not take

    recursive(idx + 1, ds, nums, result);

}

var subsets = function(nums) {

    const result = [], ds = [];

    recursive(0 , ds, nums, result);

    // console.log(result);

    return result;

};
```
