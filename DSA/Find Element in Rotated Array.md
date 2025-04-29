```js
/**

 * @param {number[]} numbers

 * @param {number} target

 * @return {number}

 */

function findPivot(arr) {

  // Pivot Index where the smalles element is located`

  let low = 0,

    high = arr.length - 1;

  while (low < high) {

    let mid = Math.floor((low + high) / 2);

    if (arr[mid] > arr[high]) {

      low = mid + 1;

    } else {

      high = mid;

    }

  }

  return low;

}

function BinSearch(arr, target, low, high) {

  let result = -1;

  while (low <= high) {

    let mid = Math.floor((low + high) / 2);

    if (arr[mid] === target) {

      return mid;

    } else if (arr[mid] > target) {

      high = mid - 1;

    } else {

      low = mid + 1;

    }

  }

  return result;

}

export default function findInRotatedArray(numbers, target) {

  let pivot = findPivot(numbers);

  console.log(pivot, target);

  let result = -1;

  let low = 0,

    high = numbers.length - 1;

  // correct portion of the array to search

  if (numbers[pivot] <= target && target <= numbers[high]) {

    result = BinSearch(numbers, target, pivot, high);

  } else {

    result = BinSearch(numbers, target, low, pivot - 1);

  }

  return result;

}
```
### Things to remember
- The pivotFindex method can return low or high because at the end just a single element will remain.
- We are using binary search because the array is sorted and the required TC is O(nLogn)

### Things to improve:
 No need to find the pivot index.