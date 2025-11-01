# **ES6 Async/Await**

---

##### **Definition:**

**Async/Await** হলো JavaScript-এর syntax যা Promise-based asynchronous operations কে **synchronous style** এ handle করতে সাহায্য করে।

- `async` keyword দিয়ে function declare করা হয়
    
- `await` keyword দিয়ে Promise resolved হওয়া পর্যন্ত function execution pause করা হয়
    

---

##### **Syntax:**

```javascript
async function functionName() {
  const result = await somePromise();
}
```

---

##### **Explanation:**

- `async function` সবসময় Promise return করে।
    
- `await` শুধুমাত্র async function-এর ভিতরে ব্যবহার করা যায়।
    
- `try/catch` block দিয়ে error handle করা হয়।
    
- কোড readable, linear, এবং callback/then chaining-এর চেয়ে সহজ হয়।
    

---

##### **Examples:**

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("Data Loaded"), 1000);
  });
}

async function loadData() {
  try {
    const data = await fetchData();
    console.log(data); // Data Loaded
  } catch(error) {
    console.error("Error:", error);
  } finally {
    console.log("Operation Completed");
  }
}

loadData();
```

---

##### **Use Case:**

1. API calls (fetch, axios)
    
2. Sequential asynchronous operations
    
3. Handling multiple Promises with readable syntax
    
4. Error handling in async operations
    

---

## **Types / Variations:**

---

### **1. Type-1: Basic Async/Await**

##### **Definition:**

Single async function, awaiting a single Promise.

##### **Syntax:**

```javascript
async function func() {
  const result = await promise;
}
```

##### **Examples:**

```javascript
function getNumber() {
  return new Promise(resolve => setTimeout(() => resolve(42), 500));
}

async function showNumber() {
  const number = await getNumber();
  console.log(number); // 42
}

showNumber();
```

##### **Explanation:**

- Execution pause হয় যতক্ষণ না Promise resolve হয়।
    
- Code readable ও synchronous এর মতো লাগে।
    

##### **Use Case:**

- Single API call or async operation
    

##### **Error Cases / Common Mistakes ⚠️:**

- `await` outside async function ❌
    
- Promise rejected হলে try/catch না থাকলে unhandled rejection
    

##### **Best Practice ⚡:**

- Always wrap await in try/catch
    

---

### **2. Type-2: Sequential Async/Await**

##### **Definition:**

Multiple async operations একের পরে এক execute করা।

##### **Syntax:**

```javascript
async function func() {
  const res1 = await promise1();
  const res2 = await promise2();
}
```

##### **Examples:**

```javascript
function fetchA() {
  return new Promise(resolve => setTimeout(() => resolve("A"), 500));
}
function fetchB() {
  return new Promise(resolve => setTimeout(() => resolve("B"), 300));
}

async function fetchSequence() {
  const a = await fetchA();
  const b = await fetchB();
  console.log(a, b); // A B
}

fetchSequence();
```

##### **Explanation:**

- Sequential, dependent async tasks handle করতে সুবিধা।
    

##### **Use Case:**

- Stepwise operations, where next depends on previous
    

##### **Error Cases / Common Mistakes ⚠️:**

- Sequential operations slower if independent → use Promise.all
    

##### **Best Practice ⚡:**

- Dependent tasks sequential, independent tasks parallel
    

---

### **3. Type-3: Parallel Async/Await (Promise.all)**

##### **Definition:**

Multiple independent Promises একসাথে resolve করা, execution fast করা।

##### **Syntax:**

```javascript
async function func() {
  const [res1, res2] = await Promise.all([promise1(), promise2()]);
}
```

##### **Examples:**

```javascript
function fetch1() { return new Promise(res => setTimeout(() => res(1), 500)); }
function fetch2() { return new Promise(res => setTimeout(() => res(2), 300)); }

async function fetchParallel() {
  const [a, b] = await Promise.all([fetch1(), fetch2()]);
  console.log(a, b); // 1 2
}

fetchParallel();
```

##### **Explanation:**

- Independent async tasks একসাথে run হয় → performance boost
    
- await + Promise.all combination খুব common
    

##### **Use Case:**

- Multiple API calls, independent data fetch
    
- Parallel file read/write
    

##### **Error Cases / Common Mistakes ⚠️:**

- কোনো একটি Promise fail হলে সব fail হয় → consider Promise.allSettled
    

##### **Best Practice ⚡:**

- Independent tasks → Promise.all
    
- Error handling individually না করলে catch use
    

---

### **4. Type-4: Error Handling with Async/Await**

##### **Definition:**

Try/catch block দিয়ে async/await এর error capture করা হয়।

##### **Syntax:**

```javascript
async function func() {
  try {
    const result = await promise();
  } catch(error) {
    console.error(error);
  }
}
```

##### **Examples:**

```javascript
function fetchData() {
  return new Promise((resolve, reject) => setTimeout(() => reject("Failed"), 500));
}

async function load() {
  try {
    const data = await fetchData();
    console.log(data);
  } catch(err) {
    console.error("Error:", err); // Error: Failed
  }
}

load();
```

##### **Explanation:**

- Catch block asynchronous error capture করে
    
- Finally block দিয়ে cleanup করা যায়
    

##### **Use Case:**

- API call fail, network error
    
- Async validation
    

##### **Error Cases / Common Mistakes ⚠️:**

- try/catch miss করলে unhandled rejection
    
- return Promise না করলে async function ফলাফল sync মনে হতে পারে
    

##### **Best Practice ⚡:**

- Always wrap await in try/catch
    
- Finally block use করে cleanup/loader handle করা
    

---

### **5. Type-5: Async Function Returning Value**

##### **Definition:**

Async function সবসময় Promise return করে।

##### **Syntax:**

```javascript
async function func() {
  return value;
}
```

##### **Examples:**

```javascript
async function getValue() {
  return 10;
}

getValue().then(v => console.log(v)); // 10
```

##### **Explanation:**

- Even plain return value → Promise.resolve(value) হিসেবে return হয়
    

##### **Use Case:**

- Sync value wrap in async function
    
- Consistent return type for async code
    

##### **Error Cases / Common Mistakes ⚠️:**

- Forgetting `.then()` for async return value
    
- Treating async return as immediate value
    

##### **Best Practice ⚡:**

- Always handle async return with await or then
    

---

## **Summary Table:**

|Feature|Description|Syntax|Use Case|
|---|---|---|---|
|Async Function|Returns Promise|`async function f(){}`|Async wrapper|
|Await|Pause until promise resolves|`const res = await promise;`|Async code sequential|
|Sequential Execution|Stepwise dependent tasks|Multiple await|Dependent async|
|Parallel Execution|Independent tasks together|`await Promise.all([...])`|Multiple API calls|
|Error Handling|Try/catch/finally|`try{await}catch(e){}`|Async error capture|
|Async Return Value|Returns promise|`return value`|Consistent async API|

---

### **Key Points:**

- Async/Await = Promise wrapper for readable async code
    
- Always use try/catch for error handling
    
- Use Promise.all for parallel tasks
    
- Async function always returns Promise
    

---

যদি চাও, আমি পরের টপিক হিসেবে **Fetch API with Async/Await + Error Handling + JSON Parsing** সাজাতে পারি।  
এটি practical web development-এর জন্য full integration-ready।

চাও কি আমি সেটা বানাই?
