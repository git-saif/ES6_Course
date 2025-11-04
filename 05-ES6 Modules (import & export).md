### **Definition:**

**ES6 Modules** হলো JavaScript-এর একটি system যার মাধ্যমে কোডকে ছোট ছোট, reusable অংশে ভাগ করা যায়।  একটি ফাইল থেকে অন্য ফাইলে কোড (function, class, variable ইত্যাদি) **export/import** করে ব্যবহার করা যায়। এটি কোডকে modular, clean এবং maintainable রাখে।

---
### **Syntax Overview:**

```javascript
// Export
export const name = "Saiful";
export function greet() { console.log("Hello"); }

// Import
import { name, greet } from './module.js';
```

---
### **Explanation:**

- **`export`**: কোনো ফাইল থেকে কোডকে বাইরে পাঠানোর জন্য।
- **`import`**: অন্য ফাইল থেকে কোড এনে ব্যবহার করার জন্য।
- প্রতিটি module defaultভাবে আলাদা scope পায় (global নয়)।

---
### **Example:**

#### 📁 `module.js`

```javascript
export const PI = 3.1416;

export function add(a, b) {
  return a + b;
}
```
#### 📁 `main.js`

```javascript
import { PI, add } from './module.js';

console.log(PI);        // 3.1416
console.log(add(5, 10)); // 15
```

#### 📁 `index.html`

```html
   <script src="main.js" type="module"></script>
```

---
### **Use Case:**

1. কোডকে ছোট reusable অংশে ভাগ করা।
2. বড় প্রজেক্টে dependency আলাদা রাখা।
3. Maintainable ও scalable কোড structure তৈরি করা।

---
## **Types of Module Export / Import**

---
### **1. Named Export**

##### **Definition:**

একটি ফাইল থেকে একাধিক variable, function, বা class export করা যায়।  
import করার সময় নাম একই রাখতে হয়।
##### **Syntax:**

```javascript
// Export
export const name = "Saiful";
export function sayHello() { console.log("Hello!"); }

// Import
import { name, sayHello } from './file.js';
```
##### **Explanation:**

`{ }` এর ভিতরের নাম অবশ্যই export করা variable/function-এর নামের সাথে মিলতে হবে।

##### **Examples:**

```javascript
// math.js
export const add = (a, b) => a + b;
export const sub = (a, b) => a - b;

// app.js
import { add, sub } from './math.js';

console.log(add(5, 2)); // 7
console.log(sub(5, 2)); // 3
```

##### **Use Case:**

যখন একাধিক value export করতে হবে এবং তাদের নাম ধরে access করা হবে।

##### **Common Mistake ⚠️**

নাম mismatch হলে error:

```javascript
import { adds } from './math.js'; // ❌ adds not exported
```

##### **Best Practice ⚡**

- একই ফাইলের related function/constant গুলো একসাথে named export করা।
- নাম meaningful রাখা।

---

### **2. Default Export**

##### **Definition:**

প্রতি ফাইলে শুধুমাত্র **একটি default export** থাকতে পারে।  
Import করার সময় যেকোনো নাম ব্যবহার করা যায়।

##### **Syntax:**

```javascript
// Export
export default function greet() {
  console.log("Hello Default Export!");
}

// Import
import myFunc from './file.js';
myFunc(); // Hello Default Export!
```

##### **Explanation:**

Default export এর জন্য `{ }` ব্যবহার করতে হয় না।

##### **Examples:**

```javascript
// user.js
export default class User {
  constructor(name) {
    this.name = name;
  }
  show() {
    console.log(`User: ${this.name}`);
  }
}

// app.js
import UserClass from './user.js';
const u = new UserClass("Saiful");
u.show(); // User: Saiful
```

##### **Use Case:**

যখন একটি ফাইল থেকে একটি মূল জিনিস export করা হয় (যেমন main function, class ইত্যাদি)।

##### **Error Cases ⚠️**

- একাধিক default export দেওয়া যায় না।

```javascript
    export default a;
    export default b; // ❌ SyntaxError
```


##### **Best Practice ⚡**

- Default export শুধু “একটি primary item” এর জন্য ব্যবহার করা উচিত।
- Named export + Default export একসাথে ব্যবহার করা যায়।

---

### **3. Mixed Export (Named + Default)**

##### **Definition:**

একই ফাইলে Default ও Named Export একসাথে দেওয়া যায়।

##### **Syntax:**

```javascript
export const version = "1.0";
export default function greet() {
  console.log("Hello!");
}
```

##### **Import Example:**

```javascript
import greet, { version } from './file.js';
greet(); // Hello!
console.log(version); // 1.0
```

##### **Explanation:**

Default item কে `{}` ছাড়া import করতে হয়, আর named item গুলো `{}` এর মধ্যে রাখতে হয়।

##### **Use Case:**

যখন module এ একটি main export এবং কিছু helper থাকে।

---
### **4. Import All (`* as`)**

##### **Definition:**

একটি module-এর সব export একসাথে একটি namespace হিসেবে import করা যায়।

##### **Syntax:**

```javascript
import * as MathUtils from './math.js';
```

##### **Examples:**

```javascript
// math.js
export const add = (a, b) => a + b;
export const sub = (a, b) => a - b;

// app.js
import * as MathUtils from './math.js';
console.log(MathUtils.add(2,3)); // 5
console.log(MathUtils.sub(5,2)); // 3
```

##### **Explanation:**

`MathUtils` এখন পুরো module object হিসেবে কাজ করে।

##### **Use Case:**

যখন অনেক export আছে, কিন্তু সব একসাথে namespace আকারে ব্যবহার করতে হয়।

##### **Best Practice ⚡**

Namespace নাম সবসময় PascalCase বা descriptive হওয়া উচিত।

---

### **5. Re-export (Export from another file)**

##### **Definition:**

এক module থেকে অন্য module এর export পুনরায় export করা যায়।

##### **Syntax:**

```javascript
export { add, sub } from './math.js';
```

##### **Example:**

```javascript
// math.js
export const add = (a,b) => a+b;
export const sub = (a,b) => a-b;

// utils.js
export { add, sub } from './math.js';

// app.js
import { add } from './utils.js';
console.log(add(10, 5)); // 15
```

##### **Explanation:**

এটি “barrel” pattern নামে পরিচিত, যেখানে এক জায়গা থেকে সব export centralized করা হয়।

##### **Use Case:**

বড় প্রজেক্টে একাধিক module একত্রে export করা।

---
## **6. Dynamic Import (import())**

##### **Definition:**

ES2020 থেকে JavaScript এ **dynamic import()** এসেছে।  
এর মাধ্যমে runtime-এ asynchronously module load করা যায়।

##### **Syntax:**

```javascript
import('./module.js').then(module => {
  module.greet();
});
```

##### **Example (Async/Await):**

```javascript
async function loadMath() {
  const math = await import('./math.js');
  console.log(math.add(5, 10)); // 15
}
loadMath();
```

##### **Use Case:**

- Lazy loading modules (React, Vue ইত্যাদিতে ব্যবহৃত)
- Performance optimization

##### **Best Practice ⚡**

- শুধুমাত্র প্রয়োজনীয় সময় module load করো।
- try/catch দিয়ে error handle করো।

---

## **Summary Table:**

|Type|Syntax|Import Style|Multiple Exports|Notes|
|---|---|---|---|---|
|**Named Export**|`export const a = 1;`|`import { a } from './file.js'`|✅|Must use same name|
|**Default Export**|`export default a;`|`import x from './file.js'`|❌|Only one per file|
|**Mixed Export**|`export default + export const`|`import def, {a}`|✅|Best of both worlds|
|**Import All**|`import * as obj`|Access by `obj.name`|✅|Useful for grouping|
|**Re-export**|`export { name } from`|Normal import|✅|Combine modules|
|**Dynamic Import**|`import('./file.js')`|Promise-based|✅|Lazy loading|

---

### **Common Mistakes ⚠️**

1. `.js` extension না দিলে browser import error দেয়।
2. Default export-এর নাম যেকোনো হতে পারে, কিন্তু named export-এর নাম পরিবর্তন করা যায় না (unless alias ব্যবহার করা হয়):

```javascript
    import { add as plus } from './math.js';
```

3. Node.js এ module system চালাতে হলে `"type": "module"` দিতে হয় `package.json` এ।

---
### **Best Practices ⚡**

✅ প্রতিটি module শুধু এক কাজ করুক।  
✅ Related function/constant এক ফাইলে রাখা।  
✅ Default export কম ব্যবহার করা (explicit named ভালো)।  
✅ Dynamic import ব্যবহার করা বড় প্রজেক্টে performance optimization এর জন্য।

---
