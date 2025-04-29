```js
export default function longestConsecutiveNumberSeq(numbers) {

    let count = 1;

    let result = 1;

    for(let i = 0 ; i < numbers?.length ; i++) {

        let current = numbers[i];

        count = 1

        while(numbers.includes(current + 1)) {

            current++;

            count++;

            result = Math.max(result, count)

        }

    }

    return result;

}
```


