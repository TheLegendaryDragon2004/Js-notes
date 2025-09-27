# Function Borrowing in JavaScript (`call`, `apply`, `bind`)

In JavaScript, functions are **first-class objects**, which means they can be stored in variables, passed as arguments, and even borrowed by other objects.  

To explicitly control what `this` points to inside a function, we use **`call`**, **`apply`**, and **`bind`**.

---

## Example Setup

```js
let name = {
    firstName: "Hari",
    lastName: "Vinayak",
    printName : function() {
        console.log(this.firstName + " " + this.lastName);
    }
};

name.printName();  
// Output -> Hari Vinayak
```

### 📝 Explanation
- Here, `printName` is a **method** of the object `name`.  
- When called as `name.printName()`, the value of `this` inside the function refers to `name`.  
- So it correctly prints `Hari Vinayak`.

---

Suppose we have another object:

```js
let name2 = {
    firstName: "Sachin",
    lastName: "Tendulkar",
};
```

We want to reuse the `printName` method for `name2` without copying it. That’s where `call`, `apply`, and `bind` come in.

---

## 1. `call()`

- **Syntax**:  
  ```js
  function.call(thisArg, arg1, arg2, ...)
  ```
- Executes the function **immediately**.  
- Pass arguments **individually** (comma-separated).  

```js
name.printName.call(name2);
// Output -> Sachin Tendulkar
```

### 📝 Explanation
- We "borrowed" `printName` from `name` and used it for `name2`.  
- Inside the function, `this` now points to `name2`.  
- Therefore it prints `Sachin Tendulkar` instead of `Hari Vinayak`.

---

With extra parameters:

```js
let printName2 = function(hometown, state) {
    console.log(this.firstName + " " + this.lastName + " " + state + " " + hometown);
};

printName2.call(name2, "Mumbai", "Kerala");
// Output -> Sachin Tendulkar Kerala Mumbai
```

### 📝 Explanation
- We defined a **standalone function** `printName2` (not attached to any object).  
- By default, if you call it normally (`printName2()`), `this` would be `undefined` (in strict mode) or the global object.  
- Using `call`, we set `this` to `name2`.  
- Arguments `"Mumbai"` and `"Kerala"` are passed **individually**.  
- The output order depends on how we arranged the concatenation inside the function.

---

## 2. `apply()`

- **Syntax**:  
  ```js
  function.apply(thisArg, [argsArray])
  ```
- Executes the function **immediately**.  
- Pass arguments **as an array** (or array-like object).  

```js
printName2.apply(name2, ["Mumbai", "Kerala"]);
// Output -> Sachin Tendulkar Kerala Mumbai
```

### 📝 Explanation
- Just like `call`, `apply` sets the value of `this` to `name2`.  
- The only difference is **argument passing style**:
  - `call`: `arg1, arg2, arg3`  
  - `apply`: `[arg1, arg2, arg3]`  
- This makes `apply` useful when arguments are already in an array.  
- Both `call` and `apply` **invoke the function immediately**.

---

## 3. `bind()`

- **Syntax**:  
  ```js
  function.bind(thisArg, arg1, arg2, ...)
  ```
- Does **not** invoke the function immediately.  
- Returns a **new function** with the given `this` value and (optionally) preset arguments.  

```js
let x = printName2.bind(name2, "Mumbai", "Kerala");
x(); 
// Output -> Sachin Tendulkar Kerala Mumbai
```

### 📝 Explanation
- `bind` doesn’t execute right away. Instead, it returns a **copy** of the function with `this` permanently set to `name2`.  
- In this case, `x` is now a new function that "remembers" `name2` as its `this`.  
- When we later call `x()`, it executes with `this = name2` and the pre-filled arguments `"Mumbai"` and `"Kerala"`.  
- This is useful when you want to **delay execution** or **store a function for later use** with a specific context.

---

## ✅ Summary

| Method    | Executes Immediately? | How to Pass Arguments          | Returns |
|-----------|------------------------|--------------------------------|---------|
| **call**  | ✅ Yes                | Individually (`arg1, arg2`)   | Result of the function |
| **apply** | ✅ Yes                | As an array (`[arg1, arg2]`)  | Result of the function |
| **bind**  | ❌ No                 | Individually (`arg1, arg2`)   | New function |

- **`call`** → Use when you know arguments beforehand and want immediate execution.
- **`apply`** → Use when arguments are already in an array.  
- **`bind`** → Use when you want to create a new function to call later with a fixed `this`.

# 🔧 Custom Implementation of `bind()` (Polyfill)

Now let’s try writing our own versions of `bind` step by step.

---

### Example Setup

```js
let name = {
    fistName: "Hari",
    lastName: "Vianyak",
};

let printname = function() {
    console.log(this.fistName + " " + this.lastName);
};

let printname2 = function(age, state, country) {
    console.log(this.fistName + " " + this.lastName + " " + age + " " + country + " " + state);
};
```

---

## 1. Basic `mybind`

```js
Function.prototype.mybind = function(...args) {
    // this -> function being bound (e.g., printname)
    let obj = this;
    return function() {
        obj.call(args[0]);
    };
};

let x = printname.mybind(name);
x(); 
// Output -> Hari Vianyak
```

### 📝 Explanation
- `mybind` takes the target object as the first argument (`args[0]`).  
- We store the original function (`this`) in `obj`.
- wont work if we dont use obj and call this directly because inside.mybind this points to function(fucntion.mybind and fucntion is an object)
  but inside returned function it will be window
- The returned function calls `obj.call(args[0])`, setting `this` to the provided object.  
- Works fine, but it **ignores extra arguments**.

---

## 2. Improved `mybind2` (support preset arguments)

```js
Function.prototype.mybind2 = function(...args) {
    let obj = this;
    let params = args.slice(1); // arguments after 'thisArg'
    return function() {
        obj.apply(args[0], params);
    };
};

let x2 = printname2.mybind2(name, 5, "india", "kerala");
x2(); 
// Output -> Hari Vianyak 5 india kerala
```

### 📝 Explanation
- Here we capture **preset arguments** (`params`).  
- When the returned function is called, we invoke the original with `apply`, passing `args[0]` as `this` and `params` as arguments.  
- Limitation: This version does **not allow passing extra arguments later**.

---

## 3. Final `mybind3` (full polyfill-like behavior)

```js
Function.prototype.mybind3 = function(...args) {
    let obj = this;
    let params = args.slice(1);
    return function(...args2) {
        obj.apply(args[0], [...params, ...args2]);
    };
};

let x3 = printname2.mybind3(name, 5, "india");
x3("kerala");
// Output -> Hari Vianyak 5 india kerala
```

### 📝 Explanation
- `params` stores **preset arguments** (given at bind time).  
- The returned function also accepts **new arguments** (`args2`).  
- We combine both sets using the spread operator `[...]`.  
- Now `mybind3` behaves like the real `bind()`:
  - Binds `this`.  
  - Allows partial application (preset arguments).  
  - Accepts more arguments at call time.  

