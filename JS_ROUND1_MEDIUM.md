# What is the purpose of 'map' method in Javascript?

The **`map()`** method in JavaScript is used to **create a new array** by **applying a function to each element** of an existing array. It does **not modify** the original array.

---

## ✅ Purpose

- Transforms each element of an array.
- Returns a **new array** with the same length.
- Commonly used for data transformation in a clean and functional style.

---

## 🔹 Syntax

```javascript
array.map(callback(currentValue, index, array), thisArg);

Example:-
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2);

console.log(doubled); // [2, 4, 6, 8]
```

❗ Important Notes
map() does not mutate the original array.

Returns a new array with the same number of elements.

Always use return inside the callback to define what will go into the new array.


# What is the purpose of 'filter' method in Javascript?
The **`filter()`** method is used to **create a new array** that includes only the elements that **pass a specific test condition** provided by a callback function.

---

## ✅ Purpose

- Filters out unwanted elements from an array.
- Returns a **new array** containing only the elements that **meet the condition**.
- Does **not modify** the original array.

---

## 🔹 Syntax

```javascript
array.filter(callback(currentValue, index, array), thisArg);

Example:-  Filter Even Numbers
const numbers = [1, 2, 3, 4, 5, 6];
const evenNumbers = numbers.filter(num => num % 2 === 0);

console.log(evenNumbers); // [2, 4, 6]
```

❗ Important Notes
filter() does not mutate the original array.

Returns a new array that may have fewer elements than the original.

The callback function should return true to keep the element, or false to exclude it.

---

# What is the purpose of 'find' method in Javascript?
The **`find()`** method returns the **first element** in an array that **satisfies a provided testing function**. If no elements match the condition, it returns `undefined`.

---

## ✅ Purpose

- Retrieve a **single element** from an array based on a condition.
- Useful when you're looking for **one specific match** rather than a group of matches.

---

## 🔹 Syntax

```javascript
array.find(callback(currentValue, index, array), thisArg);

const numbers = [5, 12, 8, 130, 44];

const found = numbers.find(num => num > 10);

console.log(found); // 12 (first number > 10)
```

❗ Important Notes
Returns the first matching element, not all matches.

Returns undefined if no elements match the condition.

Stops iterating once a match is found (better performance than filter() when only one match is needed).

# What is the purpose of 'reduce' method in Javascript?
The **`reduce()`** method executes a **reducer function** on each element of the array, resulting in a **single output value**. It's commonly used for **summing numbers**, **flattening arrays**, or **building up a result** from multiple elements.

---

## ✅ Purpose

- To **accumulate** values into a **single result**.
- Very powerful for data processing tasks.
- Does **not mutate** the original array.

---

## 🔹 Syntax

```javascript
array.reduce(callback(accumulator, currentValue, index, array), initialValue);

Example:- Sum of Numbers
const numbers = [1, 2, 3, 4, 5];
const total = numbers.reduce((acc, num) => acc + num, 0);
console.log(total); // 15
```

❗ Important Notes
Always provide an initial value to avoid unexpected results.

If initialValue is omitted, the first element is used as the initial accumulator, and iteration starts from the second element.

Can be difficult to read for beginners, but very powerful.

# What is Event Bubbling And Event Capturing?
In JavaScript, when an event occurs in the DOM (like a click), it doesn’t just affect the exact element—it travels through a **phased path** in the DOM tree. These phases are:

1. **Capturing Phase** (Event Capturing)
2. **Target Phase**
3. **Bubbling Phase** (Event Bubbling)

---

## 🔁 Event Propagation Phases

- **Event Capturing**: Event starts from the **window** and propagates **downward** to the target element.
- **Event Bubbling**: Event starts from the **target element** and **bubbles up** to the window.

By default, most event listeners in JavaScript use the **bubbling phase**.

---

## 🔸 Event Bubbling Example

```html
<div id="parent" style="padding: 20px; background: #eee;">
  Parent
  <button id="child">Click Me</button>
</div>

<script>
  document.getElementById("parent").addEventListener("click", function () {
    console.log("Parent Clicked");
  });

  document.getElementById("child").addEventListener("click", function () {
    console.log("Child Clicked");
  });
</script>
```

✅ Output when clicking the button:
Child Clicked
Parent Clicked
This is event bubbling. The event first triggers on the child, then bubbles up to the parent.

🔹 Event Capturing Example
You can listen during the capturing phase by passing true as the third argument in addEventListener.

document.getElementById("parent").addEventListener(
  "click",
  function () {
    console.log("Parent Capturing");
  },
  true // Capturing phase
);

document.getElementById("child").addEventListener("click", function () {
  console.log("Child Clicked");
});

✅ Output when clicking the button:
Parent Capturing
Child Clicked
This is event capturing—the event is caught by the parent before reaching the child.

🔐 Preventing Event Bubbling
You can stop bubbling using event.stopPropagation():

document.getElementById("child").addEventListener("click", function (e) {
  console.log("Child Clicked");
  e.stopPropagation(); // Stops event from bubbling up
});

# What are the Higher-Order Functions? Can you give an Example?
In JavaScript, **Higher-Order Functions** are functions that can do **at least one** of the following:

1. **Take another function as an argument**
2. **Return a function as a result**

This makes JavaScript a **functional programming language**, allowing you to write cleaner and more reusable code.

---

## ✅ Definition

A **Higher-Order Function (HOF)** is a function that either:
- Accepts another function as an input (callback), or
- Returns another function.

---

## 🔹 Common Examples of Higher-Order Functions in JavaScript

- `map()`
- `filter()`
- `reduce()`
- `forEach()`
- Custom functions that accept or return functions

---

## 🔸 Example: Using `map()` (Built-in Higher-Order Function)

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(function(num) {
  return num * 2;
});

console.log(doubled); // [2, 4, 6, 8]

Example:- Custom Higher-Order Function
function greetUser(greeting) {
  return function(name) {
    console.log(`${greeting}, ${name}!`);
  };
}

const sayHello = greetUser("Hello");
sayHello("Vishal"); // Hello, Vishal!
```

# What is an IIFE?

An **IIFE** (Immediately Invoked Function Expression) is a function in JavaScript that runs **as soon as it is defined**.

It is a **design pattern** used to create a function that **executes immediately** after its creation, without needing to be called explicitly.

---

## ✅ Purpose

- **Encapsulation**: Avoid polluting the global scope.
- **Privacy**: Create private variables.
- **Modular Code**: Helps structure code in self-contained units.

---

## 🔹 Syntax

```javascript
(function() {
  // Code here runs immediately
})();

Example:- Using IIFE to Create Private Scope

const counter = (function () {
  let count = 0;
  return {
    increment: function () {
      count++;
      return count;
    },
    getCount: function () {
      return count;
    }
  };
})();

console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());  // 2
```

# What are Closures? What do you understand by Closures in JS?

A **closure** is a **function that remembers its outer variables** and can access them even after the outer function has finished executing.

Closures are one of the most powerful features of JavaScript, enabling **data privacy**, **stateful functions**, and **function factories**.

---

## ✅ What is a Closure?

> A closure is created when a function is defined **inside another function** and the inner function **accesses variables** from the outer function.

---

## 🔹 Example 1: Basic Closure

```javascript
function outer() {
  const outerVar = "I'm outside!";

  function inner() {
    console.log(outerVar); // Accesses outer function's variable
  }

  return inner;
}

const myFunc = outer();
myFunc(); // Output: I'm outside!

 Example 2:- Closure for Data Privacy

 function secretCounter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const counter = secretCounter();

console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

# How do setTimeout and setInterval work?
In JavaScript, `setTimeout` and `setInterval` are **timer functions** provided by the browser or Node.js that enable **delayed** or **repeated** execution of code.

---

## 🔹 `setTimeout()`

### 📌 Purpose:
Executes a function **once** after a specified number of milliseconds.

### 🔧 Syntax:
```javascript
setTimeout(callback, delay, ...args);
callback: Function to execute

delay: Time in milliseconds

...args: Optional arguments passed to the callback

✅ Example:
setTimeout(() => {
  console.log("Executed after 2 seconds");
}, 2000);
```

## 🔹 setInterval()
### 📌 Purpose:
Executes a function repeatedly at specified intervals (in milliseconds).

### 🔧 Syntax:
```
setInterval(callback, interval, ...args);
callback: Function to run repeatedly

interval: Time interval between executions

...args: Optional arguments passed to the callback

✅ Example:
setInterval(() => {
  console.log("Runs every 1 second");
}, 1000);
🔐 Clearing Timers
To stop setTimeout before it fires: clearTimeout(timeoutId)

To stop setInterval: clearInterval(intervalId)

✂️ Example:
const id = setInterval(() => {
  console.log("Repeating...");
}, 1000);

setTimeout(() => {
  clearInterval(id);
  console.log("Stopped interval");
}, 5000);
```

🧠 How They Work (Internally)
Both setTimeout and setInterval are:

Asynchronous

Part of the browser’s Web APIs (or Node's timer APIs)
Managed by the Event Loop
The functions are placed on the task queue and executed when the call stack is empty.

# What are the Promises in JavaScript? Explain the concept of promises in JS

In JavaScript, a **Promise** is an object that represents the eventual **completion (or failure)** of an **asynchronous operation**, and its resulting value.

Promises help in **managing asynchronous code** and **avoiding callback hell** by providing a cleaner, chainable syntax.

---

## ✅ What is a Promise?

> A Promise is a placeholder for a value that is **not known yet**, but will be resolved in the future.

A Promise can be in one of three states:

| State        | Description                                |
|--------------|--------------------------------------------|
| `pending`    | Initial state, neither fulfilled nor rejected |
| `fulfilled`  | Operation completed successfully            |
| `rejected`   | Operation failed                            |

---

## 🔧 Syntax

```javascript
const promise = new Promise((resolve, reject) => {
  // async code
  if (/* success */) {
    resolve(result);
  } else {
    reject(error);
  }
});

Example: Basic Promises

const fetchData = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve("Data received!");
    } else {
      reject("Failed to fetch data.");
    }
  }, 2000);
});

fetchData
  .then(response => {
    console.log("Success:", response);
  })
  .catch(error => {
    console.error("Error:", error);
  });


Example: Chaining Promises

fetchData
  .then(data => {
    console.log("Step 1:", data);
    return "Next Step";
  })
  .then(step => {
    console.log("Step 2:", step);
  })
  .catch(err => {
    console.error("Something went wrong:", err);
  });

```

# What is the use of async and await in Javascript?
The `async` and `await` keywords in JavaScript make working with Promises easier and **more readable**, providing a way to write **asynchronous code** that looks and behaves like **synchronous** code.

They were introduced in **ES2017 (ES8)**.

---

## ✅ What is `async`?

The `async` keyword is used to **declare a function that always returns a Promise**, even if it returns a non-promise value.

### 🔧 Syntax:
```javascript
async function myFunction() {
  return "Hello";
}
```

## ✅ What is await?

The `await` keyword can only be used inside async functions. It pauses the execution of the function until the Promise is resolved or rejected.

### 🔧 Syntax:
```javascript
const result = await somePromise;
```

### 🔸 Example: Using async/await
```javascript
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Data fetched!");
    }, 2000);
  });
}

async function getData() {
  console.log("Fetching...");
  const result = await fetchData();
  console.log(result);
}

getData();
// Output:
// Fetching...
// (after 2 seconds) Data fetched!
```

### 🔸  Example: Error Handling with try-catch
```javascript
async function getUser() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error fetching user:", error);
  }
}
```

# What is the difference between call, apply and bind?

In JavaScript, `call()`, `apply()`, and `bind()` are methods used to **change the context** (`this`) of a function and optionally pass arguments.

---

## ✅ Purpose

They are used to explicitly set the `this` keyword inside a function.

---

## 🔹 `call()` Method

- Invokes the function **immediately**
- Arguments are passed **individually**

### 🔧 Syntax
```javascript
func.call(thisArg, arg1, arg2, ...);

function greet(greeting, name) {
  console.log(`${greeting}, ${name}! I'm ${this.role}`);
}

const person = { role: 'Developer' };
greet.call(person, 'Hello', 'Vishal');
// Output: Hello, Vishal! I'm Developer
```

---

## 🔹 apply() Method
- Invokes the function immediately
- Arguments are passed as an array

### 🔧 Syntax
```javascript
func.apply(thisArg, [arg1, arg2, ...]);

greet.apply(person, ['Hi', 'Vishal']);
// Output: Hi, Vishal! I'm Developer
```

---

## 🔹 bind() Method
- Returns a new function with this bound to the provided value
- Does not call the function immediately

### 🔧 Syntax
```javascript
const newFunc = func.bind(thisArg, arg1, arg2, ...);

const boundGreet = greet.bind(person, 'Hey');
boundGreet('Vishal');
// Output: Hey, Vishal! I'm Developer

```

# What is Event Delegation?
**Event Delegation** is a technique in JavaScript where a **single event listener** is added to a **parent element**, and it **handles events** that occur on its child elements using **event bubbling**.

---

## ✅ Why Use Event Delegation?

- Efficient memory usage (fewer event listeners)
- Useful when child elements are dynamically added/removed
- Centralized event handling logic

---

## 🧠 How It Works

When an event occurs on a child element, it **bubbles up** to its ancestors. By placing a listener on the parent, you can catch events on any of its current or future child elements.

---

## 🔧 Example

### 📝 HTML:
```html
<ul id="parent">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```
```javascript
const parent = document.getElementById('parent');

parent.addEventListener('click', function(event) {
  if (event.target.tagName === 'LI') {
    console.log('Clicked:', event.target.textContent);
  }
});
// Output (on clicking "Item 2"):
// makefile:

// Clicked: Item 2

```


