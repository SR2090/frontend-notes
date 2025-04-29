```js
function getAllSubarrays(arr) {
  const subarrays = [];
  // Outer loop: choose the starting index of the subarray
  for (let start = 0; start < arr.length; start++) {
    // Inner loop: choose the ending index of the subarray
    for (let end = start; end < arr.length; end++) {
      // Slice from start to end (inclusive) to create the subarray
      const subarray = arr.slice(start, end + 1);
      subarrays.push(subarray);
    }
  }
  return subarrays;
}

```

[[Drawing Note File#^AZkEO5v96uOCLfb4aTPf5|GenerateAllSubarrayofAnarraybruteForce]]