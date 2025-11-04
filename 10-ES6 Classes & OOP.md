##### **Definition:**

**Class** হলো blueprint যা দিয়ে object তৈরি করা যায়।  **OOP (Object-Oriented Programming)** হলো programming paradigm যেখানে objects, properties, methods, inheritance, encapsulation ইত্যাদি ব্যবহৃত হয়।

---
##### **Syntax:**

```javascript
// Class declaration
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

// object creation
const store = new Person( "Saif", 22);
console.log(store);  // Output: Person {name: 'Saif', age: 22}
```

---
##### **Explanation:**

- `class` = blueprint
- `constructor()` = class initialize করার জন্য
- Methods = class behavior define করে
- Object = class instance

---

##### **Examples:**

```javascript
class Car {
  constructor(brand, model) {
    this.brand = brand;
    this.model = model;
  }

  showDetails() {
    console.log(`${this.brand} - ${this.model}`);
  }
}

const car1 = new Car("Toyota", "Corolla");
car1.showDetails(); // Toyota - Corolla
```

---

##### **Use Case:**

1. Blueprint দিয়ে objects তৈরি করা
2. Reusable code & maintainable design
3. Encapsulation, Inheritance, Polymorphism support

---
## **Types / Variations:**

---
### **1. Type-1: Basic Class & Object**

##### **Definition:**

Basic class with constructor and methods.

##### **Syntax:**

```javascript
class ClassName {
  constructor(param1, param2) { ... }
  methodName() { ... }
}
```

##### **Examples:**

```javascript
class Student {
  constructor(name, grade) {
    this.name = name;
    this.grade = grade;
  }

  display() {
    console.log(`${this.name} has grade ${this.grade}`);
  }
}

const s1 = new Student("Rafi", "A");
s1.display(); // Rafi has grade A
```

##### **Explanation:**

- `constructor` automatically call হয় object create করার সময়
- Methods object instance থেকে access করা হয়

##### **Use Case:**

- Simple object representation

##### **Error Cases / Common Mistakes ⚠️:**

- Methods outside class ❌
- Constructor misspell ❌

##### **Best Practice ⚡:**

- Always use constructor for initialization
- Use methods for behavior

```js

// Class declaration
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  // Method যোগ করা হয়েছে
  greet() {
    console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
  }
}

// একাধিক object (instance) তৈরি করা হলো
const p1 = new Person("Saiful", 25);
const p2 = new Person("Ishraq", 13);
const p3 = new Person("Tuhin");

// প্রত্যেক object-এর নিজস্ব data আছে
console.log(p1);
console.log(p2);
console.log(p3);

// প্রত্যেক object তার নিজের method call করতে পারে
p1.greet();
p2.greet();
p3.greet();
```

**Output:**

```
Person {name: 'Saiful', age: 25}
Person {name: 'Ishraq', age: 13}
Person {name: 'Tuhin', age: undefined}

Hello, my name is Saiful and I'm 25 years old.
Hello, my name is Ishraq and I'm 13 years old.
Hello, my name is Tuhin and I'm undefined years old.
```

---
### **2. Type-2: Inheritance (extends & super)**

##### **Definition:**

এক class অন্য class থেকে properties/methods inherit করে।

##### **Syntax:**

```javascript
class Parent { ... }
class Child extends Parent { 
  constructor(...) { super(...); } 
}
```

##### **Examples:**

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  greet() {
    console.log(`Hello, I'm ${this.name}`);
  }
}

class Employee extends Person {
  constructor(name, age, job) {
    super(name, age);
    this.job = job;
  }
  work() {
    console.log(`${this.name} is working as ${this.job}`);
  }
}

const e1 = new Employee("Saiful", 25, "Developer");
e1.greet(); // Hello, I'm Saiful
e1.work();  // Saiful is working as Developer
```

##### **Explanation:**

- `extends` → inheritance
- `super()` → parent constructor call
- Child class parent methods access করতে পারে

##### **Use Case:**

- Code reuse
- Hierarchical relationships modeling

##### **Error Cases / Common Mistakes ⚠️:**

- `super()` না call করলে ❌ Error
- Parent methods inaccessible without inheritance

##### **Best Practice ⚡:**

- Only use inheritance when logical relation exists
- Avoid deep inheritance chain

---

### **3. Type-3: Getter & Setter**

##### **Definition:**

Object properties read/write access control করা হয়।

##### **Syntax:**

```javascript
class ClassName {
  get property() { ... }
  set property(value) { ... }
}
```

##### **Examples:**

```javascript
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  get area() {
    return this.width * this.height;
  }

  set dimensions({width, height}) {
    this.width = width;
    this.height = height;
  }
}

const rect = new Rectangle(5, 10);
console.log(rect.area); // 50
rect.dimensions = {width: 6, height: 12};
console.log(rect.area); // 72
```

##### **Explanation:**

- `get` → property value read
- `set` → property value write
- Encapsulation & validation possible

##### **Use Case:**

- Encapsulation
- Input validation
- Calculated properties

##### **Error Cases / Common Mistakes ⚠️:**

- Setter without parameter ❌
- Getter method call with () ❌

##### **Best Practice ⚡:**

- Use get/set for controlled access
- Avoid exposing internal state directly

---
### **4. Type-4: Static Methods & Properties**

##### **Definition:**

Class-level methods/properties, instance থেকে access হয় না।

##### **Syntax:**

```javascript
class ClassName {
  static methodName() { ... }
}
```

##### **Examples:**

```javascript
class MathUtils {
  static square(x) {
    return x * x;
  }
}

console.log(MathUtils.square(5)); // 25

const mu = new MathUtils();
console.log(mu.square); // undefined
```

##### **Explanation:**

- Static methods/properties belong to class
- Object instance থেকে access হয় না

##### **Use Case:**

- Utility functions
- Constant data

##### **Error Cases / Common Mistakes ⚠️:**

- Instance থেকে static call ❌

##### **Best Practice ⚡:**

- Pure functions/utility → static method
- Class constants → static property

---

### **5. Type-5: Encapsulation (Private Fields)**

##### **Definition:**

Object internal state hide করা, outside access restricted।

##### **Syntax:**

```javascript
class ClassName {
  #privateField;
}
```

##### **Examples:**

```javascript
class BankAccount {
  #balance;
  constructor(balance) {
    this.#balance = balance;
  }
  deposit(amount) {
    this.#balance += amount;
  }
  getBalance() {
    return this.#balance;
  }
}

const acc = new BankAccount(1000);
acc.deposit(500);
console.log(acc.getBalance()); // 1500
console.log(acc.#balance); // ❌ Error
```

##### **Explanation:**

- `#` prefix → private field
- Encapsulation ensures controlled access

##### **Use Case:**

- Sensitive data
- Internal logic hide

##### **Error Cases / Common Mistakes ⚠️:**

- `#` missing → public
- Direct access attempt → Error

##### **Best Practice ⚡:**

- Internal state private রাখা
- Getter/setter দিয়ে controlled access

---

## **Summary Table:**

|Feature|Description|Syntax|Example|
|---|---|---|---|
|Basic Class|Blueprint with constructor & methods|`class X{}`|`new X()`|
|Inheritance|Child class inherits parent|`extends, super()`|`class Child extends Parent`|
|Getter/Setter|Controlled property access|`get prop(){}, set prop(val){}`|`rect.area`|
|Static|Class-level method/property|`static method(){}`|`MathUtils.square(5)`|
|Encapsulation|Private fields|`#privateField`|`acc.#balance ❌`|

---

### **Key Points:**

- Class → blueprint, Object → instance
- Constructor = object init
- Methods = behavior
- Inheritance → code reuse
- Getter/Setter → controlled access
- Static → class-level
- Encapsulation → private state

---
