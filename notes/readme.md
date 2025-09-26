# Important things about js


=== checks refereences only

in used to check if propery valid or not

```js
const obj = { name: "Alice", age: 25 };

// Check if property exists
console.log("name" in obj); // true
console.log("age" in obj);  // true
console.log("gender" in obj); // false

// Inherited property
console.log("toString" in obj); // true, because it's in prototype

```
## Behaviour -2
```js
console.log(NaN === NaN);  // false
console.log(Number.isNaN(NaN)); // true
```
In JavaScript, NaN stands for Not-a-Number.
NaN is unique because it is not equal to anything, including itself.
Therefore, NaN === NaN returns false.
To correctly check if a value is NaN, use:
Number.isNaN(value) → returns true if value is NaN.

isNaN(value) → coerces the value to a number first, so sometimes gives unexpected results.

## Behaviour -1

```js
// Example 1: Non-number string
console.log(isNaN("hello"));        // true
console.log(Number.isNaN("hello")); // false

// Example 2: Numeric string
console.log(isNaN("123"));        // false
console.log(Number.isNaN("123")); // false

// Example 3: Actual NaN
console.log(isNaN(NaN));        // true
console.log(Number.isNaN(NaN)); // true
```
isNaN(value) first converts the value to a number.

"hello" → NaN → isNaN returns true
"123" → 123 → isNaN returns false
Number.isNaN(value) does not convert; it only returns true if the value is exactly NaN.

Key Points:

Use Number.isNaN() for reliable NaN checks.
Avoid isNaN() when the value might be a string or other type.
This is a common source of bugs in JS code.
## Behaviour 0
```js
function dog() {
   print("I am a dog.");
}
dog.sound = "Bark";
```
Nothing Happens cause functions treated as object in Javascript
## Behaviour 1  
```js
const obj1 = {first: 20, second: 30, first: 50};
```

Answer: {first: 50, second: 30}

Explanation: In JavaScript object literals, if you define a property key more than once, the last value assigned to that key will be its final value. The first declaration first: 20 is overwritten by the later declaration first: 50.

## Behaviour 2
```js
print(typeof(NaN));
```

Answer: Number

Explanation: NaN in Javascript is defined to be of type number despite its name(not a number).

## Behaviour 3
```js
const example = ({ a, b, c }) => {
 console.log(a, b, c);
};
example(0, 1, 2);
```

Answer: undefined undefined undefined

Explanation: The function expects an object with properties {a, b, c}. Passing individual numbers instead of an object causes all destructured values to default to undefined.

## Behaviour 4
```js
var a = Math.max();
var b = Math.min();
print(a);
print(b);
```

Answer: Infinity -Infinity

Explanation: The Math.max() method returns -Infinity by default and the Math.min() method returns Infinity value by default when passed without any parameters.

## Behaviour 5
```js
const set = new Set();
set.add(5);
set.add('Hello');
set.add({ name: 'Scaler' });
for (let item of set) {
 console.log(item + 6);
}
```

Answer: 11 Hello6 [Object]6

Explanation: First 2 numbers are added as integers, followed by string concatenation. Finally, since both are not of string type, JS stringifies both the object and the number and concatenates them. When an object is stringified it is read as [object Object] and then concatenated.

## Behaviour 6
```js
var a = "hello";
var sum = 0;
for(var i = 0; i < a.length; i++) {
   sum += (a[i] - 'a');
}
print(sum);
```

Answer: NaN

Explanation: In Javascript, the a[i] - ‘a’ is not typecasted to an integer type and hence the result is NaN. for behavior u want

```js
var a = "hello";
var sum = 0;
for(var i = 0; i < a.length; i++) {
    sum += a[i].charCodeAt(0) - 'a'.charCodeAt(0);
}
console.log(sum); // 37
```


## Behaviour 7
```js
function test(...args) {
 console.log(typeof args);
}
test(12);
```

Answer: Object

The …args parameter allows us to collect all remaining arguments into an array, and in Javascript typeof an array is an object.

## Behaviour 8
```js
var a = true + true + true * 3;
print(a)
```

Answer: 5

In JS, in arithemtic operations true is like 1

## Behaviour 9
```js
a = [1, 2, 3, 4, 5];
print(a.slice(2, 4));
```

Answer: 3 4

Explanation: JUST LIKE PYTHON




## Behaviour 10

When an operator’s value is NULL, the typeof returned by the unary operator is:

Answer: Object

Explanation: Legacy bug js
null actually primitive type

```js
console.log(typeof null);  // "object"
console.log(null === Object); // false
```

## Behaviour 11
```js
let value = "5";

switch(value) {
    case 5:
        console.log("Number 5");
        break;
    case "5":
        console.log("String 5");
        break;
    default:
        console.log("No match");
}
```
Answer: "String 5"


Explanation: The switch statement in JavaScript uses strict comparison (===).
It compares both value and type.
In this example:
value is a string "5". case 5 is a number → does not match. case "5" is a string → matches, so "String 5" is printed.

Always remember: switch does not perform type coercion like ==.

## Behaviour 12

```js
const obj = {name: "Alice", age: 25, greet: function() { console.log("Hi"); }};
const str = JSON.stringify(obj);
console.log(str);

```

Answer: {"name":"Alice","age":25}

Explanation: JSON.stringify() converts a JavaScript object or value into a JSON string.
Only enumerable properties are included; functions and undefined are ignored.
In this example: name and age are included. greet is a function → ignored.
Useful for sending data to APIs or storing objects as strings.

Object Serialization is the process in which an object or data structure is translated into a format suitable for transferral over a network, or storage

## Behaviour 13
```js
const obj = Object.create(null);

console.log(obj.toString);  // undefined
console.log(obj.hasOwnProperty); // undefined

obj.name = "Alice";
console.log(obj.name); // "Alice"
```

Answer: undefined
undefined
Alice

Explanation: Normally, objects in JavaScript inherit from Object.prototype, which provides methods like toString(), hasOwnProperty(), etc.
Using Object.create(null) creates an object without a prototype.
This object is completely "clean":
No inherited properties or methods.
Useful when you need a pure dictionary without any prototype pollution.
You can still add your own properties (e.g., obj.name = "Alice").

## Behaviour 14
```js
// Example in Node.js
const fs = require('fs');  // File system module
fs.writeFileSync('example.txt', 'Hello World');
```

```js
// Example in Browser
console.log(window.innerWidth); // width of browser window
document.getElementById('demo').innerText = "Hello";
```

Answer: Server-side JS objects interact with the server environment.
Examples include:
process → info about Node.js process
global → global object in Node.js
Buffer → binary data manipulation
fs → file system access

Can access files, databases, network, etc., which client-side JS cannot.

Objects may have methods specific to the server runtime.


Answer:Client-side JS objects interact with the browser environment.
Examples include:
window → global object in browsers
document → DOM manipulation
localStorage, sessionStorage → store data in browser

Can manipulate UI, DOM, cookies, etc., but cannot directly access files or server resources.

Objects are browser-specific.

## Behaviour 15

```js
// 1. Using console.log()
console.log("Hello World!");

// 2. Using alert()
alert("Hello World!");

// 3. Using document.write()
document.write("Hello World!");

// 4. Using innerHTML to display in HTML element
document.getElementById("demo").innerHTML = "Hello World!";

```

Answer: NaN

Explanation: JavaScript provides multiple ways to display data:

console.log() → prints data to the browser console (for debugging).
alert() → shows a popup dialog to the user.
document.write() → writes directly to the HTML document (not recommended for modern apps).
innerHTML → modifies content inside HTML elements dynamically.(it can be used for any html tag with content)

## Behaviour 16

```js
// 1. Using getElementById()
let element1 = document.getElementById("demo");
element1.innerHTML = "Hello using getElementById";

// 2. Using getElementsByClassName()
let elements = document.getElementsByClassName("myClass");
elements[0].innerHTML = "Hello using getElementsByClassName";
```

document.getElementById(id) → returns a single element with the specified id.
document.getElementsByClassName(className) → returns a live HTMLCollection of all elements with the specified class.

## Behaviour 17
```html
<noscript>
    <p>Please enable JavaScript to view this content.</p>
</noscript>

<script>
    console.log("JavaScript is enabled!");
</script>
```

Answer: noscipt tag used for non JS browsers

In JS, in arithemtic operations true is like 1

## Behaviour 18
```js
// Example: Print a message every 2 seconds
let count = 0;
const intervalId = setInterval(() => {
    console.log("Hello! Count: " + count);
    count++;
    if (count === 5) {
        clearInterval(intervalId); // Stop the interval after 5 times
    }
}, 2000);

```

setInterval(callback, delay) repeatedly executes the callback function every delay milliseconds.
Returns an interval ID that can be used to stop the timer with clearInterval().
Common use cases:

Repeatedly update UI elements (e.g., clock, slideshow).

Polling server or API.

Animations in combination with DOM manipulation



## Behaviour 19
```js
// Class Example
class Person {
    constructor(name) {
        this.name = name;
    }
    greet() {
        console.log(`Hello, I am ${this.name}`);
    }
}

const p1 = new Person("Alice");
p1.greet(); // Hello, I am Alice

// Prototype Example
Person.prototype.sayBye = function() {
    console.log(`Goodbye from ${this.name}`);
};
p1.sayBye(); // Goodbye from Alice

// Extensible flag
console.log(Object.isExtensible(p1)); // true
Object.preventExtensions(p1);
console.log(Object.isExtensible(p1)); // false

// Trying to add a new property
p1.age = 25; 
console.log(p1.age); // undefined (cannot add new property)
```

Class – ES6 feature to create objects and define methods.
Internally, classes are syntactic sugar over constructor functions and prototypes.

Prototype – Every function in JS has a prototype property; objects inherit properties/methods via the prototype chain.
Methods defined on Person.prototype are shared across all instances.

Extensible Flag – Determines if new properties can be added to an object.
Object.isExtensible(obj) → check if object is extensible.
Object.preventExtensions(obj) → prevent adding new properties.
Existing properties can still be modified unless they are read-only.

## Behaviour 20

```js
// Number Example
const number = 1234567.89;
console.log(number.toLocaleString("en-US")); // "1,234,567.89"
console.log(number.toLocaleString("de-DE")); // "1.234.567,89"

// Date Example
const date = new Date("2025-09-26T12:30:00");
console.log(date.toLocaleString("en-US")); // "9/26/2025, 12:30:00 PM"
console.log(date.toLocaleString("de-DE")); // "26.9.2025, 12:30:00"

```


Explanation: 
toLocaleString() converts a Number or Date object to a string formatted according to the local conventions.
You can pass a locale code (like "en-US" or "de-DE") to format it for different regions.
Useful for displaying numbers and dates according to user’s locale.
Key Points:

Works on Number, Date, and Array objects.

Optional parameters allow currency formatting, decimal digits, and time zones.

Default locale is usually the environment's locale if none is provided.

## Behaviour 21

```js
// 1. Spread Operator: Expanding arrays
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// 2. Spread Operator: Expanding objects
const obj1 = {a: 1, b: 2};
const obj2 = {c: 3, d: 4};
const merged = {...obj1, ...obj2};
console.log(merged); // {a:1, b:2, c:3, d:4}

// 3. Rest Operator: Collecting function arguments
function sum(...numbers) {
    return numbers.reduce((acc, val) => acc + val, 0);
}
console.log(sum(1, 2, 3, 4)); // 10

```


Explanation: The ... operator has two main uses: spread and rest.

Spread (...)
Expands arrays or objects into individual elements or properties.
Useful for copying, merging, or passing multiple arguments.

Rest (...)
Collects multiple function arguments into a single array.
Useful for variadic functions (functions accepting any number of arguments).

## Behaviour 22
```js
var a = "hello";
var sum = 0;
for(var i = 0; i < a.length; i++) {
   sum += (a[i] - 'a');
}
print(sum);
```

Answer: NaN

Explanation: In Javascript, the a[i] - ‘a’ is not typecasted to an integer type and hence the result is NaN. for behavior u want

```js
var a = "hello";
var sum = 0;
for(var i = 0; i < a.length; i++) {
    sum += a[i].charCodeAt(0) - 'a'.charCodeAt(0);
}
console.log(sum); // 37
```


## Behaviour 7
```js
function test(...args) {
 console.log(typeof args);
}
test(12);
```

Answer: Object

The …args parameter allows us to collect all remaining arguments into an array, and in Javascript typeof an array is an object.

## Behaviour 8
```js
var a = true + true + true * 3;
print(a)
```

Answer: 5

In JS, in arithemtic operations true is like 1

## Behaviour 9
```js
a = [1, 2, 3, 4, 5];
print(a.slice(2, 4));
```

Answer: 3 4

Explanation: JUST LIKE PYTHON




## Behaviour 10

When an operator’s value is NULL, the typeof returned by the unary operator is:

Answer: Object

Explanation: Legacy bug js
null actually primitive type

```js
console.log(typeof null);  // "object"
console.log(null === Object); // false
```

## Behaviour 11
```js
let value = "5";

switch(value) {
    case 5:
        console.log("Number 5");
        break;
    case "5":
        console.log("String 5");
        break;
    default:
        console.log("No match");
}
```
Answer: "String 5"


Explanation: The switch statement in JavaScript uses strict comparison (===).
It compares both value and type.
In this example:
value is a string "5". case 5 is a number → does not match. case "5" is a string → matches, so "String 5" is printed.

Always remember: switch does not perform type coercion like ==.

## Behaviour 12

```js
const obj = {name: "Alice", age: 25, greet: function() { console.log("Hi"); }};
const str = JSON.stringify(obj);
console.log(str);

```

Answer: {"name":"Alice","age":25}

Explanation: JSON.stringify() converts a JavaScript object or value into a JSON string.
Only enumerable properties are included; functions and undefined are ignored.
In this example: name and age are included. greet is a function → ignored.
Useful for sending data to APIs or storing objects as strings.

## Behaviour 13
```js
const obj = Object.create(null);

console.log(obj.toString);  // undefined
console.log(obj.hasOwnProperty); // undefined

obj.name = "Alice";
console.log(obj.name); // "Alice"
```

Answer: undefined
undefined
Alice

Explanation: Normally, objects in JavaScript inherit from Object.prototype, which provides methods like toString(), hasOwnProperty(), etc.
Using Object.create(null) creates an object without a prototype.
This object is completely "clean":
No inherited properties or methods.
Useful when you need a pure dictionary without any prototype pollution.
You can still add your own properties (e.g., obj.name = "Alice").

## Behaviour 14
```js
// Example in Node.js
const fs = require('fs');  // File system module
fs.writeFileSync('example.txt', 'Hello World');
```

```js
// Example in Browser
console.log(window.innerWidth); // width of browser window
document.getElementById('demo').innerText = "Hello";
```

Answer: Server-side JS objects interact with the server environment.
Examples include:
process → info about Node.js process
global → global object in Node.js
Buffer → binary data manipulation
fs → file system access

Can access files, databases, network, etc., which client-side JS cannot.

Objects may have methods specific to the server runtime.


Answer:Client-side JS objects interact with the browser environment.
Examples include:
window → global object in browsers
document → DOM manipulation
localStorage, sessionStorage → store data in browser

Can manipulate UI, DOM, cookies, etc., but cannot directly access files or server resources.

Objects are browser-specific.

## Behaviour 15

```js
// 1. Using console.log()
console.log("Hello World!");

// 2. Using alert()
alert("Hello World!");

// 3. Using document.write()
document.write("Hello World!");

// 4. Using innerHTML to display in HTML element
document.getElementById("demo").innerHTML = "Hello World!";

```

Answer: NaN

Explanation: JavaScript provides multiple ways to display data:

console.log() → prints data to the browser console (for debugging).
alert() → shows a popup dialog to the user.
document.write() → writes directly to the HTML document (not recommended for modern apps).
innerHTML → modifies content inside HTML elements dynamically.(it can be used for any html tag with content)

## Behaviour 16

```js
// 1. Using getElementById()
let element1 = document.getElementById("demo");
element1.innerHTML = "Hello using getElementById";

// 2. Using getElementsByClassName()
let elements = document.getElementsByClassName("myClass");
elements[0].innerHTML = "Hello using getElementsByClassName";
```

document.getElementById(id) → returns a single element with the specified id.
document.getElementsByClassName(className) → returns a live HTMLCollection of all elements with the specified class.

## Behaviour 17
```html
<noscript>
    <p>Please enable JavaScript to view this content.</p>
</noscript>

<script>
    console.log("JavaScript is enabled!");
</script>
```

Answer: noscipt tag used for non JS browsers

In JS, in arithemtic operations true is like 1

## Behaviour 18
```js
// Example: Print a message every 2 seconds
let count = 0;
const intervalId = setInterval(() => {
    console.log("Hello! Count: " + count);
    count++;
    if (count === 5) {
        clearInterval(intervalId); // Stop the interval after 5 times
    }
}, 2000);

```

setInterval(callback, delay) repeatedly executes the callback function every delay milliseconds.
Returns an interval ID that can be used to stop the timer with clearInterval().
Common use cases:

Repeatedly update UI elements (e.g., clock, slideshow).

Polling server or API.

Animations in combination with DOM manipulation






