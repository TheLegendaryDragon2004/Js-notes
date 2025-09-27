
# JavaScript Conditionals and Logical Operators

## TRUTHY VALUES VS FALSY VALUES
In JavaScript, values are either **truthy** or **falsy** when evaluated in a boolean context.

**Falsy values (evaluate to false):**
- `false`
- `0`
- `-0`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

**Truthy values (evaluate to true):**
- `"0"`, `"false"`, `" "` (non-empty strings)
- `[]` (empty array)
- `{}` (empty object)
- `42` (non-zero numbers)
- `true`
- `function() {}`
## 1️⃣ if-else Statements

```js
let age = 20;

if (age >= 18) {
  console.log("Adult");
} else if (age >= 13) {
  console.log("Teenager");
} else {
  console.log("Child");
}
````

**Explanation:**

* `if` checks a condition.
* `else if` checks another condition if previous `if` failed.
* `else` runs if none of the conditions are true.

---

## 2️⃣ Logical AND (`&&`)

```js
let isLoggedIn = true;
let hasSubscription = true;

if (isLoggedIn && hasSubscription) {
  console.log("Access granted");
}
```

**Explanation:**

* `&&` returns **true only if both operands are true**.
* Can also be used for **short-circuit evaluation**:

```js
let user = null;
user && console.log(user.name); // won't run since user is null
```

---

## 3️⃣ Logical OR (`||`)

```js
let userName = "" || "Guest";
console.log(userName); // "Guest"
```

**Explanation:**

* `||` returns the **first truthy value**.
* Useful for **default values**.
* Can also short-circuit:

```js
let value = null;
let result = value || "Default";
console.log(result); // "Default"
```

---
## NULL corecion
```js
let value1 = null ?? "Default";
console.log(value1); // "Default"

let value2 = 0 ?? 42;
console.log(value2); // 0

conole.log(null ?? 42);42
console.log(null ?? NaN);NaN
cosnole.log(0 ?? null);0
```
Explanation:

just like or but it accepts left side if it not null immediatley, else check right side if it is not null accept it or accept null

Unlike ||, it does not treat 0 or "" as nullish.
## 4️⃣ Optional Chaining (`?.`)

```js
let person = { name: "Alice", address: { city: "NY" } };

console.log(person?.address?.city); // "NY"
console.log(person?.contact?.phone); // undefined
```

**Explanation:**

* Access nested properties safely.
* If any part of the chain is `null` or `undefined`, it **returns `undefined` instead of throwing an error**.

---

## 5️⃣ Ternary Operator (`? :`)

```js
let age = 17;
let status = age >= 18 ? "Adult" : "Minor";
console.log(status); // "Minor"
```

**Explanation:**

* Shorthand for `if-else`.
* Syntax: `condition ? exprIfTrue : exprIfFalse`.
* Can be **nested** for multiple conditions:

```js
let age = 15;
let stage = age >= 18 ? "Adult" : age >= 13 ? "Teenager" : "Child";
console.log(stage); // "Teenager"
```

---


```

