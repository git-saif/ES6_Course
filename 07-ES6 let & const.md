##### **Definition:**

- **`let`** হলো block-scoped variable declaration, যা traditional `var` এর তুলনায় নিরাপদ এবং predictable।
- **`const`** হলো constant variable declaration, যার মান একবার অ্যাসাইন করলে পরিবর্তন করা যায় না (immutable binding)।

---
##### **Syntax:**

```javascript
let variableName = value;
const constantName = value;
```

---
##### **Explanation:**

- `let` variable শুধুমাত্র সেই **block, statement, বা expression** এর মধ্যে সীমাবদ্ধ থাকে।
- `const` variable-এ একবার মান assign করলে পরে পুনঃঅ্যাসাইন করা যায় না।
- `var` এর মতো function-scoped নয়, তাই hoisting behaviour ভিন্ন।

---
##### **Examples:**

```javascript
// let example
let age = 25;
age = 26; // ✅ valid
console.log(age); // 26

// const example
const name = "Saiful";
name = "Rafi"; // ❌ Error: Assignment to constant variable

// const object
const user = { name: "Saiful" };
user.name = "Rafi"; // ✅ allowed (object property change)
user = {}; // ❌ Error (cannot reassign object)
```

---
##### **Use Case:**

1. Block-scoped variable দরকার হলে `let` ব্যবহার করা।
2. Immutable value বা constant রাখা হলে `const` ব্যবহার করা।
3. Array/Object reference রাখতে `const` ব্যবহার করে reassignment block করা।

---
## **Types / Variations:**

---
### **1. Type-1: let**

##### **Definition:**

Block-scoped, mutable variable declaration।

##### **Syntax:**

```javascript
let variableName = value;
```

##### **Explanation:**

- Block-scoped মানে `{ }` এর মধ্যে ভ্যারিয়েবল শুধু সেখানে visible।
- Hoisting হয় কিন্তু temporal dead zone (TDZ) থাকে।
##### **Examples:**

```javascript
if (true) {
  let x = 10;
  console.log(x); // 10
}
console.log(x); // ❌ ReferenceError

for (let i = 0; i < 3; i++) {
  console.log(i); // 0, 1, 2
}
console.log(i); // ❌ ReferenceError
```
##### **Explanation:**

- Variable শুধুমাত্র সেই block scope-এর মধ্যে accessible।
- Loop variable-এ `var` নয়, `let` ব্যবহার করলে closure issue হয় না।

##### **Use Case:**

- Loop variable (for/while)
- Conditional block variable
- Temporary variable in function

##### **Error Cases / Common Mistakes ⚠️:**

- TDZ (temporal dead zone) এর আগে access করলে ReferenceError:

```javascript
console.log(a); // ❌ ReferenceError
let a = 5;
```

##### **Best Practice ⚡:**

- সব mutable variable-এর জন্য `let` ব্যবহার করা।
- `var` বাদ দেওয়াই ভালো, কারণ block scope predictable behaviour দেয়।

---

### **2. Type-2: const**

##### **Definition:**

Block-scoped, immutable binding variable।

##### **Syntax:**

```javascript
const variableName = value;
```

##### **Explanation:**

- `const` মানে variable reassignment করা যাবে না।
- Primitive data type immutable, কিন্তু object/array property বা element change করা যায়।

##### **Examples:**

```javascript
// Primitive
const PI = 3.1416;
PI = 3.14; // ❌ Error

// Object
const user = { name: "Saiful", age: 25 };
user.age = 26; // ✅ allowed
user = { name: "Rafi" }; // ❌ Error

// Array
const numbers = [1, 2, 3];
numbers.push(4); // ✅ allowed
numbers = []; // ❌ Error
```

##### **Explanation:**

- `const` একবার binding set করার পরে পরিবর্তন করা যাবে না।
- Object বা Array reference একই থাকে, কিন্তু content পরিবর্তন করা যায়।
##### **Use Case:**

- Constant value (PI, config value)
- Reference variable (Object, Array)
- Immutable data pattern follow করা

##### **Error Cases / Common Mistakes ⚠️:**

- Primitive value পুনরায় assign করা ❌
- Object/Array পুরো reassignment ❌
- Block scope ভুল বোঝার কারণে error (hoisting vs TDZ)

##### **Best Practice ⚡:**

- Default variable `const` ব্যবহার করা।
- Mutable হলে `let` ব্যবহার করা।
- Immutable pattern বজায় রাখা, reassignment করা এড়িয়ে যাওয়া।

---
### **3. Type-3: Temporal Dead Zone (TDZ) Concept**

##### **Definition:**

Block scope-এ `let` বা `const` declare করার আগে access করলে **ReferenceError** হয়।  
এটাকে **Temporal Dead Zone (TDZ)** বলা হয়।

##### **Explanation:**

- Hoisting হয়, কিন্তু variable use করার আগে declaration হতে হবে।

##### **Examples:**

```javascript
console.log(a); // ❌ ReferenceError
let a = 10;

{
  console.log(b); // ❌ ReferenceError
  const b = 5;
}
```

##### **Use Case:**

- Hoisting behaviour predict করতে।
- Early access থেকে bugs prevent করতে।

##### **Error Cases / Common Mistakes ⚠️:**

- `var` এর মতো hoisting আশা করা।
- Loop variable বা function block variable ভুলে আগে access করা।

##### **Best Practice ⚡:**

- Variable declaration সবসময় ব্যবহার করার আগে করা।
- `let` এবং `const` use করে predictable block scope follow করা।

---
## **Summary Table:**

|Keyword|Scope|Reassignable|Hoisting|Use Case|
|---|---|---|---|---|
|`var`|Function-scoped|✅|Hoisted, initialized with undefined|Legacy code|
|`let`|Block-scoped|✅|Hoisted, TDZ active|Mutable variable, loop, temp|
|`const`|Block-scoped|❌|Hoisted, TDZ active|Constant, config, reference (object/array)|

---
### **Key Points:**

- `let` & `const` = **block scoped**, safer than `var`.
- Default: `const`, mutable: `let`.
- `const` object/array content পরিবর্তন করা যায়, reassignment নয়।
- TDZ মানে declaration-এর আগে access ❌ ReferenceError।
- Modern JS-এ **var ব্যবহার করা পরিহার করা** উচিত।

---
## **var, let, const এগুলোর পার্থক্য:**

`var`, `let`, এবং `const` — এই তিনটি JavaScript-এ **variable declare** করার জন্য ব্যবহৃত হয়।  
তবে এদের মধ্যে কিছু গুরুত্বপূর্ণ **পার্থক্য** রয়েছে (scope, re-declaration, re-assignment ইত্যাদির দিক থেকে)।

---

## 1. var

### 🔹 Definition:

`var` হলো পুরোনো পদ্ধতি (ES5 পর্যন্ত)।  
এটি **function-scoped** এবং **hoisted** হয়।

### 🔹 বৈশিষ্ট্য:

- ✅ **Re-declare করা যায়** (same scope এ)
- ✅ **Re-assign করা যায়**
- ⚠️ **Function scoped** (block scoped নয়)
- ⚠️ **Hoisting হয়** (variable declaration উপরে উঠে যায়)
### 🔹 Example:

```js
var name = "Saif";
var name = "Islam"; // ✅ re-declare possible
name = "Rahman"; // ✅ re-assign possible

if (true) {
  var age = 25; // function scoped
}
console.log(age); // ✅ 25 (accessible outside block)
```

---

## 2. let

### 🔹 Definition:

`let` হলো **ES6 (2015)** এ নতুন করে আনা keyword।  
এটি **block-scoped** ({} এর ভিতরে সীমাবদ্ধ)।

### 🔹 বৈশিষ্ট্য:

- ❌ **Re-declare করা যায় না** (same scope এ)
- ✅ **Re-assign করা যায়**
- ✅ **Block scoped**
- ⚠️ Hoisting হয়, তবে **temporal dead zone** এর কারণে আগে ব্যবহার করা যায় না

### 🔹 Example:

```js
let name = "Saif";
// let name = "Islam"; ❌ Error: already declared
name = "Rahman"; // ✅ re-assign possible

if (true) {
  let city = "Dhaka";
  console.log(city); // ✅ Dhaka
}
// console.log(city); ❌ Error: not defined (block scoped)
```

---

## 3. const

### 🔹 Definition:

`const` ও ES6 থেকে এসেছে।  
এটি **block-scoped**, এবং **constant (unchangeable)** মান রাখে।

### 🔹 বৈশিষ্ট্য:

- ❌ **Re-declare করা যায় না**
- ❌ **Re-assign করা যায় না**
- ✅ **Block scoped**
- ⚠️ Object/Array এর ক্ষেত্রে **property পরিবর্তন করা যায়**, তবে variable নিজে re-assign করা যায় না

### 🔹 Example:

```js
const country = "Bangladesh";
// country = "India"; ❌ Error: can't reassign

if (true) {
  const capital = "Dhaka";
  console.log(capital); // ✅ Dhaka
}
// console.log(capital); ❌ Error: not defined
```

👉 **Object এর ক্ষেত্রে:**

```js
const person = { name: "Saif", age: 25 };
person.age = 30; // ✅ allowed (property পরিবর্তন করা যায়)
console.log(person); // { name: "Saif", age: 30 }

// person = { name: "Rahim" }; ❌ Error: re-assign not allowed
```

---

## 🧾 Summery:

|Feature / Keyword|var|let|const|
|---|---|---|---|
|**Scope**|Function scoped|Block scoped|Block scoped|
|**Re-declare**|✅ Possible|❌ Not allowed|❌ Not allowed|
|**Re-assign**|✅ Possible|✅ Possible|❌ Not allowed|
|**Hoisting**|✅ Yes (initialized with `undefined`)|⚠️ Yes (TDZ error before declaration)|⚠️ Yes (TDZ error before declaration)|
|**Introduced In**|ES5 (Old JS)|ES6 (Modern JS)|ES6 (Modern JS)|

---

## 🧠 Use Cases (Best Practice):

✅ **`const`** – Default choice; use it when value should not change  
✅ **`let`** – When variable value needs to change later  
⚠️ **`var`** – Avoid using; it causes confusion due to function-scope & hoisting issues

---
