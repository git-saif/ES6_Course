# **ES6 Spread & Rest Operator**

---

##### Definition:

ES6-এ **Spread (`...`)** এবং **Rest (`...`)** — দুইটি অপারেটর একই “তিনটি ডট” (`...`) ব্যবহার করলেও কাজের দিক থেকে সম্পূর্ণ আলাদা।

- **Spread Operator (`...`)**: iterable (যেমন array, object, string) কে “expand” বা “unpack” করে।
    
- **Rest Operator (`...`)**: function parameter বা destructuring-এর সময় একাধিক মানকে “collect” করে একটি array-তে রাখে।
    

---

##### Syntax:

```javascript
// Spread
const newArray = [...oldArray];
const newObject = { ...oldObject };

// Rest
function sum(...numbers) { return numbers.reduce((a,b)=>a+b,0); }
```

---

##### Explanation:

- Spread Operator ডাটা **ভেঙে ফেলে (expand)**।
    
- Rest Operator ডাটা **জমা করে (collect)**।
    

তারা দুজন একরকম দেখতে হলেও তাদের ব্যবহারের প্রেক্ষাপট আলাদা।

---

##### examples:

```javascript
// Spread Example
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];
console.log(arr2); // [1, 2, 3, 4, 5]

// Rest Example
function addAll(...nums) {
  return nums.reduce((sum, n) => sum + n, 0);
}
console.log(addAll(1, 2, 3, 4)); // 10
```

---

##### Explanation:

Spread Operator array/object-এর মান “ছড়িয়ে দেয়”, আর Rest Operator parameter বা variable-এ “সংগ্রহ করে” রাখে।  
একজন unpack করে, অন্যজন pack করে।

---

##### Use Case:

1. Array/Object clone করা বা merge করা (Spread)।
    
2. Function parameter হিসেবে যেকোনো সংখ্যক argument handle করা (Rest)।
    
3. Destructuring-এর সময় কিছু মান আলাদা রেখে বাকিগুলো একত্রে নেওয়া।
    

---

## **Types / Variations:**

---

### **1. Type-1: Spread Operator (`...`)**

##### Definition:

Spread Operator হলো এমন একটি অপারেটর যা **iterable data structure (array, string, object)** কে “unpack” করে individual element বা property আকারে প্রকাশ করে।

##### Syntax:

```javascript
[...iterable]
{ ...object }
```

##### Explanation:

যখন কোনো iterable কে নতুন array বা object-এ কপি করা হয়, তখন Spread Operator ব্যবহার করা হয়।  
এটি shallow copy তৈরি করে, অর্থাৎ reference type ভেতরে একই object-কে নির্দেশ করে।

##### examples:

```javascript
// Array cloning
const numbers = [1, 2, 3];
const clone = [...numbers];
console.log(clone); // [1, 2, 3]

// Array merging
const a = [1, 2];
const b = [3, 4];
const merged = [...a, ...b];
console.log(merged); // [1, 2, 3, 4]

// String to array
const str = "Hi";
const chars = [...str];
console.log(chars); // ['H', 'i']

// Object cloning
const user = { name: "Saiful", age: 25 };
const cloneUser = { ...user };
console.log(cloneUser); // { name: "Saiful", age: 25 }

// Object merging
const details = { city: "Dhaka" };
const mergedUser = { ...user, ...details };
console.log(mergedUser); // { name: "Saiful", age: 25, city: "Dhaka" }
```

##### Explanation:

- **Array clone**: নতুন array তৈরি হয়।
    
- **Array merge**: একাধিক array একত্রে যুক্ত করা যায়।
    
- **Object clone/merge**: Object copy বা merge করা যায়।
    
- **String to array**: প্রতিটি character আলাদা element হয়।
    

##### Use Case:

1. Array বা Object কপি করা।
    
2. একাধিক array/object merge করা।
    
3. Function call-এর সময় array expand করা:
    
    ```javascript
    const nums = [1, 2, 3];
    console.log(Math.max(...nums)); // 3
    ```
    

##### Error Cases / Common Mistakes ⚠️:

- Deep copy হয় না, শুধুমাত্র shallow copy হয়।
    
    ```javascript
    const obj = { nested: { a: 1 } };
    const copy = { ...obj };
    copy.nested.a = 999;
    console.log(obj.nested.a); // 999 ❌
    ```
    
- Object spread কেবল plain object-এর জন্য কাজ করে (Map, Set-এর জন্য নয়)।
    

##### Best Practice ⚡:

- Nested data হলে structuredClone() বা lodash ব্যবহার করা উচিত।
    
- Spread Operator read-only data manipulation-এর ক্ষেত্রে সবচেয়ে ভালো।
    

---

### **2. Type-2: Rest Operator (`...`)**

##### Definition:

Rest Operator function parameter বা destructuring context-এ ব্যবহার হয়,  
যেখানে এটি একাধিক মানকে একত্রে **array** বা **object** আকারে সংগ্রহ করে রাখে।

##### Syntax:

```javascript
function func(...args) { }
const [a, ...rest] = [1, 2, 3];
const {x, ...others} = {x:1, y:2, z:3};
```

##### Explanation:

- Function parameter-এ: যেকোনো সংখ্যক argument গ্রহণ করা যায়।
    
- Destructuring-এ: কিছু মান বাদ দিয়ে বাকিগুলো একত্রে নেওয়া যায়।
    

##### examples:

```javascript
// Function Rest Parameter
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}
console.log(sum(10, 20, 30)); // 60

// Array Rest in Destructuring
const [first, ...others] = [1, 2, 3, 4, 5];
console.log(first);  // 1
console.log(others); // [2, 3, 4, 5]

// Object Rest in Destructuring
const user = { name: "Saiful", age: 25, city: "Dhaka" };
const { name, ...info } = user;
console.log(name); // Saiful
console.log(info); // { age: 25, city: "Dhaka" }
```

##### Explanation:

- Function-এ `...numbers` সব argument কে array করে নেয়।
    
- Array বা object destructuring-এ rest অপারেটর বাকিগুলো সংগ্রহ করে রাখে।
    
- সব সময় **শেষে** (at the end) থাকতে হয়।
    

##### Use Case:

1. Unknown number of parameters handle করা।
    
2. Destructuring-এ বাদ দেওয়া মান ছাড়া বাকিগুলো নেওয়া।
    
3. Function-এর মধ্যে arguments dynamicভাবে process করা।
    

##### Error Cases / Common Mistakes ⚠️:

- Rest parameter অবশ্যই **শেষে** থাকতে হবে।
    
    ```javascript
    function wrong(a, ...b, c) {} // ❌ SyntaxError
    ```
    
- এক function-এ একাধিক rest parameter রাখা যায় না।
    
- Destructuring-এ rest variable এর আগে অবশ্যই আলাদা ভ্যারিয়েবল থাকতে হবে।
    

##### Best Practice ⚡:

- Function parameter handle করার সময় arguments অবজেক্ট না ব্যবহার করে rest parameter ব্যবহার করা উচিত।
    
- Rest variable নাম meaningful রাখা উচিত (যেমন `...others`, `...remaining`)।
    

---

### **3. Type-3: Spread & Rest Combined Use**

##### Definition:

অনেক ক্ষেত্রে Spread এবং Rest Operator একসাথে ব্যবহার হয়—এক জায়গায় মান “ছড়ানো” হয়, অন্য জায়গায় “সংগ্রহ” করা হয়।

##### Syntax:

```javascript
function func(a, b, ...rest) {
  const newArray = [...rest];
}
```

##### Explanation:

এখানে rest parameter দিয়ে argument সংগ্রহ করা হয়েছে,  
আর spread operator দিয়ে সেগুলো নতুন array-তে ছড়িয়ে দেওয়া হয়েছে।

##### examples:

```javascript
function combine(first, ...rest) {
  const result = [first, ...rest];
  console.log(result);
}
combine(1, 2, 3, 4); // Output: [1, 2, 3, 4]

// Copy and modify object
const user = { name: "Saiful", age: 25 };
const updatedUser = { ...user, city: "Dhaka" };
console.log(updatedUser); // { name: "Saiful", age: 25, city: "Dhaka" }

// Merge arrays and collect rest
const arr1 = [1, 2];
const arr2 = [3, 4];
const merged = [...arr1, ...arr2];
const [first, ...remaining] = merged;
console.log(first, remaining); // 1 [2, 3, 4]
```

##### Use Case:

1. Function-এ dynamic argument handle করে array/object merge করা।
    
2. ডাটা মডিফাই করার সময় immutability বজায় রাখা।
    
3. React বা modern framework-এ props/object spread বা rest ব্যবহার করা।
    

##### Error Cases / Common Mistakes ⚠️:

- ভুল জায়গায় spread/rest ব্যবহার করলে syntax error হয়।
    
- Object spread করার সময় nested object deep copy হয় না।
    

##### Best Practice ⚡:

- Spread/Rest ব্যবহার করার সময় immutable pattern বজায় রাখতে হবে।
    
- জটিল merge করার সময় shallow copy limitation মাথায় রাখা উচিত।
    

---

## **Summary:**

|Operator|Purpose|Works On|Example|
|---|---|---|---|
|**Spread (`...`)**|ডাটা “ছড়িয়ে” দেয়|Array, Object, String|`const arr2 = [...arr1]`|
|**Rest (`...`)**|একাধিক মান “সংগ্রহ” করে|Function params, Destructuring|`function sum(...nums)`|

**Key Points:**

- Spread = **Unpack / Expand**
    
- Rest = **Pack / Collect**
    
- Spread Operator cloning, merging, এবং function argument এ ব্যবহৃত হয়।
    
- Rest Operator function parameter ও destructuring এ ব্যবহৃত হয়।
    
- তারা দেখতে এক হলেও কাজের ধরন সম্পূর্ণ বিপরীত।
    
- Spread shallow copy করে, deep copy নয়।
    
- Rest parameter সর্বদা function-এর শেষ parameter হিসেবে থাকতে হবে।
    

---

তুমি কি পরের টপিক হিসেবে **Default Parameters** নিতে চাও, নাকি **ES6 Modules (import/export)** শুরু করবো?