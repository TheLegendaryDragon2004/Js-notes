```js
let arr = [40,50,60];
console.log(typeof arr);//object
```
arr is an array, but typeof returns "object" because arrays are technically objects in JavaScript.

```js
function k(){
    console.log("Kari");
}
console.log(typeof k);//function
console.log(typeof k());//Kari undefined
```
k is a function, so typeof k is "function".
Calling k() prints "Kari" and returns undefined, so typeof k() is "undefined".

```js
function l(){
    console.log("a");
    return "pARI";
}

console.log(typeof l());//a string
```
l() prints "a" and returns "pARI", so typeof l() is "string".
```js
var a ="Hari";
console.log(typeof a);//string
a=67;
console.log(typeof a);//number
a={name:"Hari",age:67};
console.log(typeof a);//object
a=[6,7,8];
console.log(typeof a);//object
```
Variables in JavaScript are dynamically typed. a can hold a string, number, object, or array. typeof reflects the current value's type.
```js
console.log(typeof null);//object historical bug
console.log(null == Object);//false
console.log(null === Object);//false
console.log(arr instanceof Object);//true
console.log(Array.isArray(arr));//true
```
typeof null is "object" (historical quirk).
null == Object is false.
Arrays are objects (instanceof Object is true).
Use Array.isArray() to reliably check for arrays.

```js
console.log(typeof NaN); // "number"
console.log(typeof Infinity); // "number"
let s = Symbol("id");
console.log(s);//Symbol(id)
console.log(typeof s); // "symbol"
```
NaN and Infinity are of type "number".
Symbol is a unique primitive type with "symbol" type.

```js
console.log(typeof {});   // "object"
console.log(typeof []);   // "object"
console.log(Array.isArray([])); // true ✅

//typeof can be used both as operator and function
console.log(typeof 5);          // "number"
console.log(typeof(5));         // "number" 
```
Objects and arrays are "object".
Arrays can be verified with Array.isArray().
typeof can be used as both an operator and function.



```js
//You get NaN when a numeric operation fails:
console.log(0 / 0);       // NaN
console.log(Math.sqrt(-1)); // NaN
console.log(parseInt("abc")); // NaN
console.log("a" * 2);     // NaN

//NaN not equal to itself
console.log(NaN === NaN); // false
console.log(NaN == NaN);  // false

//To check properly:

console.log(Number.isNaN(NaN)); // true
console.log(isNaN(NaN));        // true

//isNaN() does type coercion.

console.log(isNaN("abc"));     // true (string → NaN)
console.log(isNaN(undefined)); // true (undefined → NaN)
console.log(isNaN("123"));     // false (string → number 123)


console.log(Number.isNaN("abc")); // false
console.log(Number.isNaN("123")); //false
console.log(Number.isNaN(NaN));   // true
```
isNaN() converts values to numbers before checking, so "abc" and undefined are NaN.
Number.isNaN() is strict and returns true only for NaN.
```js
//Any comparison with NaN is false, except !=.
console.log(NaN != 5); // true
console.log(NaN > 5);  // false
console.log(NaN < 5);  // false
console.log(NaN >= 5); // false
console.log(NaN <= 5); // false
console.log(NaN == 5); // false
```




