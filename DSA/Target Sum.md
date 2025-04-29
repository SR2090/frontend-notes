```js
const arr = [1,3,10,11,14];
// result 13 return possible index that will add up to this number
// will the array be sorted ? no then sort the array
// index i,j !== j,i 
const targetSum = 13;
const indexes = []
let startIdx = 0, endIdx = arr.length - 1;
// for(let i = 0 ; i < arr.length; i++) {
//     if(arr[startIdx] + arr[endIdx] > targetSum) {
//         endIdx -= 1;
//     }else if(arr[startIdx] + arr[endIdx] < targetSum){
//         startIdx += 1;
//     }else{
//         indexes.push([startIdx, endIdx]);
//         startIdx++;
//         endIdx--;
//     }
// }

while(startIdx < endIdx) {
     if(arr[startIdx] + arr[endIdx] > targetSum) {
        endIdx -= 1;
    }else if(arr[startIdx] + arr[endIdx] < targetSum){
        startIdx += 1;
    }else{
        indexes.push([startIdx, endIdx]);
        startIdx++;
        endIdx--;
    }
}
console.log(indexes)
```