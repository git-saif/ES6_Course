##### **Definition:**

`for...of` হলো ES6-এর একটি **iterable loop**, যা **array, string, map, set, NodeList** ইত্যাদি iterable object-এর উপর সহজে iterate করতে ব্যবহৃত হয়।  
এটি প্রতিবার iteration-এ iterable object-এর **actual value** return করে (index নয়)।

---

##### **Syntax:**

```javascript
for (let variable of iterable) {
    // code to execute
}
```

---

##### **Explanation:**

- `for...of` iterable object-এর প্রতিটি element-এর মান access করতে ব্যবহৃত হয়।
- এটি **values iterate** করে (যেখানে `for...in` keys iterate করে)।
- শুধুমাত্র iterable object-এর সাথেই কাজ করে (যেমন Array, String, Map, Set, Arguments, ইত্যাদি)।

---

##### **Examples:**

```javascript
// Example 1: Array
const numbers = [10, 20, 30];
for (const num of numbers) {
  console.log(num);
}
// Output:
// 10
// 20
// 30

// Example 2: String
for (const char of "Saiful") {
  console.log(char);
}
// Output: S a i f u l

// Example 3: Set
const fruits = new Set(["apple", "banana", "mango"]);
for (const fruit of fruits) {
  console.log(fruit);
}
// Output: apple banana mango

// Example 4: Map
const user = new Map([
  ["name", "Saiful"],
  ["age", 25],
]);
for (const [key, value] of user) {
  console.log(`${key}: ${value}`);
}
// Output:
// name: Saiful
// age: 25
```

---

##### **Explanation:**

- `for...of` প্রতিটি iteration-এ iterable object থেকে পরবর্তী value নেয়।
- Array বা String হলে value মানে হচ্ছে প্রতিটি item/character।
- Map বা Set হলে এটি key-value বা unique value pair প্রদান করে।

---

##### **Use Case:**

1. Array, String, Set, Map-এর উপর iterate করা।
2. Readable ও concise iteration লেখার জন্য।
3. যখন শুধুমাত্র **value দরকার**, index না।
4. Complex loops (like nested arrays) সহজে লেখা যায়।

---

## **Types / Variations:**

---

### **1. Type-1: for...of with Array**

##### **Definition:**

Array-এর প্রতিটি element iterate করার জন্য ব্যবহৃত হয়।

##### **Syntax:**

```javascript
for (let element of array) {
  // code
}
```

##### **Examples:**

```javascript
const nums = [1, 2, 3];
for (let n of nums) {
  console.log(n * 2);
}
// Output: 2, 4, 6
```

##### **Explanation:**

প্রতিটি iteration-এ array-এর value পাওয়া যায়, index নয়।

##### **Use Case:**

- Array-এর value process করা
- Summation, filtering, transformation

##### **Error Cases / Common Mistakes ⚠️:**

- Non-iterable object দিলে `TypeError` হয়

```javascript
const obj = { a: 1, b: 2 };
for (let x of obj) { } // ❌ TypeError
```

##### **Best Practice ⚡:**

- Array iteration-এর জন্য সর্বাধিক readable loop হলো `for...of`।

---

### **2. Type-2: for...of with String**

##### **Definition:**

String-এর প্রতিটি character iterate করতে ব্যবহৃত হয়।

##### **Syntax:**

```javascript
for (let char of string) {
  // code
}
```

##### **Examples:**

```javascript
for (let letter of "HELLO") {
  console.log(letter);
}
// Output: H E L L O
```

##### **Explanation:**

প্রতিটি iteration-এ string-এর একেকটি character return করে।

##### **Use Case:**

- Character checking, counting
- Word manipulation

##### **Error Cases / Common Mistakes ⚠️:**

- String না হলে error হবে।

##### **Best Practice ⚡:**

- String parsing বা character-level কাজের জন্য `for...of` খুব কার্যকর।

---

### **3. Type-3: for...of with Map / Set**

##### **Definition:**

Map বা Set-এর element iterate করার জন্য ব্যবহৃত হয়।

##### **Syntax:**

```javascript
for (let [key, value] of map) {
  // code
}
```

##### **Examples:**

```javascript
const map = new Map([
  ["name", "Saiful"],
  ["age", 25],
]);

for (const [k, v] of map) {
  console.log(`${k}: ${v}`);
}
// Output:
// name: Saiful
// age: 25
```

##### **Explanation:**

Map এর ক্ষেত্রে প্রতিটি iteration-এ key-value pair পাওয়া যায়।  
Set এর ক্ষেত্রে শুধুমাত্র value পাওয়া যায়।

##### **Use Case:**

- Key-value data process করা
- Unique list iterate করা

##### **Error Cases / Common Mistakes ⚠️:**

- Map বা Set destructuring ভুল করলে undefined আসবে।

##### **Best Practice ⚡:**

- Always destructure `[key, value]` in Map iteration for clarity.

---

## **Comparison: for...of vs for...in**

|Feature|for...of|for...in|
|---|---|---|
|Iterates over|Values|Keys (or indexes)|
|Works with|Iterable objects|Objects|
|Suitable for|Arrays, Strings, Maps, Sets|Plain objects|
|Example|`for (x of arr)`|`for (x in obj)`|

---

## **Summary:**

- **`for...of`** ব্যবহার করতে হবে **iterable object** iterate করার সময়।
- এটি **value iterate করে**, index নয়।
- Non-iterable object দিলে `TypeError` হবে।
- Array, String, Map, Set, NodeList ইত্যাদি জন্য এটি সবচেয়ে readable loop।
- `for...of` = cleaner + concise + error-free iteration।

---
