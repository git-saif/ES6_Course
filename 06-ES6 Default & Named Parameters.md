একদম ঠিক! 👌  
এখন দেখা যাক **ES6 Default Parameters** এবং **Named Parameters** —  
এই দুটি বিষয় JavaScript Function Parameter Handling-এর খুব গুরুত্বপূর্ণ অংশ।  
নিচে পুরো বিষয়টি **Basic → Advanced** আকারে সাজানো হলো তোমার নোট ফরম্যাটে।

---

# **ES6 Default & Named Parameters**

---

##### **Definition:**

**ES6 Default Parameters** এমন একটি ফিচার যা function-এর parameter-এ default মান সেট করতে দেয়,  
যখন argument পাস করা হয় না বা undefined হয়।

**Named Parameters** মানে হলো object আকারে function-এর parameter পাস করা,  
যাতে parameter-এর ক্রম (order) গুরুত্বপূর্ণ না হয়।

---

##### **Syntax:**

```javascript
// Default Parameter
function greet(name = "Guest") {
  console.log(`Hello, ${name}`);
}

// Named Parameter (Object Destructuring)
function createUser({ name, age }) {
  console.log(`Name: ${name}, Age: ${age}`);
}
```

---

##### **Explanation:**

- **Default Parameter** দিয়ে fallback মান নির্ধারণ করা হয়।
    
- **Named Parameter** ব্যবহার করলে function call আরও readable হয়।
    
- Named Parameter সাধারণত destructuring-এর মাধ্যমে ব্যবহৃত হয়।
    

---

##### **Examples:**

```javascript
// Default Parameter Example
function sayHello(name = "Friend") {
  console.log(`Hello, ${name}!`);
}
sayHello("Saiful"); // Hello, Saiful!
sayHello(); // Hello, Friend!

// Named Parameter Example
function introduce({ name, age, country = "Bangladesh" }) {
  console.log(`${name} is ${age} years old from ${country}`);
}
introduce({ name: "Rafi", age: 22 }); // Rafi is 22 years old from Bangladesh
```

---

##### **Use Case:**

- Function-এর parameter অনুপস্থিত থাকলে fallback মান দেওয়া।
    
- Function parameter-এর ক্রম (order) পরিবর্তনযোগ্য করা।
    
- Code readability ও flexibility বাড়ানো।
    

---

## **Types / Variations:**

---

### **1. Type-1: Default Parameters**

##### **Definition:**

Function parameter-এর মান না থাকলে **default value** ব্যবহার করার পদ্ধতি।

##### **Syntax:**

```javascript
function functionName(param = defaultValue) {
  // code
}
```

##### **Explanation:**

যখন function call করার সময় কোনো argument পাস করা হয় না,  
অথবা argument-এর মান undefined হয়, তখন default value কার্যকর হয়।

##### **Examples:**

```javascript
// Basic Example
function multiply(a, b = 2) {
  return a * b;
}
console.log(multiply(5));    // Output: 10
console.log(multiply(5, 3)); // Output: 15

// Using function call as default
function getTaxRate() {
  return 0.15;
}
function calculate(price, tax = getTaxRate()) {
  return price + (price * tax);
}
console.log(calculate(100)); // Output: 115

// Default with destructuring
function printUser({ name = "Guest", age = 18 } = {}) {
  console.log(`Name: ${name}, Age: ${age}`);
}
printUser(); // Output: Name: Guest, Age: 18
```

##### **Explanation:**

- Function-এর default মান static বা dynamic (function call) দু’ভাবেই হতে পারে।
    
- Destructuring-এর সঙ্গে ব্যবহার করলে error এড়ানো যায়।
    

##### **Use Case:**

1. Optional parameter-এর fallback মান সেট করা।
    
2. Function কে flexible ও reusable করা।
    
3. API বা form data না থাকলে default data ব্যবহার করা।
    

##### **Error Cases / Common Mistakes ⚠️:**

- Undefined argument না হলে default মান কাজ করে না।
    
    ```javascript
    multiply(5, null); // Output: 0 ❌ (default মান নেয়নি)
    ```
    
- Parameter-এর default মান আগে থাকা variable বা function-এর উপর নির্ভর করলে careful হতে হয়।
    

##### **Best Practice ⚡:**

- Default value simple রাখো।
    
- Nested destructuring-এর সময় সবসময় default object `{}` ব্যবহার করো।
    
    ```javascript
    function config({ port = 3000 } = {}) {}
    ```
    

---

### **2. Type-2: Named Parameters (Object Destructuring)**

##### **Definition:**

Named Parameter মানে হলো function call-এর সময় parameter-গুলো object আকারে পাস করা,  
যাতে ক্রম (order) গুরুত্বপূর্ণ না থাকে, বরং নামের ভিত্তিতে মান match হয়।

##### **Syntax:**

```javascript
function functionName({ param1, param2 }) { ... }

functionName({ param2: "value2", param1: "value1" });
```

##### **Explanation:**

- Named parameter সাধারণত destructuring-এর মাধ্যমে implement করা হয়।
    
- Parameter-এর সংখ্যা বেশি হলে কোড পড়া সহজ হয়।
    
- Default মানও দেওয়া যায়।
    

##### **Examples:**

```javascript
// Basic Example
function createUser({ name, age }) {
  console.log(`Name: ${name}, Age: ${age}`);
}
createUser({ age: 22, name: "Saiful" }); // Order doesn't matter ✅

// Default value with named parameters
function connectDB({ host = "localhost", port = 3306, user = "root" } = {}) {
  console.log(`Connecting to ${host}:${port} as ${user}`);
}
connectDB(); // Connecting to localhost:3306 as root
connectDB({ port: 5000, user: "admin" }); // Connecting to localhost:5000 as admin

// Optional parameter safety
function sendEmail({ to, subject = "No Subject", body = "" } = {}) {
  console.log(`Email sent to ${to} with subject "${subject}"`);
}
sendEmail({ to: "user@example.com" });
```

##### **Explanation:**

- Named parameter ব্যবহারে কোড self-documenting হয়।
    
- Default মান থাকলে missing field error দেয় না।
    

##### **Use Case:**

1. Function-এ অনেক parameter থাকলে readability বজায় রাখা।
    
2. API বা configuration object pass করা।
    
3. Optional parameter handle করা সহজ করা।
    

##### **Error Cases / Common Mistakes ⚠️:**

- যদি function-এ object destructuring করা হয় কিন্তু call করার সময় object পাস না করা হয় → ❌ Error:
    
    ```javascript
    function greet({ name }) { console.log(name); }
    greet(); // ❌ TypeError
    ```
    
- Undefined parameter handle না করলে destructuring error হতে পারে।
    

##### **Best Practice ⚡:**

- Default empty object `{}` ব্যবহার করা উচিত:
    
    ```javascript
    function greet({ name = "Guest" } = {}) { ... }
    ```
    
- Named parameter ব্যবহার করার সময় সবসময় destructuring syntax clean রাখো।
    

---

### **3. Type-3: Combined Usage (Default + Named Parameters)**

##### **Definition:**

Function-এর parameter যদি destructured object হয়,  
তাহলে তার মধ্যে default মান নির্ধারণ করা যায় — একে **Combined Usage** বলা হয়।

##### **Syntax:**

```javascript
function funcName({ param1 = val1, param2 = val2 } = {}) {}
```

##### **Examples:**

```javascript
function setupServer({ host = "localhost", port = 8000 } = {}) {
  console.log(`Server running on ${host}:${port}`);
}

// Both parameters missing
setupServer(); // Output: Server running on localhost:8000

// Only port provided
setupServer({ port: 3000 }); // Output: Server running on localhost:3000
```

##### **Explanation:**

এতে function সবসময় default safe থাকে —  
object না দিলেও error হবে না, আবার কিছু field না দিলেও default মান বসবে।

##### **Use Case:**

- Configuration, environment variable, options object ইত্যাদিতে সবচেয়ে বেশি ব্যবহৃত।
    

##### **Error Cases / Common Mistakes ⚠️:**

- Default object বাদ দিলে undefined destructuring error হতে পারে।
    
    ```javascript
    function test({ a = 1 }) {}
    test(); // ❌ Error (object missing)
    ```
    

##### **Best Practice ⚡:**

- সবসময় `{}` কে default object হিসেবে ব্যবহার করো।
    
- Parameter বেশি হলে Named + Default দুটো একসাথে ব্যবহার করা ভালো।
    

---

## **Summary:**

|Feature|Description|Example|Safe Default|
|---|---|---|---|
|**Default Parameter**|Argument না থাকলে fallback মান ব্যবহার|`function add(a=5,b=2){}`|✅|
|**Named Parameter**|Object আকারে parameter পাস|`function func({x,y}){}`|❌|
|**Combined (Named + Default)**|Destructuring + Default fallback|`function f({x=1,y=2}={}){}`|✅|

---

### **Common Mistakes ⚠️**

1. `null` পাস করলে default মান কাজ করে না (শুধু `undefined` হলে কাজ করে)।
    
2. Object destructuring-এ default object না দিলে TypeError হয়।
    
3. Parameter default মানে complex logic দিলে readability কমে যায়।
    

---

### **Best Practices ⚡**

✅ Default parameter সহজ ও বোধগম্য রাখো।  
✅ Named parameter-এর জন্য সবসময় destructuring-এর সঙ্গে `{}` fallback দাও।  
✅ Default value হিসেবে function call ব্যবহার করা যায়, কিন্তু performance issue মাথায় রাখো।  
✅ Named parameter optional হলে explicit default value ব্যবহার করো।

---

তুমি কি পরের টপিক হিসেবে **ES6 Classes** (constructor, inheritance, static, super, getter/setter) তৈরি করতে চাও এই একই ফরম্যাটে?