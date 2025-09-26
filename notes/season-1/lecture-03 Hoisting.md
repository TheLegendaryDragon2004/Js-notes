# Episode 3 : Hoisting in JavaScript (variables & functions)

- Let's observe the below code and it's explaination:

```js
getName(); // Namaste Javascript
console.log(x); // undefined
var x = 7;
function getName() {
  console.log("Namaste Javascript");
}
```

- It should have been an outright error in many other languages, as it is not possible to even access something which is not even created (defined) yet But in JS, We know that in memory creation phase it assigns undefined and puts the content of function to function's memory. And in execution, it then executes whatever is asked. Here, as execution goes line by line and not after compiling, it could only print undefined and nothing else. This phenomenon, is not an error. However, if we remove var x = 7; then it gives error. Uncaught ReferenceError: x is not defined

- **Hoisting** is a concept which enables us to extract values of variables and functions even before initialising/assigning value without getting error and this is happening due to the 1st phase (memory creation phase) of the Execution Context.

- So in previous lecture, we learnt that execution context gets created in two phase, so even before code execution, memory is created so in case of variable, it will be initialized as undefined while in case of function the whole function code is placed in the memory. Example:

```js
getName(); // Namaste JavaScript
console.log(x); // Uncaught Reference: x is not defined.
console.log(getName); // f getName(){ console.log("Namaste JavaScript); }
function getName() {
  console.log("Namaste JavaScript");
}
```

U need to note that for different environment like node it will show [Function: getName]

- Now let's observe a different example and try to understand the output.

```js
getName(); // Uncaught TypeError: getName is not a function because it is like undefined ()
console.log(getName);
var getName = function () {
  console.log("Namaste JavaScript");
};
// The code won't execute as the first line itself throws an TypeError.
```

<hr>

```js
console.log(getName);\\undefined
var getName = function () {
  console.log("Namaste JavaScript");
};
getname() \\works as expected 
```
```js
console.log(getName);\\not function
var getName = () => {
  console.log("Namaste JavaScript");
};
getname()
// The code won't execute as the first line itself throws an TypeError.
```

```js
console.log(x);
console.log(add(9,2));//11

var x = 0;
function add(a,b){
    return a + b;
}
console.log(add(5,2));//7
```
if arguments same logic only
```js
var add;  // hoisted, initialized as undefined

console.log(add);        // prints undefined
console.log(add(2, 3));  // calling undefined → TypeError
add = function (a, b) {  // now assignment happens
  return a + b;
};
console.log(add(2, 3));  // works now
```




**Special**
```js
var getName = function pari() {
  console.log("Namaste JavaScript");
};
```
This assigns a function object to getName.

The function has an internal name pari:

It’s only visible inside the function itself (for recursion or self-reference).

Outside, pari is not defined in the outer/global scope.


but it can be used for recusion 

```js
pari()\\error
console.log(getName);
var getName = function pari() {
  console.log("Namaste JavaScript");
  pari();
};
getName();
```
The above code will print namaste javascript endlessly


Watch Live On Youtube below:

<a href="https://www.youtube.com/watch?v=Fnlnw8uY6jo&ab_channel=AkshaySaini" target="_blank"><img src="https://img.youtube.com/vi/Fnlnw8uY6jo/0.jpg" width="750"
alt="Hoisting Youtube Link"/></a>
