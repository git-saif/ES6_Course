##### **Definition:**

**Object Shorthand** হলো ES6 feature যা object creation কে **concise ও readable** করে।

- Property shorthand
- Method shorthand
- Computed property names

---
##### **Syntax:**

```javascript
// Property shorthand
const name = "Saiful";
const obj = { name };

// Method shorthand
const obj2 = {
  greet() {
    console.log("Hello");
  }
};

// Computed property
const key = "age";
const obj3 = {
  [key]: 25
};
```

---
##### **Explanation:**

- **Property Shorthand:** variable name same থাকলে `{name: name}` → `{name}`
- **Method Shorthand:** function declaration কম করে লেখা যায় `{ greet() {} }`
- **Computed Property:** dynamic key use করা যায় `[variable]`

---
##### **Examples:**

```javascript
// Property shorthand
const firstName = "Saiful";
const lastName = "Islam";
const user = { firstName, lastName };
console.log(user); // { firstName: "Saiful", lastName: "Islam" }

// Method shorthand
const calculator = {
  add(a, b) { return a + b; },
  subtract(a, b) { return a - b; }
};
console.log(calculator.add(5, 3)); // 8

// Computed property
const prop = "score";
const player = { [prop]: 100 };
console.log(player); // { score: 100 }
```

---
##### **Use Case:**

1. Object initialization সহজ ও readable করা
2. Method define করার compact way
3. Dynamic property key define করা

---
## **Types / Variations:**

---

### **1. Type-1: Property Shorthand**

##### **Definition:**

Variable নাম ও property নাম same থাকলে shorthand ব্যবহার।

##### **Syntax:**

```javascript
const x = 10;
const obj = { x };
```

##### **Examples:**

```javascript
const name = "Saiful";
const age = 25;
const user = { name, age };
console.log(user); // { name: "Saiful", age: 25 }
```

##### **Explanation:**

- `{name: name, age: age}` লিখার প্রয়োজন নেই
- Code compact ও readable হয়

##### **Use Case:**

- Object initialization
- Return object from function

##### **Error Cases / Common Mistakes ⚠️:**

- Variable undefined → runtime error

```javascript
const obj = { firstName }; // ❌ if firstName not defined
```

##### **Best Practice ⚡:**

- Use shorthand for cleaner object initialization

---
### **2. Type-2: Method Shorthand**

##### **Definition:**

Object method declare করার compact form।

##### **Syntax:**

```javascript
const obj = {
  methodName() { ... }
};
```

##### **Examples:**

```javascript
const person = {
  name: "Saiful",
  greet() { console.log(`Hello, ${this.name}`); }
};
person.greet(); // Hello, Saiful
```

##### **Explanation:**

- `greet: function() {}` এর জায়গায় সরাসরি method লিখা যায়
- `this` context preserve হয়

##### **Use Case:**

- Object behavior define
- Cleaner methods declaration

##### **Error Cases / Common Mistakes ⚠️:**

- Arrow function shorthand ব্যবহার করলে `this` bind হয় না

##### **Best Practice ⚡:**

- Object method → normal function shorthand
- Arrow function → use carefully inside object

---
### **3. Type-3: Computed Property Names**

##### **Definition:**

Dynamic property key ES6 object shorthand দিয়ে set করা।

##### **Syntax:**

```javascript
const key = "dynamicKey";
const obj = { [key]: value };
```

##### **Examples:**

```javascript
const prop = "score";
const player = { [prop]: 100 };
console.log(player); // { score: 100 }

const suffix = "Name";
const user = { ["first" + suffix]: "Saiful" };
console.log(user); // { firstName: "Saiful" }
```

##### **Explanation:**

- Square brackets `[ ]` use করে key runtime-এ generate করা যায়
- Useful for dynamic data keys

##### **Use Case:**

- Dynamic API response
- Property mapping
- Computed keys from variables

##### **Error Cases / Common Mistakes ⚠️:**

- Bracket miss → property not computed
- Duplicate key → overwritten

##### **Best Practice ⚡:**

- Dynamic keys only when necessary
- Avoid unnecessary complexity

---
## **Summary Table:**

| Shorthand Type | Syntax         | Example           | Use Case        |
| -------------- | -------------- | ----------------- | --------------- |
| Property       | `{ varName }`  | `{ name, age }`   | Object init     |
| Method         | `method(){}`   | `{ greet(){}}`    | Object behavior |
| Computed       | `[key]: value` | `{ [prop]: 100 }` | Dynamic keys    |

---
### **Key Points:**

- Shorthand = concise, readable object
- Property → variable name same
- Method → compact function
- Computed → dynamic property key
- Use all three together for clean ES6 code
---
