# ECMASCRIPT 2023/2024

related links

-   [Clean Code JavaScript](https://github.com/FrontendEraspace/clean-code-javascript)
-   [Clean Code & Code Conventions Next.js](https://github.com/FrontendEraspace/clean-code-nextjs)

## 1. Object.groupBy()

```js
const inventory = [
    { name: "asparagus", type: "vegetables", quantity: 5 },
    { name: "bananas", type: "fruit", quantity: 0 },
    { name: "goat", type: "meat", quantity: 23 },
    { name: "cherries", type: "fruit", quantity: 5 },
    { name: "fish", type: "meat", quantity: 22 },
];
// groupBy key type
const result = Object.groupBy(inventory, ({ type }) => type);

/*
{
  vegetables: [
    { name: 'asparagus', type: 'vegetables', quantity: 5 },
  ],
  fruit: [
    { name: "bananas", type: "fruit", quantity: 0 },
    { name: "cherries", type: "fruit", quantity: 5 }
  ],
  meat: [
    { name: "goat", type: "meat", quantity: 23 },
    { name: "fish", type: "meat", quantity: 22 }
  ]
}
*/
```

```js
function myCallback({ quantity }) {
    return quantity > 5 ? "ok" : "restock";
}

const result2 = Object.groupBy(inventory, myCallback);

/*
{
  restock: [
    { name: "asparagus", type: "vegetables", quantity: 5 },
    { name: "bananas", type: "fruit", quantity: 0 },
    { name: "cherries", type: "fruit", quantity: 5 }
  ],
  ok: [
    { name: "goat", type: "meat", quantity: 23 },
    { name: "fish", type: "meat", quantity: 22 }
  ]
}
*/
```

## 2. toReversed()

reverse array tanpa mengubah array aslinya

```js
const items = [1, 2, 3];
console.log(items); // [1, 2, 3]

const reversedItems = items.toReversed();
console.log(reversedItems); // [3, 2, 1]
console.log(items); // [1, 2, 3]
```

## 3. toSorted()

Sama seperti toReversed(), toSorted() tidak mengubah original object

```js
const months = ["Mar", "Jan", "Feb", "Dec"];
const sortedMonths = months.toSorted();
console.log(sortedMonths); // ['Dec', 'Feb', 'Jan', 'Mar']
console.log(months); // ['Mar', 'Jan', 'Feb', 'Dec']

const values = [1, 10, 21, 2];
const sortedValues = values.toSorted((a, b) => a - b);
console.log(sortedValues); // [1, 2, 10, 21]
console.log(values); // [1, 10, 21, 2]
```

## 4. toSpliced()

```js
const months = ["Jan", "Mar", "Apr", "May"];

// Inserting an element at index 1
const months2 = months.toSpliced(1, 0, "Feb");
console.log(months2); // ["Jan", "Feb", "Mar", "Apr", "May"]

// Deleting two elements starting from index 2
const months3 = months2.toSpliced(2, 2);
console.log(months3); // ["Jan", "Feb", "May"]

// Replacing one element at index 1 with two new elements
const months4 = months3.toSpliced(1, 1, "Feb", "Mar");
console.log(months4); // ["Jan", "Feb", "Mar", "May"]

// Original array is not modified
console.log(months); // ["Jan", "Mar", "Apr", "May"]
```

## 5. Array.prototype.with()

membuat copy dari array dan replace value at given index

```js
const arr = [1, 2, 3, 4, 5];
console.log(arr.with(2, 6)); // [1, 2, 6, 4, 5]
console.log(arr); // [1, 2, 3, 4, 5]
```

## 6. Array.prototype.findLast()

```js
const array1 = [5, 12, 50, 130, 44];

const found = array1.findLast((element) => element > 45);

console.log(found);
// Expected output: 130
```

## 7. Array.prototype.findLastIndex()

```js
const array1 = [5, 12, 50, 130, 44];

const isLargeNumber = (element) => element > 45;

console.log(array1.findLastIndex(isLargeNumber));
// Expected output: 3
// Index of element with value: 130
```

## 8. Top-level await

using await outside async function

```js
const data = await fetchData();
console.log(data);
```

## 8. Array.prototype.at()

```js
const array1 = [5, 12, 8, 130, 44];

let index = 2;

console.log(`An index of ${index} returns ${array1.at(index)}`);
// Expected output: "An index of 2 returns 8"

index = -2;

console.log(`An index of ${index} returns ${array1.at(index)}`);
// Expected output: "An index of -2 returns 130"
```

## 9. Numeric Separators

Gunakan jika angka numeric terlalu besar digitnya agar lebih readable

```js
const price = 1_000_000;
```

## 10. Nullish Coalescing && Nullish Coalescing Assignment

return nilai sebelah kanan jika yang sebelah kiri null || undefined

```js
const foo = null ?? "default string";
console.log(foo);
// Expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// Expected output: 0

const a = { duration: 50 };

a.duration ??= 10;
console.log(a.duration);
// Expected output: 50

a.speed ??= 25;
console.log(a.speed);
// Expected output: 25
```

## 11. Object.hasOwn()

Cek apakah suatu object memiliki `key` tertentu

```js
const object1 = {
    prop: "exists",
};

console.log(Object.hasOwn(object1, "prop"));
// Expected output: true

console.log(Object.hasOwn(object1, "toString"));
// Expected output: false

console.log(Object.hasOwn(object1, "undeclaredPropertyValue"));
```

## 12. Static field & method

```js
class Test {
    static firstName = "test-static-name";

    static greeting() {
        console.log("Hello this is a greeting from a static method");
    }
}

Test.firstName;
// Output: test-static-name

Test.greeting();
// Output: Hello this is a greeting from a static method
```

## 13. Error cause

```js
const getUsers = async (array) => {
    try {
        const users = await fetch("https://myapi/users");
        return users;
    } catch (error) {
        console.log("enter");
        throw new Error("Something when wrong, please try again later", {
            cause: error, // pass error cause as 2nd param
        });
    }
};
```

## 14. Promise.any()

return satu promise manapun yang fulfilled

```js
const promise1 = Promise.reject(0);
const promise2 = new Promise((resolve) => setTimeout(resolve, 100, "quick"));
const promise3 = new Promise((resolve) => setTimeout(resolve, 500, "slow"));

const promises = [promise1, promise2, promise3];

Promise.any(promises).then((value) => console.log(value));

// Expected output: "quick"
```

## 15. String.prototype.replaceAll()

replace all occurences of matched string

```js
const paragraph = "I think Ruth's dog is cuter than your dog!";

console.log(paragraph.replaceAll("dog", "monkey"));
// Expected output: "I think Ruth's monkey is cuter than your monkey!"

// Global flag required when calling replaceAll with regex
const regex = /Dog/gi;
console.log(paragraph.replaceAll(regex, "ferret"));
// Expected output: "I think Ruth's ferret is cuter than your ferret!"
```

## 16. shebang

```js
#!/usr/bin/env node

console.log("hello");
```

run file js as script

```bash
./index.js
```

## 17. await import

```js
import { myData } from "./myData.js";
const data = await myData();
```

## 18. Optional Chaining

```js
const car = { type: "Fiat", model: "500", color: "white" };
let name = car?.name; // undefined
```

## 19. Object.fromEntries()

```js
const fruits = [
    ["apples", 300],
    ["pears", 900],
    ["bananas", 500],
];

const myObj = Object.fromEntries(fruits);
console.log(myObj);

/*
output: { apples: 300, pears: 900, bananas: 500 }
*/
```

## 20. BigInt

```js
let y = 9999999999999999; // 10000000000000000
let bigY = 9999999999999999n; // 9999999999999999n
```
