Here’s your content converted into proper Markdown (`.md`) format:

# 🔹 JavaScript `prototype`, `__proto__`, and Prototype Inheritance

## What is a `prototype`?

In JavaScript, a **`prototype` is an object** that is associated with every function (except arrow functions). It allows you to **attach properties and methods that can be shared by all instances** created using that function as a constructor.

Think of it as a **blueprint**: instead of copying methods to every object, you store them on the prototype so all instances can access them through the **prototype chain**.

---

JavaScript is **prototype-based**, which means:

* Objects inherit from other objects via the **prototype chain**.
* ES6 `class` syntax is just **syntactic sugar** over this system.

Understanding **`prototype` vs `__proto__`** is crucial for mastering inheritance.

---

## 1. `prototype` vs `__proto__`

| Feature   | `prototype`                                                          | `__proto__`                                                    |
| --------- | -------------------------------------------------------------------- | -------------------------------------------------------------- |
| Type      | Property of a **function**                                           | Property of an **object**                                      |
| Purpose   | Holds properties/methods **shared by instances** created using `new` | Points to the object that the current object **inherits from** |
| Access    | `FunctionName.prototype`                                             | `object.__proto__` or `Object.getPrototypeOf(object)`          |
| Settable? | Yes, can assign a new object to it                                   | Yes, can assign a new prototype (rare)                         |
| Used by   | JavaScript when **creating instances with `new`**                    | JavaScript **lookup mechanism** for property/method access     |

### 🔹 Key Points

1. Every function has a `prototype` object by default (except arrow functions).
2. Every object has a `__proto__` property (inherited from `Object`) that points to the prototype it inherits from.
3. When a function is used as a constructor (`new Func()`):
   * The created object’s `__proto__` is set to `Func.prototype`.
4. When looking up properties:
   * JS first checks the object itself → then `__proto__` → up the chain → `Object.prototype` → `null`.

---

## 2. Example: `prototype` vs `__proto__`

```js
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    console.log(`Hello, I am ${this.name}`);
};

let p = new Person("Hari");

console.log(p.__proto__ === Person.prototype); // true
console.log(Person.prototype.__proto__ === Object.prototype); // true
console.log(Object.prototype.__proto__); // null

p.greet(); // Hello, I am Hari
````

### 📝 Explanation

* `p.__proto__` → points to `Person.prototype`.
* `Person.prototype.__proto__` → points to `Object.prototype`.
* The chain ends at `Object.prototype.__proto__` → `null`.
* Method `greet` is not on `p` itself; JS **looks up the prototype chain**.

---

## 3. Adding methods to the prototype

```js
Person.prototype.sayBye = function() {
    console.log(`${this.name} says bye`);
};

p.sayBye(); // Hari says bye
```

* All existing and future instances of `Person` can use `sayBye`.
* Memory-efficient: the method is **shared**, not recreated per instance.

---

## 4. Constructor Functions and `prototype` Quirks

1. Changing the prototype **after creating instances**:

```js
function Person(name) { this.name = name; }
let p1 = new Person("A");

Person.prototype.sayHi = function() { console.log("Hi"); };
let p2 = new Person("B");

p1.sayHi(); // Works! Existing instance inherits new method
```

2. Replacing the prototype entirely:

```js
Person.prototype = { greet() { console.log("Hey"); } };

let p3 = new Person("C");
p1.greet(); // Error! p1 still points to old prototype
p3.greet(); // Works
```

✅ **Takeaway:** Changing the prototype object entirely breaks links for previous instances.

---

## 5. `__proto__` Details & Edge Cases

* `__proto__` is **just a reference** to the prototype object.
* You can set it manually:

```js
let obj1 = { a: 1 };
let obj2 = { b: 2 };

obj2.__proto__ = obj1;
console.log(obj2.a); // 1
```

* But modifying `__proto__` is **slow** and not recommended in performance-critical code.

* Use `Object.create()` instead:

```js
let animal = { eats: true };
let rabbit = Object.create(animal);
console.log(rabbit.eats); // true
```

---

## 6. Prototype Inheritance

### 6.1 Function Constructor Inheritance

```js
function Animal(type) { this.type = type; }
Animal.prototype.makeSound = function() { console.log(`${this.type} sound`); }

function Dog(name) { this.name = name; }
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() { console.log(`${this.name} barks`); }

let dog = new Dog("Rex");
dog.makeSound(); // Rex sound
dog.bark();      // Rex barks
```

* `Dog.prototype = Object.create(Animal.prototype)` → sets **prototype chain**.
* `dog.__proto__` → `Dog.prototype`.
* `Dog.prototype.__proto__` → `Animal.prototype`.
* `Animal.prototype.__proto__` → `Object.prototype`.

---

### 6.2 Object Literal Inheritance

```js
let vehicle = { wheels: 4 };
let car = Object.create(vehicle);
car.brand = "Tesla";

console.log(car.wheels); // 4
```

* `car` inherits `wheels` from `vehicle` via prototype.
* Clean and simple way to set up **single-level inheritance**.

---

## 7. Edge Cases & Quirks

1. **Arrow functions do not have a `prototype` property.**

```js
const foo = () => {};
console.log(foo.prototype); // undefined
```

2. **Primitives are auto-boxed when accessing methods.**

```js
let str = "hello";
console.log(str.toUpperCase()); // HELLO
```

* JS internally creates `new String(str)` temporarily.

3. **Overwriting prototype vs extending prototype**

```js
function A() {}
A.prototype.x = 1;

A.prototype = { y: 2 }; // breaks old instances
```

4. **`instanceof` operator**

```js
console.log(dog instanceof Dog); // true
console.log(dog instanceof Animal); // true
console.log(dog instanceof Object); // true
```

* Checks whether the prototype chain contains `constructor.prototype`.

5. **`Object.prototype` is the top of the chain**

* All objects eventually inherit from `Object.prototype`.
* Its `__proto__` is `null`.

6. **Circular prototype chain is not allowed**

```js
// Not allowed, will cause infinite loop
obj.__proto__ = obj;
```

---

## 8. Summary

* **`prototype`** → shared methods/properties for instances (function property).
* **`__proto__`** → reference to the prototype object an instance inherits from (object property).
* **Prototype chain** → used for **property/method lookup**.
* Use **Object.create()** for safe inheritance, or **constructor + prototype** for ES5-style OOP.
* Quirks:

  * Arrow functions: no `prototype`.
  * Overwriting prototype breaks old instances.
  * `__proto__` exists for lookup but not ideal for modification.
  * All objects ultimately link to `Object.prototype`.

---

### 🔹 Diagram (Prototype Chain)

```
dog
  __proto__ --> Dog.prototype
                    __proto__ --> Animal.prototype
                                         __proto__ --> Object.prototype
                                                              __proto__ --> null
```

```

This is ready to save as a `.md` file.  

If you want, I can **also add an ES6 `class` section showing how it maps to prototypes** in the same Markdown.  

Do you want me to add that?
```
