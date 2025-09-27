
# JavaScript Arrays, Objects, Destructuring, Rest & Spread

## Array Basics

```js
let arr = [10, 20, 30, 40];

console.log(arr[0]); // 10
console.log(arr.length); // 4

arr.push(50);   // Add at end
console.log(arr); // [10, 20, 30, 40, 50]

arr.pop();      // Remove from end
console.log(arr); // [10, 20, 30, 40]

arr.shift();    // Remove from start
console.log(arr); // [20, 30, 40]

arr.unshift(5); // Add at start
console.log(arr); // [5, 20, 30, 40]
````

**Explanation:**

* Arrays are zero-indexed.
* `push`/`pop` add/remove at the **end**.
* `shift`/`unshift` remove/add at the **start**.

---

## Object Basics

```js
let user = {
  name: "Alice",
  age: 25,
  city: "New York"
};

console.log(user.name);      // Alice
console.log(user["age"]);    // 25
console.log(user.age);       // 25

user.job = "Developer";      // Add property
delete user.city;            // Remove property
```

**Explanation:**

* Objects store key-value pairs.
* Access properties via dot `.` or bracket `[]`.
* Properties can be added or removed dynamically.

---

## Array Destructuring

```js
let numbers = [1, 2, 3, 4, 5, 6];

// Basic destructuring
let [a, b] = numbers;
console.log(a, b); // 1 2

// Skipping values
let [first, , third] = numbers;
console.log(first, third); // 1 3

let [first1, , , fourth, , sixth] = numbers;
console.log(first1, fourth, sixth); // 1 4 6

// Default values
let [x, y, z = 10] = [5, 6];
console.log(x, y, z); // 5 6 10
```

**Explanation:**

* Destructuring extracts values from arrays into variables.
* You can skip elements with commas and set default values.

---

## Object Destructuring

```js
let person = {
  name2: "Bob",
  age: 30,
  country: "USA"
};

// Basic destructuring
let { name2, age } = person;
console.log(name2, age); // Bob 30

// Rename variables
let { country: nation } = person;
console.log(nation); // USA
console.log(person.country); // USA
console.log(person.nation); // undefined

// Default values
let { job = "Unemployed" } = person;
console.log(job); // Unemployed
```

**Explanation:**

* You can extract object properties into variables.
* Rename variables or set default values for missing keys.

---

## Rest Operator (`...`)

```js
let [p, q, ...rest] = [10, 20, 30, 40, 50];
console.log(p, q); // 10 20
console.log(rest); // [30, 40, 50]

let student = { id: 1, name: "Eve", grade: "A" };
let { id, ...others } = student;
console.log(id);      // 1
console.log(others);  // { name: "Eve", grade: "A" }
```

**Explanation:**

* Collect remaining array elements or object properties into a new array/object.

---

## Spread Operator (`...`)

```js
let arr1 = [1, 2];
let arr2 = [3, 4];
let merged = [...arr1, ...arr2];
console.log(merged); // [1, 2, 3, 4]

let obj1 = { a: 1, b: 21 };
let obj2 = { b: 62, c: 3 };
let combined = { ...obj2, ...obj1 };
console.log(combined); // { b: 21, c: 3, a: 1 }

let obj11 = { a: 1, b: 21 };
let obj21 = { b: 62, c: 3 };
let combined2 = { ...obj11, ...obj21 };
console.log(combined2); // { a: 1, b: 62, c: 3 }
```

**Explanation:**

* Spread operator expands arrays or objects.
* For objects, **later properties override earlier ones** if keys duplicate.

---

## Duplicate Keys in Objects

```js
const obj234 = {a:5, a:6, b:5};
console.log(obj234); // { a:6, b:5 }

let obj2342 = {a:5, a:6, b:5};
console.log(obj2342); // { a:6, b:5 }
```

**Explanation:**

* If an object has **duplicate keys**, the **last value wins**.

