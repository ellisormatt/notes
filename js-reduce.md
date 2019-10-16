- Sum all values in the array using normal, expanded notation

```
const numbers = [1,2,3,4,5];

let sum = 0;

for (let n of numbers) {
        sum += n;
}

```
- Sum all values using reduce() method

```
console.log(sum);
*/

const numbers = [1,2,3,4,5];

// accumulator = 0, currentValue = 1 => accumulator = 1
// accumulator = 1, currentValue = 2 => accumulator = 3
// accumulator = 3, currentValue = 3 => accumulator = 6
// accumulator = 6, currentValue = 4 => accumulator = 10
// accumulator = 10, currentValue = 5 => accumulator = 15
const sum = numbers.reduce((accumulator,currentValue) => {
        return accumulator + currentValue;
}, 0);

console.log(sum);
```

Shortest hand I know of to write this

```
let sum = numbers.reduce((accumulator,currentValue) => accumulator+currentValue,0);
```
