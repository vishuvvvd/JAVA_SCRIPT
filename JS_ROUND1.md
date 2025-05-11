# JavaScript Overview

## ❓ What is JavaScript?

**JavaScript** is a **high-level, interpreted programming language** that is primarily used to create **interactive and dynamic content** on the web. It is one of the core technologies of the World Wide Web, alongside **HTML** and **CSS**.

### 🔑 Key Features:
- Lightweight and interpreted
- Dynamically typed
- Supports object-oriented, functional, and imperative programming
- Event-driven and asynchronous by nature
- Runs in both the browser and on servers (via Node.js)

---

## 🌍 Where is JavaScript Commonly Used?

### 1. **Front-End Web Development**
- Dynamic user interfaces
- Form validation and DOM manipulation
- Frameworks: **React**, **Angular**, **Vue.js**

### 2. **Back-End Web Development**
- Server-side programming with **Node.js**
- RESTful APIs and real-time apps (e.g., chat apps)
- Frameworks: **Express.js**, **Nest.js**

### 3. **Mobile App Development**
- Hybrid mobile apps using **React Native**, **Ionic**

### 4. **Desktop Application Development**
- Cross-platform apps using **Electron.js**  
  _Examples: Visual Studio Code, Slack_

### 5. **Game Development**
- Browser-based games  
  _Libraries: **Phaser.js**, **Three.js**_

### 6. **Internet of Things (IoT)**
- Controlling hardware with JavaScript using **Johnny-Five**, **Node.js**

### 7. **Automation and Scripting**
- Writing small utilities or automation scripts in Node.js

### 8. **Machine Learning & Data Visualization**
- ML in the browser with **TensorFlow.js**
- Data charts and visuals using **D3.js**, **Chart.js**

---

## ❓ What are Template Literals?

**Template Literals** (also known as **template strings**) are a feature introduced in **ES6 (ECMAScript 2015)** that allows for **easier string interpolation**, **multi-line strings**, and **expression embedding**.

They are enclosed by **backticks** (`` ` ``) instead of single (`'`) or double (`"`) quotes.

---

## 🧠 Key Features

### ✅ 1. **String Interpolation**
You can embed variables and expressions inside a string using the `${}` syntax.

```javascript
const name = "Vishal";
const greeting = `Hello, ${name}!`;
console.log(greeting); // Output: Hello, Vishal!

---
## 📘 What is Hoisting in JavaScript?

### ❓ Definition

**Hoisting** is a JavaScript mechanism where **variables and function declarations** are **moved (or "hoisted") to the top of their scope** before code execution.

This means you can use variables and functions **before** you declare them — though the behavior differs for `var`, `let`, `const`, and function declarations.

---

### 🧠 Key Points

- **Function declarations** are hoisted entirely (including their body).
- **`var` declarations** are hoisted but initialized with `undefined`.
- **`let` and `const`** are hoisted too, but are **not initialized**, leading to a **Temporal Dead Zone (TDZ)** — using them before declaration throws a `ReferenceError`.

---

### ✅ Example 1: Hoisting with `var`

```javascript
console.log(x); // Output: undefined
var x = 5;

---

## 📘 Difference Between `var`, `let`, and `const` in JavaScript

In JavaScript, `var`, `let`, and `const` are used to declare variables. They differ in **scope**, **hoisting behavior**, **re-declaration**, and **mutability**.

---

## 🔍 Comparison Table

| Feature               | `var`                         | `let`                         | `const`                        |
|------------------------|-------------------------------|-------------------------------|-------------------------------|
| **Scope**             | Function-scoped               | Block-scoped                 | Block-scoped                 |
| **Hoisting**          | Hoisted (initialized as `undefined`) | Hoisted (but not initialized – TDZ) | Hoisted (but not initialized – TDZ) |
| **Re-declaration**    | ✅ Allowed                    | ❌ Not allowed in same scope | ❌ Not allowed in same scope |
| **Re-assignment**     | ✅ Allowed                    | ✅ Allowed                    | ❌ Not allowed               |
| **Default Usage**     | Legacy code, avoid in modern JS | Modern variable declaration | Constants or final variables |

---

## ✅ Example: Scope

```javascript
function testVar() {
  if (true) {
    var x = 10;
  }
  console.log(x); // ✅ Works: 10
}

function testLet() {
  if (true) {
    let y = 20;
  }
  console.log(y); // ❌ ReferenceError: y is not defined
}

//Re-declaration
// var
var a = 1;
var a = 2; // ✅ Allowed

// let
let b = 1;
let b = 2; // ❌ SyntaxError: Identifier 'b' has already been declared

// const
const c = 1;
const c = 2; // ❌ SyntaxError: Identifier 'c' has already been declared

//Re-assignment
// var
var a = 10;
a = 20; // ✅ Allowed

// let
let b = 30;
b = 40; // ✅ Allowed

//const with Objects and Arrays
// const
const c = 50;
c = 60; // ❌ TypeError: Assignment to constant variable

//
const user = { name: "Alice" };
user.name = "Bob"; // ✅ Allowed: modifying properties is OK

user = { name: "Charlie" }; // ❌ TypeError: Assignment to constant variable

const list = [1, 2, 3];
list.push(4); // ✅ Allowed
list = [5, 6]; // ❌ TypeError
END```

---

## 📘 JavaScript Data Types

JavaScript provides different **data types** to hold various kinds of values. These types are categorized into **primitive** and **non-primitive (reference)** types.

---

## 📂 Categories of Data Types

### 1. 🧱 **Primitive Data Types** (Immutable)

These are the most basic data types and **do not have properties or methods**.

| Type      | Description                             | Example           |
|-----------|-----------------------------------------|-------------------|
| `Number`  | Represents numeric values               | `42`, `3.14`, `-7` |
| `String`  | Textual data                            | `"Hello"`, `'A'`  |
| `Boolean` | Logical value: `true` or `false`        | `true`, `false`   |
| `Null`    | Represents intentional absence of value | `null`            |
| `Undefined` | Value not assigned yet               | `undefined`       |
| `Symbol`  | Unique and immutable identifiers        | `Symbol("id")`    |
| `BigInt`  | For large integers beyond `2^53 - 1`    | `123456789012345678901234567890n` |

---

### 2. 🗂️ **Non-Primitive (Reference) Data Types**

These hold **collections of values** or **more complex entities**.

| Type     | Description                               | Example                        |
|----------|-------------------------------------------|--------------------------------|
| `Object` | Collection of key-value pairs             | `{ name: "Alice", age: 25 }`   |
| `Array`  | Ordered list of values                    | `[1, 2, 3]`                     |
| `Function` | Callable object (a type of object)     | `function greet() {}`          |
| `Date`, `RegExp`, etc. | Built-in object types      | `new Date()`, `/abc/`          |

---

## 🔍 Type Checking

- Use `typeof` to check the data type of a value.

```javascript
typeof "Hello";       // "string"
typeof 42;            // "number"
typeof true;          // "boolean"
typeof undefined;     // "undefined"
typeof null;          // "object" ← (historical bug in JS)
typeof Symbol("id");  // "symbol"
typeof BigInt(123);   // "bigint"
typeof { name: "A" }; // "object"
typeof [1, 2, 3];     // "object"
typeof function(){};  // "function"
```
---

## 🔹 6. JavaScript Arrays

Arrays are ordered collections of elements.

### ✅ Syntax:
```javascript
let fruits = ["Apple", "Banana", "Cherry"];
console.log(fruits[0]); // Apple
```

### ✅ Looping:
```javascript
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

### ✅ Access last item:
```javascript
let last = fruits[fruits.length - 1];
```

### ✅ Mixed values:
```javascript
let mixed = [1, "Hello", true, null];
```

---

## 🔍 JavaScript: `==` vs `===`

In JavaScript, `==` and `===` are comparison operators used to check equality, but they behave differently.

---

## 📌 1. `==` (Equality or Abstract Equality)

- Compares **values** after **type conversion**
- Performs **type coercion** if operands are of different types

### ✅ Example:
```javascript
5 == "5"         // true  → because "5" is converted to number 5
0 == false       // true  → false becomes 0
null == undefined // true  → both are loosely equal

5 === "5"         // false → different types
0 === false       // false → number vs boolean
"hello" === "hello" // true → same value and type
```
---

## What is the purpose of isNaN function? 

The **`isNaN()`** function is used to check if a value is **NaN** (Not-a-Number). It returns `true` if the value is **not a valid number** and `false` if the value is a valid number (even if it's a string representation of a number).

---

## 🔍 Purpose of `isNaN()`

- **Checks if a value is NaN** (Not-a-Number).
- **Performs type coercion**, which means it tries to convert the value to a number before making the comparison.

---

## 📚 Syntax:
```javascript
isNaN(value);

//Examples
console.log(isNaN(123));        // false   → 123 is a valid number
console.log(isNaN('123'));      // false   → "123" is coerced to number 123
console.log(isNaN('Hello'));    // true    → "Hello" cannot be converted to a valid number
console.log(isNaN(NaN));        // true    → NaN is not a number
console.log(isNaN(true));       // false   → true is coerced to 1 (valid number)
console.log(isNaN(undefined));  // true    → undefined cannot be converted to a number

// ⚠️ Important Notes:
// isNaN() tries to convert non-numeric values to a number before checking if they are NaN.

// To strictly check if a value is NaN, use the Number.isNaN() method (introduced in ES6), which does not perform type coercion.

// ✅ Example of Number.isNaN():
console.log(Number.isNaN('123'));    // false
console.log(Number.isNaN(NaN));      // true
console.log(Number.isNaN(123));      // false
```
---

## What is null and undefined?
Both `null` and `undefined` are **primitive values** in JavaScript, but they represent different concepts.
---

## 🔹 1. `undefined`

- **Represents a variable that has been declared but not yet assigned a value**.
- Automatically assigned to variables that are **declared but not initialized**.

### ✅ Example:
```javascript
let a;
console.log(a); // undefined → a is declared but not initialized

let b = undefined;
console.log(b); // undefined → explicitly set to undefined

✅ Example:
javascript
Copy
Edit
function greet() {}
console.log(greet()); // undefined → no return value
🔹 2. null
Represents the intentional absence of any object value.

Used to explicitly indicate "no value" or "no object".

✅ Example:
javascript
Copy
Edit
let user = null; 
console.log(user); // null → user is intentionally set to have no value

let obj = { name: "Alice", age: null }; 
console.log(obj.age); // null → age property is explicitly set to null
🔍 Key Differences Between null and undefined
Feature	undefined	null
Type	undefined (primitive)	object (historical bug)
Represents	A variable that has been declared but not assigned a value	An intentional absence of any object value
Assignment	Automatically assigned to uninitialized variables	Explicitly assigned to represent no value
Default Return Value	Default return value for functions without a return statement	Not used as a return value unless explicitly assigned

🧪 Example of null and undefined in Comparison:
javascript
Copy
Edit
let a;
let b = null;

console.log(a == b);    // true → both are falsy values but represent different concepts
console.log(a === b);   // false → different types (undefined vs object)
console.log(a == undefined);  // true → a is undefined
console.log(b == null);       // true → b is explicitly null
📝 Summary
undefined is the default value for uninitialized variables and functions with no return statement.

null is an explicit assignment to represent no value or no object.

---

## Explain the use of typeof operator.?
The **`typeof`** operator is used to check the **data type** of a given variable or expression in JavaScript. It returns a string that represents the type of the operand.

---

## 🔹 Syntax:

```javascript
typeof operand;
🔹 Return Values of typeof:
"undefined" — If the operand is undefined.

"boolean" — If the operand is a boolean value.

"number" — If the operand is a numeric value.

"bigint" — If the operand is a BigInt.

"string" — If the operand is a string.

"symbol" — If the operand is a Symbol.

"object" — If the operand is an object (including arrays, null, etc.).

"function" — If the operand is a function.

🔹 Examples:
✅ Checking undefined:
javascript
Copy
Edit
let a;
console.log(typeof a); // "undefined" → variable is declared but not initialized
✅ Checking boolean:
javascript
Copy
Edit
let isActive = true;
console.log(typeof isActive); // "boolean"
✅ Checking number:
javascript
Copy
Edit
let age = 25;
console.log(typeof age); // "number"
✅ Checking bigint:
javascript
Copy
Edit
let bigNumber = 12345678901234567890n;
console.log(typeof bigNumber); // "bigint"
✅ Checking string:
javascript
Copy
Edit
let name = "John";
console.log(typeof name); // "string"
✅ Checking symbol:
javascript
Copy
Edit
let symbol = Symbol("id");
console.log(typeof symbol); // "symbol"
✅ Checking object:
javascript
Copy
Edit
let user = { name: "Alice", age: 30 };
console.log(typeof user); // "object"

let arr = [1, 2, 3];
console.log(typeof arr); // "object" (arrays are also objects)

let obj = null;
console.log(typeof obj); // "object" (this is a historical JavaScript bug)
✅ Checking function:
javascript
Copy
Edit
function greet() {}
console.log(typeof greet); // "function"

```
