চমৎকার ✅  
নিচে **“ES6 Destructuring”** নিয়ে সম্পূর্ণ নোট দেওয়া হলো —  
তোমার নির্ধারিত স্ট্রাকচার অনুযায়ী, **Basic থেকে Advanced** পর্যন্ত সব বিষয় অন্তর্ভুক্ত করা হয়েছে।

---

# **ES6 Destructuring**

---

##### Definition:

**Destructuring** হলো ES6-এর একটি feature যা দিয়ে **object** বা **array** থেকে মানগুলো সহজে আলাদা ভ্যারিয়েবলে বের করা যায়।  
এটি traditional assignment-এর বিকল্প, যা কোডকে সংক্ষিপ্ত ও পড়তে সহজ করে।

---

##### Syntax:

```javascript
// Array Destructuring
const [a, b] = [10, 20];

// Object Destructuring
const {name, age} = {name: "Saiful", age: 25};
```

---

##### Explanation:

Destructuring-এর মাধ্যমে একটি array বা object থেকে একাধিক মান একসাথে বের করা যায়।  
আগে যেভাবে আলাদা আলাদা ভ্যারিয়েবল অ্যাসাইন করতে হতো, এখন তা এক লাইনে করা যায়।

---

##### examples:

```javascript
// Array Destructuring
const numbers = [1, 2, 3];
const [x, y, z] = numbers;
console.log(x, y, z); // Output: 1 2 3

// Object Destructuring
const user = { name: "Saiful", age: 25 };
const { name, age } = user;
console.log(name, age); // Output: Saiful 25
```

---

##### Explanation:

উপরের উদাহরণে দেখা যাচ্ছে, array বা object-এর মান সরাসরি ভ্যারিয়েবলে অ্যাসাইন হচ্ছে।  
এতে কোড আরও সংক্ষিপ্ত ও পরিষ্কার হয়।

---

##### Use Case:

1. Function parameter থেকে data বের করা।
    
2. API response থেকে নির্দিষ্ট field নেওয়া।
    
3. Object copy বা nested value দ্রুত পাওয়া।
    
4. Array বা object-এ থেকে নির্দিষ্ট data extract করা।
    

---

## **Types / Variations:**

---

### **1. Type-1: Array Destructuring**

##### Definition:

Array Destructuring হলো array থেকে মানগুলো ভ্যারিয়েবলে অ্যাসাইন করার shorthand পদ্ধতি।

##### Syntax:

```javascript
const [var1, var2, var3] = array;
```

##### Explanation:

এটি array-এর index অনুযায়ী মান অ্যাসাইন করে।  
অর্থাৎ, প্রথম মান প্রথম ভ্যারিয়েবলে, দ্বিতীয় মান দ্বিতীয় ভ্যারিয়েবলে ইত্যাদি।

##### examples:

```javascript
const colors = ["red", "green", "blue"];
const [first, second, third] = colors;
console.log(first, second, third); // Output: red green blue

// Skipping values
const [a, , c] = [10, 20, 30];
console.log(a, c); // Output: 10 30

// Default values
const [x = 1, y = 2, z = 3] = [5];
console.log(x, y, z); // Output: 5 2 3

// Swapping variables
let p = 10, q = 20;
[p, q] = [q, p];
console.log(p, q); // Output: 20 10
```

##### Explanation:

- **Skipping values**: কমার মাধ্যমে কিছু মান বাদ দেওয়া যায়।
    
- **Default values**: যদি কোনো মান undefined হয়, default মান ব্যবহার হয়।
    
- **Swapping variables**: আলাদা কোনো temp variable ছাড়াই মান অদলবদল করা যায়।
    

##### Use Case:

- Array data থেকে নির্দিষ্ট মান নেওয়া।
    
- Function থেকে multiple return value handle করা।
    
- Temporary variable ছাড়া swapping করা।
    

##### Error Cases / Common Mistakes ⚠️:

- যদি ডান পাশে array না থাকে, TypeError হতে পারে।
    
    ```javascript
    const [a, b] = null; // ❌ TypeError
    ```
    
- ভ্যারিয়েবল সংখ্যা বেশি হলে extra variable-এ undefined আসে।
    

##### Best Practice ⚡:

- Default value ব্যবহার করা উচিত যখন undefined আসার সম্ভাবনা থাকে।
    
- Skipping values ব্যবহার করলে readability ঠিক রাখা উচিত।
    

---

### **2. Type-2: Object Destructuring**

##### Definition:

Object Destructuring হলো object-এর property থেকে মান বের করে একই নামে ভ্যারিয়েবলে অ্যাসাইন করার পদ্ধতি।

##### Syntax:

```javascript
const {prop1, prop2} = object;
```

##### Explanation:

এটি object-এর property name অনুযায়ী মান অ্যাসাইন করে।  
Variable name এবং property name এক হতে হবে।

##### examples:

```javascript
const user = { name: "Saiful", age: 25, country: "Bangladesh" };
const { name, age } = user;
console.log(name, age); // Output: Saiful 25

// Default values
const { city = "Dhaka" } = user;
console.log(city); // Output: Dhaka

// Renaming variable
const { name: userName, age: userAge } = user;
console.log(userName, userAge); // Output: Saiful 25

// Nested destructuring
const student = {
  info: { id: 1, name: "Rafi" },
  scores: { math: 90, english: 85 }
};
const {
  info: { name: studentName },
  scores: { math }
} = student;
console.log(studentName, math); // Output: Rafi 90
```

##### Explanation:

- Default value তখন কাজ করে যখন property undefined থাকে।
    
- Property-কে অন্য নামে rename করা যায় (`name: userName`)।
    
- Nested destructuring-এর মাধ্যমে inner object থেকে মান নেওয়া যায়।
    

##### Use Case:

1. API response থেকে data extract করা।
    
2. Component props (React/Vue)-এ data destructure করা।
    
3. Configuration object থেকে নির্দিষ্ট field নেওয়া।
    

##### Error Cases / Common Mistakes ⚠️:

- Object undefined হলে destructure করতে গেলে error হয়।
    
    ```javascript
    const { x } = undefined; // ❌ TypeError
    ```
    
- Variable নাম ভুল দিলে undefined পাওয়া যায়।
    

##### Best Practice ⚡:

- Nested destructuring-এর আগে optional chaining (`?.`) ব্যবহার করা উচিত।
    
    ```javascript
    const { name } = user?.info || {};
    ```
    
- Default মান ব্যবহার করে কোড সেফ করা উচিত।
    

---

### **3. Type-3: Function Parameter Destructuring**

##### Definition:

Function-এর parameter হিসেবে object বা array destructure করে সরাসরি মান নেওয়া যায়।

##### Syntax:

```javascript
function display({name, age}) {
  console.log(name, age);
}
```

##### Explanation:

Function কল করার সময় সরাসরি object বা array পাস করলে তার ভেতরকার property গুলো destructure করে ব্যবহার করা যায়।

##### examples:

```javascript
// Object destructuring in function parameter
function printUser({ name, age }) {
  console.log(`Name: ${name}, Age: ${age}`);
}
const user = { name: "Saiful", age: 25 };
printUser(user); // Output: Name: Saiful, Age: 25

// Array destructuring in function parameter
function printCoords([x, y]) {
  console.log(`X: ${x}, Y: ${y}`);
}
printCoords([10, 20]); // Output: X: 10, Y: 20

// Default values in function parameter
function greet({ name = "Guest" }) {
  console.log(`Hello, ${name}`);
}
greet({}); // Output: Hello, Guest
```

##### Explanation:

- Object destructuring-এর মাধ্যমে parameter থেকে সরাসরি field নেওয়া যায়।
    
- Default value function parameter-এর মধ্যেই দেওয়া যায়।
    

##### Use Case:

1. API বা form data থেকে নির্দিষ্ট মান function-এর মধ্যে নেওয়া।
    
2. Optional parameter handle করা।
    
3. React props বা configuration object থেকে value পাওয়া।
    

##### Error Cases / Common Mistakes ⚠️:

- যদি function-এ object পাস না করা হয়, তাহলে error হবে।
    
    ```javascript
    printUser(); // ❌ TypeError
    ```
    

##### Best Practice ⚡:

- Default parameter (`{}`) ব্যবহার করা উচিত error এড়াতে।
    
    ```javascript
    function printUser({ name, age } = {}) { ... }
    ```
    

---

## **Summary:**

|Type|Description|Example|
|---|---|---|
|**Array Destructuring**|Array থেকে মান বের করা|`const [a, b] = [10, 20];`|
|**Object Destructuring**|Object property থেকে মান বের করা|`const {name, age} = user;`|
|**Function Parameter Destructuring**|Function parameter থেকেই destructure করা|`function greet({name}) {}`|

**Key Points:**

- Destructuring কোডকে সংক্ষিপ্ত, readable ও cleaner করে।
    
- Default value undefined হলে fallback হিসেবে কাজ করে।
    
- Nested structure থেকেও মান বের করা যায়।
    
- Object destructuring property name অনুযায়ী কাজ করে।
    
- Optional chaining (`?.`) ও default parameter destructuring-এ সবচেয়ে নিরাপদ পদ্ধতি।
    

---

তুমি কি পরের টপিক হিসেবে **Spread Operator (...)** নিতে চাও, নাকি **Rest Parameter** দিয়ে শুরু করবো?
