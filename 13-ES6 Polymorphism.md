##### **Definition:**

**Polymorphism** (Greek: _poly = many, morph = form_) মানে হলো **একই interface বা method-এর একাধিক রূপ থাকা**।  
অর্থাৎ, **একটি method বিভিন্ন class-এ ভিন্নভাবে কাজ করতে পারে** — এই বৈশিষ্ট্যই হলো _Polymorphism_।

ES6-এ এটি মূলত **Inheritance ও Method Overriding** ব্যবহার করে implement করা হয়।

---

##### **Syntax:**

```javascript
class Parent {
  makeSound() {
    console.log("Some generic sound");
  }
}

class Dog extends Parent {
  makeSound() {
    console.log("Bark");
  }
}

class Cat extends Parent {
  makeSound() {
    console.log("Meow");
  }
}

const animals = [new Dog(), new Cat()];

for (const animal of animals) {
  animal.makeSound(); // same method name, different behavior
}
```

---

##### **Explanation:**

- Parent class একটি **common method (interface)** define করে।
- Child classes method override করে নিজ নিজ behavior define করে।
- এক জায়গা থেকে call করা হলেও প্রতিটি object নিজস্ব implementation execute করে।

---

##### **Examples:**

###### **Example 1: Basic Method Overriding (Compile-time Polymorphism)**

```javascript
class Shape {
  area() {
    return "Area not defined";
  }
}

class Circle extends Shape {
  constructor(radius) {
    super();
    this.radius = radius;
  }
  area() {
    return Math.PI * this.radius * this.radius;
  }
}

class Rectangle extends Shape {
  constructor(width, height) {
    super();
    this.width = width;
    this.height = height;
  }
  area() {
    return this.width * this.height;
  }
}

const shapes = [new Circle(5), new Rectangle(4, 6)];

for (const shape of shapes) {
  console.log(shape.area());
}
// Output:
// 78.53981633974483
// 24
```

###### **Example 2: Polymorphism with Function Parameters**

```javascript
class Animal {
  speak() { console.log("Animal speaks"); }
}

class Dog extends Animal {
  speak() { console.log("Dog barks"); }
}

class Cat extends Animal {
  speak() { console.log("Cat meows"); }
}

function makeItSpeak(animal) {
  animal.speak(); // Works differently depending on the object
}

makeItSpeak(new Dog()); // Dog barks
makeItSpeak(new Cat()); // Cat meows
```

###### **Example 3: Using super() in Polymorphism**

```javascript
class Vehicle {
  start() {
    console.log("Starting vehicle...");
  }
}

class Car extends Vehicle {
  start() {
    super.start();
    console.log("Car engine started!");
  }
}

const c = new Car();
c.start();
// Output:
// Starting vehicle...
// Car engine started!
```

---

##### **Explanation:**

- একই `area()` বা `speak()` method সব class-এ আলাদা কাজ করছে।
- এটি runtime-এ নির্ধারণ হয় কোন object কোন method execute করবে → **Runtime Polymorphism**।
- `super.method()` দিয়ে parent behavior retain করা যায়।

---

##### **Use Case:**

1. **Reusable design:** একই interface ব্যবহার করে বিভিন্ন behavior তৈরি করা যায়।
2. **Scalability:** নতুন class যোগ করলেও পুরনো code পরিবর্তন করতে হয় না।
3. **Clean architecture:** Logic centralize করা যায়।
4. **Dynamic behavior:** runtime-এ object অনুযায়ী response পরিবর্তন হয়।

---

## **Types / Variations:**

---

### **1. Type-1: Compile-time Polymorphism (Method Overloading - Limited in JS)**

##### **Definition:**

একই নামের function বিভিন্ন parameter pattern-এ কাজ করে।  
(তবে JavaScript-এ method overloading নেই, কিন্তু optional/default parameters দিয়ে simulate করা যায়।)

##### **Syntax:**

```javascript
function add(a, b, c = 0) {
  return a + b + c;
}
console.log(add(2, 3));    // 5
console.log(add(2, 3, 4)); // 9
```

##### **Explanation:**

- Parameter count অনুযায়ী method behavior পরিবর্তিত হয়।

##### **Use Case:**

- Optional argument handling।

##### **Error Cases / Common Mistakes ⚠️:**

- Function overloading as language feature নেই; manually handle করতে হয়।

##### **Best Practice ⚡:**

- Default parameter ও argument checking ব্যবহার করতে হবে।

---

### **2. Type-2: Runtime Polymorphism (Method Overriding)**

##### **Definition:**

Child class same-named method redefine করে। Object অনুযায়ী runtime-এ execution পরিবর্তিত হয়।

##### **Syntax:**

```javascript
class Parent { display() { ... } }
class Child extends Parent { display() { ... } }
```

##### **Example:**

```javascript
class Bird {
  fly() { console.log("Bird is flying..."); }
}
class Eagle extends Bird {
  fly() { console.log("Eagle soars high..."); }
}
class Penguin extends Bird {
  fly() { console.log("Penguins can’t fly!"); }
}

const birds = [new Eagle(), new Penguin()];
for (const b of birds) b.fly();
```

##### **Explanation:**

- একই interface `fly()` সব class-এ আলাদা কাজ করছে।
- Object অনুযায়ী আলাদা output পাওয়া যায়।

##### **Use Case:**

- যখন অনেক subclass-এর common interface দরকার কিন্তু behavior আলাদা।

##### **Error Cases / Common Mistakes ⚠️:**

- Parent method call করতে ভুললে common behavior হারিয়ে যায়।

##### **Best Practice ⚡:**

- Override method-এ `super.method()` ব্যবহার করে parent behavior retain করা।

---

### **3. Type-3: Interface-based Polymorphism (Duck Typing in JS)**

##### **Definition:**

JavaScript এ strict interface নেই, কিন্তু “if it looks like a duck and quacks like a duck” নীতিতে কাজ করা যায়।

##### **Syntax:**

```javascript
function makeSpeak(obj) {
  obj.speak(); // যতক্ষণ obj.speak() আছে, ততক্ষণ ঠিকঠাক কাজ করবে
}

const dog = { speak() { console.log("Woof!"); } };
const cat = { speak() { console.log("Meow!"); } };

makeSpeak(dog);
makeSpeak(cat);
```

##### **Explanation:**

- একই function বিভিন্ন object handle করছে শুধুমাত্র তাদের behavior অনুযায়ী।
- এটি dynamic polymorphism এর উদাহরণ।

##### **Use Case:**

- Loose typing environment এ flexible design pattern।

##### **Error Cases / Common Mistakes ⚠️:**

- যদি `obj.speak()` না থাকে → runtime error (`TypeError`)।

##### **Best Practice ⚡:**

- Optional chaining বা `typeof obj.speak === 'function'` check করে নেয়া উচিত।

---

## **Error Cases / Common Mistakes ⚠️:**

1. Parent constructor call করতে `super()` ভুলে গেলে runtime error হবে।
2. Overriding method এর spelling বা parameter ভুল হলে polymorphism কাজ করবে না।
3. Dynamic typing এর জন্য method না থাকলে “is not a function” error হয়।

---

## **Best Practice ⚡:**

- Common interface নাম ব্যবহার করতে হবে (readable & predictable)।
- Parent behavior retain করতে চাইলে `super.method()` ব্যবহার করা।
- Polymorphism প্রয়োগ করতে inheritance structure clean রাখা।
- Duck typing ব্যবহারে আগে method existence যাচাই করা।

---

## **Summary:**

|Concept|Description|Example|Type|
|---|---|---|---|
|Method Overriding|Parent method redefine|`class Dog extends Animal { speak(){} }`|Runtime|
|Default Params|Overloading simulation|`function add(a,b,c=0)`|Compile-time|
|Duck Typing|Interface-less polymorphism|`obj.speak()`|Interface-based|

---

### **Key Takeaways:**

- **Polymorphism** = এক interface, একাধিক implementation।
- JavaScript-এ এটি মূলত **method overriding + dynamic typing** এর মাধ্যমে কাজ করে।
- Code structure হয় modular, reusable, এবং maintainable।
- ব্যবহার হয় inheritance, interfaces, ও dynamic dispatch system-এ।

---
