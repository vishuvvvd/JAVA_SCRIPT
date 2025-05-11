# Explain the Event loop in Javascript?
The **Event Loop** is a fundamental concept in JavaScript that enables **non-blocking**, **asynchronous programming** using **single-threaded** execution.

---

## 🧠 Why is it important?

JavaScript is **single-threaded**, meaning it can only execute one piece of code at a time. The event loop allows JavaScript to perform **non-blocking I/O operations** (like fetching data or reading files) while still executing other code.

---

## 🧩 Components Involved

1. **Call Stack** – Executes functions in a Last In, First Out (LIFO) order.
2. **Web APIs / Browser APIs** – Handle async tasks like `setTimeout`, `DOM events`, or `fetch`.
3. **Callback Queue / Task Queue** – Stores callback functions ready to be executed after the call stack is empty.
4. **Microtask Queue** – Stores microtasks (`Promise.then`, `MutationObserver`) and has higher priority than callback queue.
5. **Event Loop** – Continuously checks if the call stack is empty, then pushes tasks from the queues.

---

## 🔄 How the Event Loop Works

1. A function is called and added to the **call stack**.
2. If it includes async code (e.g., `setTimeout`, `fetch`, `Promise`), it's handled by **Web APIs**.
3. Once the async task is complete:
   - The **callback queue** gets the task (for `setTimeout`)
   - The **microtask queue** gets the task (for `Promise.then`)
4. **Event loop** checks:
   - Is call stack empty?
   - If yes, it pushes microtasks first, then macrotasks into the call stack.

---

## 🔧 Example:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");

// OP:

// Start
// End
// Promise
// Timeout
```
🔍 Explanation:
"Start" and "End" are synchronous and run first.

Promise.then is a microtask and runs before setTimeout, which is a macrotask.

# What is the difference between promise and an async/await function?
Both `Promise` and `async/await` are used to handle **asynchronous operations** in JavaScript, but they differ in syntax and readability.

---

## ✅ What is a Promise?

A `Promise` is an object representing the **eventual completion or failure** of an asynchronous operation.

### 🔧 Syntax:
```javascript
const promise = new Promise((resolve, reject) => {
  // async task
});
```

## ✅ What is async/await?
async and await are syntactic sugar built on top of Promises to write asynchronous code in a synchronous-looking style.
async makes a function return a Promise.
await pauses the execution of an async function until the Promise is resolved or rejected.

## Comparison Example

### 🔹 Using Promises:
```javascript
function getData() {
  fetch("https://jsonplaceholder.typicode.com/users/1")
    .then((response) => response.json())
    .then((data) => {
      console.log("Promise:", data.name);
    })
    .catch((error) => {
      console.error("Error:", error);
    });
}
getData();
```

### 🔹 Using async/await:
```javascript
async function getData() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
    const data = await response.json();
    console.log("Async/Await:", data.name);
  } catch (error) {
    console.error("Error:", error);
  }
}
getData();
```

# Describe the purpose of reduce method in arrays?

The `reduce()` method in JavaScript is used to **reduce** an array to a **single value** by executing a **callback function** on each element of the array (from left to right).

---

## ✅ Purpose

- Summing values
- Flattening arrays
- Grouping data
- Transforming arrays into objects

---

## 🔧 Syntax

```javascript
array.reduce(callback(accumulator, currentValue, index, array), initialValue)
```

- accumulator – stores the result of the callback
- currentValue – the current item being processed
- initialValue – optional value to start with (if not provided, first element is used)

### Example 1: Sum of Numbers
```javascript
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((acc, curr) => acc + curr, 0);

console.log(sum); // Output: 15

```

### Example 2: Count Occurrences of Items
```javascript
const fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple'];

const count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});

console.log(count);
// Output: { apple: 3, banana: 2, orange: 1 }

```

### Example 3:  Flatten an Array
```javascript
const nested = [[1, 2], [3, 4], [5]];

const flat = nested.reduce((acc, curr) => acc.concat(curr), []);

console.log(flat); // Output: [1, 2, 3, 4, 5]

```


# Explain the concept of Currying in Javascript?
## 📘 What is Currying?

**Currying** is a technique in JavaScript where a function is **transformed** into a sequence of functions, **each taking a single argument**.

Instead of:
```js
f(a, b, c)

f(a)(b)(c)
```

## ✅ Purpose of Currying
- Improves code reusability
- Enables function composition
- Helps create specialized or partially applied functions

## 🔧 Example: Normal Function vs Curried

###  Normal Function
```javascript
function add(a, b) {
  return a + b;
}
console.log(add(2, 3)); // 5
```

###  Curried Version
```javascript
function curriedAdd(a) {
  return function(b) {
    return a + b;
  };
}

const addTwo = curriedAdd(2);
console.log(addTwo(3)); // 5

```

### Currying Multiple Arguments
```javascript
function multiply(a) {
  return function(b) {
    return function(c) {
      return a * b * c;
    };
  };
}
console.log(multiply(2)(3)(4)); // 24

```


# What is a Generator function, and how it is used?
A **Generator Function** is a special type of function in JavaScript that can **pause** its execution using the `yield` keyword and **resume** later from where it left off.

Defined using the `function*` syntax.

---

## 🔧 Syntax

```javascript
function* generatorName() {
  yield value1;
  yield value2;
  // ...
}

function* countToThree() {
  yield 1;
  yield 2;
  yield 3;
}

const counter = countToThree();

console.log(counter.next()); // { value: 1, done: false }
console.log(counter.next()); // { value: 2, done: false }
console.log(counter.next()); // { value: 3, done: false }
console.log(counter.next()); // { value: undefined, done: true }

```
### 🧠 Use Case Example: Custom Iterator
```javascript
function* idGenerator() {
  let id = 1;
  while (true) {
    yield id++;
  }
}

const getId = idGenerator();

console.log(getId.next().value); // 1
console.log(getId.next().value); // 2
console.log(getId.next().value); // 3
```


# What are Weak Maps and Weak Sets in Javascript?

## 🔹 What is a WeakMap?
A **WeakMap** is a collection of key-value pairs in which the **keys must be objects**, and the references to those keys are **weakly held**, meaning they **do not prevent garbage collection** if there are no other references to the key.

### ✅ Key Characteristics:
- Only **objects** can be used as keys (not primitives).
- Keys are **not enumerable** (cannot be iterated).
- Automatically removes entries when the key object is garbage collected.

### 🔧 Example:
```javascript
const wm = new WeakMap();

let obj = { name: "Vishal" };
wm.set(obj, "This is a weak reference");

console.log(wm.get(obj)); // Output: This is a weak reference

obj = null; // Now the object is eligible for garbage collection
```

## 🔹 What is a WeakSet?
A **WeakSet** is a collection of objects only, similar to a regular Set, but the values are held weakly.

### ✅ Key Characteristics:
- Only stores objects (not primitives).
- No duplicates allowed.
- Values are not enumerable (no .forEach(), no loops).
- Useful for keeping track of object references without preventing garbage collection.

### 🔧 Example:
```javascript
const ws = new WeakSet();

let user = { name: "Alice" };
ws.add(user);

console.log(ws.has(user)); // true

user = null; // Object can be garbage collected
```

# How does javascript handle Memory Management?
## 📘 What is Memory Management?

Memory management in JavaScript refers to the process of:
1. **Allocating memory** when values are created
2. **Using memory** while executing code
3. **Automatically releasing memory** when it's no longer needed (Garbage Collection)

---

## 🔹 Memory Lifecycle

1. **Allocate**: Memory is allocated when variables, objects, arrays, or functions are created.
2. **Use**: The allocated memory is used for reading and writing operations.
3. **Release**: Memory is freed when values become unreachable.

---

## ♻️ Garbage Collection (GC)

JavaScript uses **Automatic Garbage Collection** – you don't manually free memory.

The most common strategy used is:

### 🔍 Mark-and-Sweep Algorithm

- The GC starts from **roots** (like `window`, `global`, current scope).
- It **marks** everything that's reachable.
- Anything **unmarked** is considered unreachable and **collected**.

---

## ✅ Example: Reachable vs Unreachable

```javascript
let user = {
  name: "Vishal",
};

user = null; // The object is no longer reachable => eligible for GC
```

## Common Memory Leaks

### 1. Global Variables
```javascript
someGlobal = "I'm global"; // Not declared with let/const/var

```

### 2. Detached DOM Elements
```javascript
let element = document.getElementById("demo");
element.remove(); // But variable still references it

```

### 3. Closures Holding References
```javascript
function outer() {
  let largeData = new Array(1000000).fill("*");
  return function inner() {
    console.log(largeData[0]);
  };
}

```

### 4. Forgotten Timers / Intervals
```javascript
setInterval(() => {
  console.log("Leaking!");
}, 1000); // Never cleared => memory leak
```

## 🛠 Best Practices to Avoid Leaks
- Use let and const (avoid accidental globals)
- Dereference variables (obj = null) when done
- Remove event listeners when not needed
- Clear timers (clearTimeout, clearInterval)
- Avoid unnecessary references (like caching large DOM trees)



# Describe the difference between Shallow and Deep coppying.

## 📘 What is Copying in JavaScript?

In JavaScript, **copying** refers to creating a new variable with the same content as an existing one. There are two main types:

- **Shallow Copy**: Copies only the first level of properties.
- **Deep Copy**: Recursively copies all levels of nested objects or arrays.

---

## 🧪 Shallow Copy

### ✅ Definition

A **shallow copy** creates a new object or array, but **nested objects are still referenced**, not copied.

### 🔧 Example

```javascript
const original = {
  name: "Vishal",
  address: { city: "Belagavi" }
};

const shallow = { ...original };
shallow.name = "Rahul";
shallow.address.city = "Bangalore";

console.log(original.name);         // Vishal ✅ (not affected)
console.log(original.address.city); // Bangalore ❌ (changed!)
```

### 🛠 Common Shallow Copy Methods
```javascript
// Arrays
const arr = [1, 2, 3];
const shallowArr = [...arr]; // or arr.slice()

// Objects
const obj = { a: 1 };
const shallowObj = Object.assign({}, obj); // or { ...obj }
```


## 🌊 Deep Copy

### ✅ Definition
A deep copy recursively copies all levels of a data structure, so the new object has no shared references with the original.

### Example
```javascript
const original = {
  name: "Vishal",
  address: { city: "Belagavi" }
};

const deep = JSON.parse(JSON.stringify(original));
deep.address.city = "Mysore";

console.log(original.address.city); // Belagavi ✅ (not changed)

```

### ⚠️ Limitations of JSON.parse/stringify
- Doesn't copy functions
- Loses undefined, Symbol, and Date objects

### ✅ Better Deep Copy Libraries
- lodash → _.cloneDeep(object)
- structuredClone() (built-in in modern browsers)

// Modern way
const deepClone = structuredClone(original);



# What is Javascript's Strict mode, and how it is enabled?
## 📘 What is Strict Mode?

**Strict Mode** is a way to opt in to a restricted version of JavaScript. It helps you write cleaner, more secure, and more optimized code by catching silent errors and preventing unsafe actions.

Introduced in **ECMAScript 5**, it enforces stricter parsing and error handling.

---

## ✅ How to Enable Strict Mode

### 1. **In a Script (Global Scope)**
```javascript
'use strict';

x = 10; // ❌ ReferenceError: x is not defined
function demo() {
  'use strict';
  y = 20; // ❌ ReferenceError: y is not defined
}
demo();
```

## 🔒 Why Use Strict Mode?
### ✅ Benefits:
- Eliminates silent JavaScript errors.
- Prevents accidental global variable creation.
- Disallows duplicate parameter names.
- Throws error for assigning to read-only properties.
- Makes this in functions default to undefined instead of window.

## 🧪 Examples
### ❌ Without Strict Mode:
```javascript
a = 5;
console.log(a); // 5 (no error, but pollutes global scope)

```

### ✅ With Strict Mode:
```javascript
'use strict';

b = 10; // ReferenceError: b is not defined

```

# Explain the Observer pattern and how it is related to javascript?
## 📘 What is the Observer Pattern?

The **Observer Pattern** is a design pattern in which:
- **One object (Subject)** maintains a list of dependents (Observers),
- Notifies them **automatically** of any state changes, usually by calling one of their methods.

It's widely used for implementing **event-driven** or **reactive** architectures.

---

## 🔄 Real-Life Analogy

> Think of a **YouTube channel (Subject)**. When you **subscribe (Observer)** to it, you get notified (callback) every time it uploads a new video (state change).

---

## 🧠 Key Components

| Component | Role |
|----------|------|
| Subject  | Holds state and manages observers |
| Observer | Wants to be notified of state changes |
| Notify   | Triggered when state changes |

---

## 📌 Observer Pattern in JavaScript

JavaScript is inherently **event-driven**, making the Observer Pattern extremely common.

### ✅ Example: Custom Implementation

```javascript
class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(fn) {
    this.observers.push(fn);
  }

  unsubscribe(fn) {
    this.observers = this.observers.filter(subscriber => subscriber !== fn);
  }

  notify(data) {
    this.observers.forEach(observer => observer(data));
  }
}

// Usage
const subject = new Subject();

const observer1 = (data) => console.log('Observer 1:', data);
const observer2 = (data) => console.log('Observer 2:', data);

subject.subscribe(observer1);
subject.subscribe(observer2);

subject.notify('Hello Observers!'); // Both observers are notified
```

## 📦 Where is Observer Pattern used in JavaScript?
### 🔹 1. DOM Events
```javascript
button.addEventListener('click', () => {
  console.log('Button clicked!');
});
```

### 🔹 2. RxJS and Reactive Programming
```javascript
import { Subject } from 'rxjs';

const subject = new Subject();
subject.subscribe(data => console.log('Received:', data));
subject.next('New Data'); // Observer notified

```

### 🔹 2. Vue.js, React (State management)
- Many frontend libraries use observer-like behavior to detect and respond to changes in state.


# 🌐 WebSockets in JavaScript

## 📘 What are WebSockets?

**WebSockets** are a communication protocol that enables **full-duplex** (two-way) communication between a **client** (usually a browser) and a **server** over a **single, long-lived connection**.

Unlike HTTP, which is **request-response based**, WebSockets allow both the client and server to **send messages at any time**, making it ideal for **real-time applications**.

---

## 🎯 Role of WebSockets in JavaScript

- Enable **real-time communication** in web apps
- Useful in chat apps, online gaming, stock tickers, live dashboards, collaborative tools, etc.
- **Reduces latency and overhead** compared to frequent HTTP polling

---

## ⚙️ How WebSockets Work

1. The client opens a WebSocket connection using JavaScript.
2. The server upgrades the HTTP connection to a WebSocket protocol.
3. Both can now send/receive messages asynchronously.

---

## 🧪 Example: Using WebSockets in JavaScript

```javascript
// Step 1: Create a WebSocket connection
const socket = new WebSocket('ws://localhost:3000');

// Step 2: Listen for messages from the server
socket.onmessage = function(event) {
  console.log('Message from server:', event.data);
};

// Step 3: Send a message to the server
socket.onopen = function() {
  socket.send('Hello Server!');
};

// Step 4: Handle errors
socket.onerror = function(error) {
  console.log('WebSocket error:', error);
};

// Step 5: Handle connection close
socket.onclose = function() {
  console.log('Connection closed');
};
```

## 📦 When to Use WebSockets?
### 🔁 Real-time chat systems (e.g., WhatsApp Web)

- 📈 Live data streaming (e.g., stock price updates)
- 🎮 Multiplayer online games
- ✍️ Collaborative editing (e.g., Google Docs)

## 🧠 Difference Between WebSocket and HTTP

| Feature         | WebSocket                       | HTTP                              |
|----------------|----------------------------------|------------------------------------|
| **Communication** | Full-duplex (bi-directional)     | Half-duplex (client initiates)     |
| **Connection**    | Persistent                       | Stateless (short-lived)            |
| **Overhead**      | Low                              | High (headers per request)         |
| **Use Case**      | Real-time communication          | Traditional request/response model |

---

### 📌 Summary

- **WebSocket** is ideal for applications requiring **live, real-time interaction**, such as chat apps or live data feeds.
- **HTTP** is best for standard web page requests, APIs, and one-time client-server interactions.

> 💡 Use WebSockets when you need ongoing data exchange without the overhead of repeated HTTP requests.
