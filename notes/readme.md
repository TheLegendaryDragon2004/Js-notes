


https://www.interviewbit.com/javascript-mcq/ 

# JavaScript Code Snippet Outputs – Summary

## 1. Duplicate Keys in Objects
```js
const obj1 = {first: 20, second: 30, first: 50};
console.log(obj1);
Output:

js
Copy code
{ first: 50, second: 30 }
Explanation:
When an object is declared with duplicate keys, the last value assigned to that key overrides previous values.

2. typeof(NaN)
js
Copy code
print(typeof(NaN));
Output:

js
Copy code
number
Explanation:
Even though NaN stands for Not a Number, its type in JavaScript is defined as "number".

3. Destructuring Function Parameters
js
Copy code
const example = ({ a, b, c }) => {
  console.log(a, b, c);
};
example(0, 1, 2);
Output:

js
Copy code
undefined undefined undefined
Explanation:
The function expects an object with properties {a, b, c}. Passing individual numbers instead of an object causes all destructured values to default to undefined.
