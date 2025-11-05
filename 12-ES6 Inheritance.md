##### **Definition:**

**Inheritance** হলো একটি **Object-Oriented Programming (OOP)** concept,  যেখানে একটি **class** অন্য একটি **class থেকে properties ও methods** উত্তরাধিকারসূত্রে পায়।  
- ES6 এ inheritance করা হয় **`extends`** ও **`super()`** keyword ব্যবহার করে।
- এর মাধ্যমে কোড পুনরায় ব্যবহার করা যায় (code reusability) এবং structure আরও পরিষ্কার হয়।

---

##### **Syntax:**

```javascript
class ParentClass {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log(`Hello, ${this.name}`);
  }
}

class ChildClass extends ParentClass {
  constructor(name, age) {
    super(name); // parent constructor call
    this.age = age;
  }
  displayAge() {
    console.log(`${this.name} is ${this.age} years old.`);
  }
}
```

---

##### **Explanation:**

- `extends` ব্যবহার করে child class, parent class-এর behavior (method/property) পায়।
- `super()` keyword parent class-এর constructor call করে।
- Parent class-এর methods, child class থেকে access করা যায়।

---

##### **Examples:**

```javascript

// Base (Parent) Class
class Car {
  constructor(brand) {
    this.brand = brand; // গাড়ির ব্র্যান্ড
  }

  start() {
    // শুধু মান return করা হচ্ছে, console.log নয়
    return `${this.brand} car has started.`;
  }
}

// Derived (Child) Class
class CarModel extends Car {
  constructor(brand, model, year) {
    super(brand); // parent class-এর constructor কে কল করা হলো
    this.model = model; // গাড়ির মডেল
    this.year = year;   // গাড়ির বছর
  }

  // নতুন method: মডেল তথ্য দেখানো
  showDetails() {
    return `${this.brand} ${this.model} (${this.year})`;
  }

  // parent-এর start() method override করা হলো
  start() {
    return `${this.brand} ${this.model} engine started successfully!`;
  }
}

// object তৈরি করা হলো
const car1 = new CarModel("Toyota", "Land Cruiser", 2023);
const car2 = new CarModel("BYD", "Syllion", 2024);

// return value গুলো আলাদা করে console.log করা হলো
console.log(car1.start());       // Output: Toyota Corolla engine started successfully!
console.log(car1.showDetails()); // Output: Toyota Corolla (2023)

console.log(car2.start());       // Output: Tesla Model S engine started successfully!
console.log(car2.showDetails()); // Output: Tesla Model S (2024)
```

---

##### **Explanation:**

1. `CarModel` class টি `Car` class কে **extend** করেছে।
2. `super()` keyword parent constructor (`Car`) কে কল করেছে, যাতে `brand` property ইনিশিয়াল হয়।
3. Parent class-এর `start()` method override করে `CarModel` নিজস্ব behavior define করেছে।
4. Parent class-এর সব property ও method (`brand`, `start()`) child class (`CarModel`) inherit করেছে।

---

##### **Use Case:**

1. Reusability — একই logic বারবার না লিখে parent class থেকে নেওয়া।
2. Code organization — base class এবং derived class আলাদা রাখা।
3. Polymorphism — একই method আলাদা class-এ আলাদা behavior।
4. Layered architecture — যেমন: Model → BaseModel → UserModel।

---
## **Types / Variations:**

---

### **1. Type-1: Single Level Inheritance**

##### **Definition:**

একটি child class একটি parent class থেকে inherit করে।

##### **Syntax:**

```javascript
class A {}
class B extends A {}
```

##### **Example:**

```javascript
class Vehicle {
  start() { console.log("Vehicle started"); }
}
class Car extends Vehicle {}
const c = new Car();
c.start(); // Vehicle started
```

##### **Explanation:**

- `Car` class `Vehicle` থেকে method পায়।
- এক স্তরে inheritance হয়েছে (single level)।

##### **Use Case:**

- Simple reusable base class তৈরি করা।

##### **Error Cases / Common Mistakes ⚠️:**

- `super()` না ডাকলে constructor error হবে।

```javascript
class Car extends Vehicle {
  constructor() {
    // ❌ Must call super() before accessing this
    this.name = "BMW"; // Error
  }
}
```

##### **Best Practice ⚡:**

- Always call `super()` in child constructor before using `this`।

---

### **2. Type-2: Multi-Level Inheritance**

##### **Definition:**

একাধিক স্তরে inheritance হয় — অর্থাৎ class → subclass → sub-subclass।

##### **Syntax:**

```javascript
class A {}
class B extends A {}
class C extends B {}
```

##### **Example:**

```javascript
class LivingThing {
  breathe() { console.log("Breathing..."); }
}
class Animal extends LivingThing {
  move() { console.log("Moving..."); }
}
class Dog extends Animal {
  bark() { console.log("Barking..."); }
}

const dog = new Dog();
dog.breathe(); // Breathing...
dog.move();    // Moving...
dog.bark();    // Barking...
```

##### **Explanation:**

- `Dog` → `Animal` → `LivingThing` এর inheritance chain তৈরি হয়েছে।
- Top-most parent থেকে নিচ পর্যন্ত সব property/method inherited হয়েছে।

##### **Use Case:**

- Layered inheritance structure।

##### **Error Cases / Common Mistakes ⚠️:**

- Circular inheritance করা যায় না (একটি class নিজেই নিজেকে extend করতে পারে না)।

##### **Best Practice ⚡:**

- Multi-level chain ছোট রাখো। Deep chain debugging কঠিন হয়।

---

### **3. Type-3: Method Overriding**

##### **Definition:**

Child class একই নামের method redefine করে parent method কে override করে।

##### **Syntax:**

```javascript
class Parent {
  sayHello() { console.log("Hello from Parent"); }
}
class Child extends Parent {
  sayHello() { console.log("Hello from Child"); }
}
```

##### **Example:**

```javascript
class Animal {
  speak() { console.log("Animal sound"); }
}
class Cat extends Animal {
  speak() { console.log("Meow"); }
}
const c = new Cat();
c.speak(); // Meow
```

##### **Explanation:**

- Child class-এর method parent এর উপর প্রাধান্য পায়।
- চাইলে `super.methodName()` দিয়ে parent method-ও call করা যায়।

##### **Use Case:**

- Polymorphism implement করা।

##### **Error Cases / Common Mistakes ⚠️:**

- Parent method completely replace হয়ে যায় যদি `super.method()` না ডাকা হয়।

##### **Best Practice ⚡:**

- Overriding করলে চাইলে parent behavior `super.method()` দিয়ে retain করা যেতে পারে।

---

## **Error Cases / Common Mistakes ⚠️:**

1. `super()` call এর আগে `this` ব্যবহার করলে error হয়।
2. Non-class object কে `extends` করলে TypeError।
3. Static method inheritance করতে গেলে keyword miss করলে error হবে।

---

## **Best Practice ⚡:**

- Constructor এ সবসময় `super()` call করতে হবে।
- Deep inheritance hierarchy avoid করতে হবে।
- Common logic base class এ রাখতে হবে।
- Proper method overriding ব্যবহার করতে হবে (redundant নয়)।

---

## **Summary:**

|Concept|Keyword|Description|Example|
|---|---|---|---|
|Inheritance|`extends`|Parent class inherit করা|`class B extends A {}`|
|Constructor Linking|`super()`|Parent constructor call করা|`super(name)`|
|Method Overriding|Same method redefine|`speak()` override||
|Access Parent Method|`super.method()`|Parent method call|`super.speak()`|

---

### **Key Takeaways:**

- `extends` → inheritance তৈরি করে
- `super()` → parent constructor/method call করে
- Parent class এর সব property ও method child এ পাওয়া যায়
- Inheritance → **code reusability + scalability + maintainability** বাড়ায়

---
