# 🌐 JavaScript — Interview Questions & Answers

> Top JavaScript interview questions with theoretical answers and code examples.
> Source: [Intellipaat — JavaScript Interview Questions](https://intellipaat.com/blog/interview-question/javascript-interview-questions/)

---

## Basics & Core Concepts

### Q1. Is JavaScript Dynamic or Static?

JavaScript is a **dynamically typed** language — variable types are determined at runtime, not compile time.

```javascript
let x = 42; // Number
x = "hello"; // Now a String — no error!
x = true; // Now a Boolean
```

---

### Q2. Data Types in JavaScript

| Primitive Types               | Reference Types |
| ----------------------------- | --------------- |
| `string`, `number`, `boolean` | `Object`        |
| `undefined`, `null`           | `Array`         |
| `symbol`, `bigint`            | `Function`      |

```javascript
typeof "hello"; // "string"
typeof 42; // "number"
typeof true; // "boolean"
typeof undefined; // "undefined"
typeof null; // "object" (historical bug)
typeof {}; // "object"
typeof []; // "object"
typeof function () {}; // "function"
```

---

### Q3. var vs let vs const

| Feature   | `var`           | `let`     | `const`   |
| --------- | --------------- | --------- | --------- |
| Scope     | Function        | Block     | Block     |
| Hoisting  | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Reassign  | ✅              | ✅        | ❌        |
| Redeclare | ✅              | ❌        | ❌        |

```javascript
// var — function scoped, hoisted
console.log(a); // undefined (hoisted)
var a = 10;

// let — block scoped
if (true) {
  let b = 20;
}
// console.log(b); // ReferenceError

// const — block scoped, cannot reassign
const c = 30;
// c = 40; // TypeError
const arr = [1, 2];
arr.push(3); // ✅ Mutation allowed, reassignment not
```

---

### Q4. Hoisting

```javascript
// Function declarations are fully hoisted
greet(); // Works!
function greet() {
  console.log("Hello");
}

// var is hoisted but value is undefined
console.log(x); // undefined
var x = 5;

// let/const are hoisted but in Temporal Dead Zone (TDZ)
// console.log(y); // ReferenceError
let y = 10;
```

---

### Q5. == vs === (Loose vs Strict Equality)

```javascript
5 == "5"; // true (type coercion)
5 === "5"; // false (no coercion)

null == undefined; // true
null === undefined; // false

0 == false; // true
0 === false; // false

// Always use === unless you explicitly need coercion
```

---

### Q6. Arrow Functions

```javascript
// Regular function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// Key difference: 'this' binding
const obj = {
  name: "Alice",
  regular: function () {
    console.log(this.name);
  }, // "Alice"
  arrow: () => {
    console.log(this.name);
  }, // undefined (lexical this)
};
```

---

### Q7. Closures

A **closure** is a function that remembers variables from its outer scope even after the outer function returns.

```javascript
function counter() {
  let count = 0;
  return {
    increment: () => ++count,
    decrement: () => --count,
    getCount: () => count,
  };
}

const c = counter();
c.increment(); // 1
c.increment(); // 2
c.decrement(); // 1
c.getCount(); // 1
// 'count' is private — cannot be accessed directly
```

---

### Q8. map() vs forEach()

```javascript
const nums = [1, 2, 3, 4];

// map — returns a NEW array
const doubled = nums.map((n) => n * 2); // [2, 4, 6, 8]

// forEach — returns undefined, used for side effects
nums.forEach((n) => console.log(n)); // prints each number
```

---

### Q9. Higher-Order Functions

```javascript
// A function that takes or returns another function
function multiplier(factor) {
  return (number) => number * factor;
}

const double = multiplier(2);
const triple = multiplier(3);

double(5); // 10
triple(5); // 15

// Array HOFs
[1, 2, 3, 4, 5]
  .filter((n) => n % 2 === 0) // [2, 4]
  .map((n) => n * 10) // [20, 40]
  .reduce((sum, n) => sum + n, 0); // 60
```

---

### Q10. 'this' Keyword

```javascript
// Global context
console.log(this); // Window (browser) / {} (Node.js)

// Object method
const user = {
  name: "Alice",
  greet() {
    console.log(this.name);
  }, // "Alice"
};

// Explicit binding
function sayHi() {
  console.log(this.name);
}
sayHi.call({ name: "Bob" }); // "Bob"
sayHi.apply({ name: "Charlie" }); // "Charlie"
const bound = sayHi.bind({ name: "Diana" });
bound(); // "Diana"
```

---

### Q11. Promises & Async/Await

```javascript
// Promise
function fetchUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) resolve({ id, name: "User" + id });
      else reject(new Error("Invalid ID"));
    }, 1000);
  });
}

// Promise chaining
fetchUser(1)
  .then((user) => console.log(user))
  .catch((err) => console.error(err));

// Async/Await
async function getUser() {
  try {
    const user = await fetchUser(1);
    console.log(user);
  } catch (err) {
    console.error(err);
  }
}

// Promise.all — parallel execution
const [user1, user2] = await Promise.all([fetchUser(1), fetchUser(2)]);
```

---

### Q12. Event Loop, Call Stack & Task Queue

```javascript
console.log("1"); // Call stack (sync)

setTimeout(() => console.log("2"), 0); // Macro task queue

Promise.resolve().then(() => console.log("3")); // Microtask queue

console.log("4"); // Call stack (sync)

// Output: 1, 4, 3, 2
// Microtasks (promises) execute before macrotasks (setTimeout)
```

---

### Q13. Destructuring & Spread Operator

```javascript
// Object destructuring
const { name, age, city = "Unknown" } = { name: "Alice", age: 25 };

// Array destructuring
const [first, , third] = [1, 2, 3]; // first=1, third=3

// Spread operator
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 }; // { a: 1, b: 2, c: 3 }

// Rest parameters
function sum(...nums) {
  return nums.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3, 4); // 10
```

---

### Q14. Debouncing & Throttling

```javascript
// Debounce — waits until user stops, then fires
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

const searchInput = debounce((query) => {
  console.log("Searching:", query);
}, 300);

// Throttle — fires at most once per interval
function throttle(fn, limit) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}
```

---

### Q15. Event Bubbling & Delegation

```javascript
// Event Bubbling: event travels from target → up to document
// Event Capturing: event travels from document → down to target

document.getElementById("parent").addEventListener(
  "click",
  (e) => {
    console.log("Parent clicked");
  },
  false,
); // false = bubbling (default)

// Event Delegation — handle child events on parent
document.getElementById("list").addEventListener("click", (e) => {
  if (e.target.tagName === "LI") {
    console.log("Clicked:", e.target.textContent);
  }
});
```

---

### Q16. Prototypal Inheritance

```javascript
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function () {
  return `${this.name} makes a sound`;
};

function Dog(name, breed) {
  Animal.call(this, name); // Call parent constructor
  this.breed = breed;
}
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function () {
  return "Woof!";
};

const rex = new Dog("Rex", "Lab");
rex.speak(); // "Rex makes a sound"
rex.bark(); // "Woof!"

// ES6 class syntax (syntactic sugar)
class Cat extends Animal {
  purr() {
    return "Purr...";
  }
}
```

---

### Q17. Currying

```javascript
// Regular function
function add(a, b, c) {
  return a + b + c;
}

// Curried version
function curriedAdd(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}
curriedAdd(1)(2)(3); // 6

// Arrow function curry
const multiply = (a) => (b) => a * b;
const double = multiply(2);
double(5); // 10
```

---

### Q18. null vs undefined

```javascript
let a;
console.log(a); // undefined — declared but not assigned
console.log(typeof a); // "undefined"

let b = null;
console.log(b); // null — intentionally empty
console.log(typeof b); // "object" (JS bug)

null == undefined; // true
null === undefined; // false
```

---

### Q19. Object.freeze() & Deep Freeze

```javascript
const obj = { name: "Alice", address: { city: "NYC" } };
Object.freeze(obj);

obj.name = "Bob"; // Silently fails (no error in non-strict)
obj.address.city = "LA"; // ✅ Works! freeze is SHALLOW

// Deep freeze
function deepFreeze(obj) {
  Object.freeze(obj);
  Object.getOwnPropertyNames(obj).forEach((prop) => {
    if (typeof obj[prop] === "object" && obj[prop] !== null) {
      deepFreeze(obj[prop]);
    }
  });
  return obj;
}
```

---

### Q20. Web Workers

```javascript
// main.js
const worker = new Worker("worker.js");
worker.postMessage({ data: [1, 2, 3, 4, 5] });
worker.onmessage = (e) => {
  console.log("Result:", e.data); // Sum from worker
};

// worker.js
self.onmessage = (e) => {
  const sum = e.data.data.reduce((a, b) => a + b, 0);
  self.postMessage(sum);
};
```

---
