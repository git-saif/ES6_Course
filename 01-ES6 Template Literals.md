##### Definition:

Template Literals হলো JavaScript-এর একটি ES6 ফিচার, যা ব্যাকটিক (`` ` ``) ব্যবহার করে স্ট্রিং লেখার সুযোগ দেয়। এটি মাল্টি-লাইন স্ট্রিং, স্ট্রিং ইন্টারপোলেশন, এবং embedded expression ব্যবহারের মাধ্যমে আরও সুবিধাজনকভাবে স্ট্রিং তৈরি করতে সাহায্য করে।

---
##### Syntax:

```javascript
`string text`
`string text ${expression} string text`
```

---

##### Explanation:

Template Literals-এর মাধ্যমে স্ট্রিং-এর মধ্যে **variable**, **expression**, এমনকি **function call** যুক্ত করা যায় `${}` সিনট্যাক্স ব্যবহার করে।  এটি সাধারণ single (' ') বা double (" ") quote-এর পরিবর্তে ব্যাকটিক (`` ` ``) দিয়ে ঘেরা হয়।  
Template Literals মাল্টি-লাইন স্ট্রিংও সমর্থন করে, অর্থাৎ নতুন লাইনের জন্য `\n` ব্যবহার করতে হয় না।

---

##### examples:

```javascript
// Basic example
const name = "Saiful";
const message = `Hello, ${name}! Welcome to ES6.`;
console.log(message); // Output: Hello, Saiful! Welcome to ES6.

// Multi-line example
const paragraph = `
This is line 1.
This is line 2.
This is line 3.
`;
console.log(paragraph);

// Expression interpolation
const a = 10;
const b = 20;
console.log(`Sum: ${a + b}`); // Output: Sum: 30

// Function call inside template literal
function greet() {
  return "Good Morning";
}
console.log(`Message: ${greet()} Saiful`); // Output: Message: Good Morning Saiful
```

---

##### Explanation:

উপরের উদাহরণগুলোতে দেখা যাচ্ছে,

- `${}` এর মাধ্যমে variable এবং expression ব্যবহার করা হচ্ছে।
- ব্যাকটিক ( ) ব্যবহার করে multiline string তৈরি করা যাচ্ছে।
- function call-এর ফলাফলও `${}` এর মাধ্যমে যুক্ত করা সম্ভব।

---

##### Use Case:

Template Literals সাধারণত নিচের ক্ষেত্রে বেশি ব্যবহৃত হয়:

1. **Dynamic string তৈরি করতে**, যেখানে variable বা expression প্রয়োজন হয়।
2. **HTML Template তৈরি করতে**, যেমন JavaScript-এর মধ্যে HTML structure dynamically যুক্ত করা।
3. **Logging এবং Debugging**-এর সময় complex data সহজভাবে প্রদর্শন করতে।
4. **String formatting** সহজ করার জন্য।

---

## **Types / Variations:**

### **1. Type-1: Basic Template Literal**

##### Definition:

এটি Template Literal-এর সবচেয়ে সাধারণ রূপ, যেখানে শুধু ব্যাকটিক ব্যবহার করে স্ট্রিং লেখা হয়।

##### Syntax:

```javascript
`Hello World`
```

##### Explanation:

এখানে কোনো `${}` ব্যবহার করা হয়নি, শুধু ব্যাকটিক (`) ব্যবহার করা হয়েছে।  
এটি সাধারণ স্ট্রিং-এর মতো কাজ করে, তবে মাল্টি-লাইন সাপোর্ট করে।

##### examples:

```javascript
const text = `
Line 1
Line 2
Line 3
`;
console.log(text);
```

##### Explanation:

এইভাবে ব্যাকটিক ব্যবহার করে একাধিক লাইনে স্ট্রিং লেখা যায়, যেখানে `\n` ব্যবহার করার দরকার নেই।

##### Use Case:

মাল্টি-লাইন মেসেজ, HTML টেমপ্লেট, লগ মেসেজ ইত্যাদি লেখার ক্ষেত্রে এটি ব্যবহার করা হয়।

##### Error Cases / Common Mistakes ⚠️:

- ব্যাকটিক () ভুলে গেলে SyntaxError হতে পারে।
- কিছু সময় `${}` লিখে variable না দিলে “unexpected token” error হয়।

##### Best Practice ⚡:

- সর্বদা ব্যাকটিক (`) বন্ধ আছে কি না তা নিশ্চিত করা উচিত।
- বড় HTML বা template string তৈরির সময় indentation ঠিক রাখা উচিত।

---

### **2. Type-2: String Interpolation**

##### Definition:

String Interpolation মানে `${}` এর মাধ্যমে dynamic value (variable, expression, function call) string-এর মধ্যে ব্যবহার করা।

##### Syntax:

```javascript
`Some text ${variableOrExpression} more text`
```

##### Explanation:

`${}` এর ভিতরে যেকোনো valid JavaScript expression রাখা যায়, যা evaluate হয়ে স্ট্রিং-এর মধ্যে বসে যায়।

##### examples:

```javascript
const name = "Saiful";
const age = 25;
const info = `My name is ${name} and I am ${age} years old.`;
console.log(info);

const total = `5 + 3 = ${5 + 3}`;
console.log(total);

const greet = name => `Hello, ${name.toUpperCase()}!`;
console.log(greet("world"));
```

##### Explanation:

- `${}` এর মাধ্যমে variable এবং expression একত্রে লেখা যায়।
- Expression dynamic ভাবে evaluate হয়।

##### Use Case:

Dynamic text, UI text rendering, template-based data binding ইত্যাদিতে ব্যবহৃত হয়।

##### Error Cases / Common Mistakes ⚠️:

- `${}` এর ভিতরে invalid expression দিলে runtime error হয়।
- undefined বা null value `${}` এ দিলে output “undefined” বা “null” হিসেবে দেখা যায়।

##### Best Practice ⚡:

- `${}` এর ভিতরে শুধু প্রয়োজনীয় expression ব্যবহার করা উচিত।
- জটিল expression আগে variable-এ রেখে পরে interpolate করা ভালো।

---

### **3. Type-3: Tagged Template Literals**

##### Definition:

Tagged Template Literal হলো এমন একটি ফিচার, যেখানে একটি function template literal প্রসেস করে কাস্টম আউটপুট তৈরি করে।

##### Syntax:

```javascript
function tag(strings, ...values) {
  // custom logic
}
tag`Hello ${name}, you have ${messages} messages.`;
```

##### Explanation:

Tagged Template Literal ব্যবহার করলে, template literal পার্স করার আগে function call হয়।  
এই function তিনটি জিনিস পায়:

1. **strings** — literal অংশগুলো array হিসেবে।
2. **values** — `${}` এর expression গুলোর value array হিসেবে।
3. এগুলোর মাধ্যমে custom format, escaping, translation, ইত্যাদি করা যায়।

##### examples:

```javascript
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => {
    return result + str + (values[i] ? `**${values[i]}**` : "");
  }, "");
}

const name = "Saiful";
const task = "ES6 Notes";
console.log(highlight`Hello ${name}, complete your ${task} soon!`);
```

**Output:**

```
Hello **Saiful**, complete your **ES6 Notes** soon!
```

##### Explanation:

উদাহরণে, `highlight` ফাংশন template literal-এর value গুলোকে bold করে দিচ্ছে।  
এটি custom formatting-এর এক দুর্দান্ত উদাহরণ।

##### Use Case:

1. Custom string formatting
2. Security purpose (e.g. escaping HTML to prevent XSS)
3. Localization (translate strings dynamically)
4. Markdown-like formatting

##### Error Cases / Common Mistakes ⚠️:

- Function return না করলে `undefined` দেখা যায়।
- ভুলভাবে arguments handle করলে string অসম্পূর্ণ হতে পারে।

##### Best Practice ⚡:

- Tagged templates ব্যবহার করার সময় side-effect এড়িয়ে চলা উচিত।
- জটিল logic আলাদা utility function হিসেবে রাখা উচিত।

---

## **Summary:**

|Feature|Description|Example|
|---|---|---|
|**Basic Template Literal**|ব্যাকটিক দিয়ে মাল্টি-লাইন স্ট্রিং তৈরি|`` `Hello World` ``|
|**String Interpolation**|`${}` এর মাধ্যমে variable/expression যোগ করা|`` `Hi ${name}` ``|
|**Tagged Template**|Function দিয়ে template প্রসেস করা|`tag\`Hello ${name}``|

**Key Points:**

- Template Literals dynamic string তৈরি করার জন্য শক্তিশালী টুল।
- `${}` এর মধ্যে expression রাখা যায়।
- Tagged Template Literal কাস্টম স্ট্রিং প্রসেসিং-এর সুযোগ দেয়।
- কোডের পাঠযোগ্যতা (readability) বাড়ায় ও string concatenation এর প্রয়োজন কমায়।

---
