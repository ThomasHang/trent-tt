---
title: ES6基础
tags:
  - react
categories:
  - 技术分享
permalink: posts/react/02.html
poster:
  topic: null
  headline: react教程
  caption: null
  color: null
topic: react
excerpt: 本教程介绍了一些git的基本命令，包括版本控制、提交、回退、合并等。
abbrlink: f30f6a08
date: 2025-02-06 09:47:59
updated: 2024-11-02 23:51:59
references:
---

---

### 1️⃣ **变量声明：`let` 和 `const`**

- **`let`** 用于声明一个可以重新赋值的变量，作用域是块级作用域（block scope）。
- **`const`** 用于声明一个常量，一旦赋值后不能更改，作用域也是块级作用域。

```javascript
let x = 10; // 可变
x = 20; // 可以重新赋值

const y = 30; // 常量，不能重新赋值
// y = 40;    // 错误，常量不能改变
```

---

### 2️⃣ **箭头函数（Arrow Functions）**

箭头函数是一种简洁的函数表达式，省略了 `function` 关键字，并且箭头函数不会绑定 `this`。

```javascript
// 普通函数
function sum(a, b) {
  return a + b;
}

// 箭头函数
const sum = (a, b) => a + b;
```

**特点：**

- 自动绑定外部的 `this`。
- 没有 `arguments` 对象。

---

### 3️⃣ **解构赋值（Destructuring）**

解构赋值可以方便地从数组或对象中提取值并赋给变量。

- **数组解构**：

```javascript
const arr = [1, 2, 3];
const [a, b] = arr;
console.log(a, b); // 输出：1 2
```

- **对象解构**：

```javascript
const person = { name: "John", age: 30 };
const { name, age } = person;
console.log(name, age); // 输出：John 30
```

---

### 4️⃣ **扩展运算符（Spread Operator）**

扩展运算符（`...`）用于展开数组或对象，或者用于合并多个对象/数组。

- **数组合并**：

```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];
const merged = [...arr1, ...arr2];
console.log(merged); // 输出：[1, 2, 3, 4]
```

- **对象合并**：

```javascript
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const mergedObj = { ...obj1, ...obj2 };
console.log(mergedObj); // 输出：{ a: 1, b: 2 }
```

---

### 5️⃣ **模板字符串（Template Literals）**

模板字符串用反引号（`` ` ``）包裹，可以直接插入变量和表达式。

```javascript
const name = "John";
const greeting = `Hello, ${name}!`;
console.log(greeting); // 输出：Hello, John!
```

---

### 6️⃣ **默认参数（Default Parameters）**

在函数声明时，可以为参数设置默认值。

```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}`);
}

greet(); // 输出：Hello, Guest
greet("Alice"); // 输出：Hello, Alice
```

---

### 7️⃣ **`for...of` 循环**

`for...of` 用于遍历数组、字符串等可迭代对象。

```javascript
const arr = [1, 2, 3];
for (const num of arr) {
  console.log(num); // 输出：1 2 3
}
```

---

### 8️⃣ **`Promise` 和 `async/await`**

- **`Promise`** 用于异步操作的结果值的表示。
- **`async/await`** 使得处理 `Promise` 的方式变得更直观。

```javascript
// Promise
const fetchData = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Data fetched!"), 1000);
});

fetchData.then((result) => console.log(result)); // 输出：Data fetched!

// async/await
async function fetchDataAsync() {
  const result = await fetchData;
  console.log(result); // 输出：Data fetched!
}
```

---

### 9️⃣ **类（Classes）**

ES6 引入了类的概念，提供了更简洁的语法来创建对象。

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, I'm ${this.name}, and I'm ${this.age} years old.`);
  }
}

const john = new Person("John", 30);
john.greet(); // 输出：Hello, I'm John, and I'm 30 years old.
```

---

### 🔟 **模块化（Modules）**

ES6 引入了模块化，使得代码可以更好地分离和重用。

- **导出（`export`）**：

```javascript
// person.js
export const name = "John";
export function greet() {
  console.log("Hello!");
}
```

- **导入（`import`）**：

```javascript
// app.js
import { name, greet } from "./person.js";
console.log(name); // 输出：John
greet(); // 输出：Hello!
```

---

### **1️⃣ `map()` 方法**

`map()` 方法会返回一个新的数组，数组中的元素是通过调用提供的函数处理原数组元素后得到的结果。这个方法不会改变原数组。

#### 语法：

```javascript
array.map(callback(currentValue, index, array), thisArg);
```

- `callback`: 用于处理每个元素的函数。
- `currentValue`: 当前元素。
- `index` (可选): 当前元素的索引。
- `array` (可选): 调用 `map` 的数组。

#### 示例：

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map((num) => num * 2);
console.log(doubled); // 输出：[2, 4, 6, 8]
```

### **2️⃣ `filter()` 方法**

`filter()` 方法创建一个新数组，其中包含通过提供的函数测试的所有元素，元素满足条件时被保留。原数组不会被修改。

#### 语法：

```javascript
array.filter(callback(currentValue, index, array), thisArg);
```

- `callback`: 用于测试每个元素的函数，返回 `true` 或 `false`。
- `currentValue`: 当前元素。
- `index` (可选): 当前元素的索引。
- `array` (可选): 调用 `filter` 的数组。

#### 示例：

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter((num) => num % 2 === 0);
console.log(evenNumbers); // 输出：[2, 4, 6]
```

### **3️⃣ `reduce()` 方法**

`reduce()` 方法对数组中的每个元素执行一个指定的函数，最终计算出一个单一的值（比如和、积等）。该方法接收两个参数：回调函数和初始值。

#### 语法：

```javascript
array.reduce(callback(accumulator, currentValue, index, array), initialValue);
```

- `callback`: 用于执行每个元素的函数。
  - `accumulator`: 上次调用回调时返回的累积值，或者是 `initialValue`。
  - `currentValue`: 当前处理的元素。
  - `index` (可选): 当前元素的索引。
  - `array` (可选): 调用 `reduce` 的数组。
- `initialValue` (可选): 累积值的初始值。如果不提供，`reduce()` 将使用数组的第一个元素作为初始值。

#### 示例：

```javascript
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 输出：15
```

#### 更复杂的例子（求数组中对象的总和）：

```javascript
const orders = [
  { product: "Shirt", price: 20 },
  { product: "Pants", price: 50 },
  { product: "Shoes", price: 30 },
];

const totalPrice = orders.reduce((acc, order) => acc + order.price, 0);
console.log(totalPrice); // 输出：100
```

### 总结：

- **`map()`**: 适用于需要转换数组中的每个元素并返回新数组的场景。
- **`filter()`**: 适用于从原数组中筛选符合条件的元素，返回一个新数组。
- **`reduce()`**: 适用于将数组中的所有元素汇总成一个单一值的场景，如求和、求积等。

---

### 📝 **练习**

让我们通过一些练习来加深对这三个方法的理解。

### 练习 1：箭头函数 & 解构赋值

假设有一个用户列表，每个用户对象包含 `name` 和 `age`，请编写一个函数：

- 使用 **箭头函数** 遍历用户列表。
- 使用 **解构赋值** 提取每个用户的 `name` 和 `age`。

```javascript
const users = [
  { name: "Alice", age: 28 },
  { name: "Bob", age: 25 },
  { name: "Charlie", age: 32 },
];

const printUsers = () => {
  users.forEach(({ name, age }) => {
    console.log(`${name} is ${age} years old.`);
  });
};

printUsers();
```

---

### 练习 2：扩展运算符（Spread Operator）

假设你有两个对象，分别包含个人信息和联系信息。请编写一个函数，使用 **扩展运算符** 合并这两个对象，并返回一个新对象。

```javascript
const personalInfo = {
  name: "John",
  age: 30,
};

const contactInfo = {
  email: "john@example.com",
  phone: "123-456-7890",
};

const mergeInfo = () => {
  const fullInfo = { ...personalInfo, ...contactInfo };
  console.log(fullInfo);
};

mergeInfo();
```

---

### 练习 3：默认参数 & `for...of` 循环

编写一个函数，计算给定数字数组的总和。如果没有传入数组，则默认使用空数组。请使用 **默认参数** 和 **`for...of`** 循环来实现。

```javascript
const sumNumbers = (numbers = []) => {
  let sum = 0;
  for (const num of numbers) {
    sum += num;
  }
  console.log(`The sum is: ${sum}`);
};

sumNumbers([1, 2, 3, 4]); // 输出：The sum is: 10
sumNumbers(); // 输出：The sum is: 0
```

---

### 练习 4：Promise & `async/await`

编写一个模拟异步请求的函数，返回一个 Promise。使用 **`async/await`** 来处理该 Promise 并输出结果。

```javascript
const fetchData = new Promise((resolve, reject) => {
  setTimeout(() => {
    const data = "Fetched data from API";
    resolve(data);
  }, 2000);
});

const getData = async () => {
  const result = await fetchData;
  console.log(result); // 输出：Fetched data from API
};

getData();
```

---

### 练习 5：类（Classes）与实例化

编写一个 `Person` 类，并创建一个实例。类中包含一个方法，用于输出该人的名字和年龄。

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hi, I'm ${this.name} and I am ${this.age} years old.`);
  }
}

const person1 = new Person("Alice", 25);
person1.greet(); // 输出：Hi, I'm Alice and I am 25 years old.
```

---

### 练习 6：模块化（Modules）

编写两个文件：

**person.js**

```javascript
// person.js
export const name = "Alice";
export const age = 25;

export function greet() {
  console.log(`Hi, I'm ${name} and I am ${age} years old.`);
}
```

**app.js**

```javascript
// app.js
import { name, age, greet } from "./person.js";

console.log(name); // 输出：Alice
greet(); // 输出：Hi, I'm Alice and I am 25 years old.
```

#### 练习 7：`map()` 方法

给定一个数组 `numbers = [1, 2, 3, 4, 5]`，使用 `map()` 方法将每个数字都乘以 10，并返回一个新数组。

```javascript
const numbers = [1, 2, 3, 4, 5];
const multipliedNumbers = numbers.map((num) => num * 10);
console.log(multipliedNumbers); // 输出：[10, 20, 30, 40, 50]
```

#### 练习 8：`filter()` 方法

给定一个数组 `numbers = [1, 2, 3, 4, 5, 6]`，使用 `filter()` 方法筛选出所有大于 3 的数字。

```javascript
const numbers = [1, 2, 3, 4, 5, 6];
const greaterThanThree = numbers.filter((num) => num > 3);
console.log(greaterThanThree); // 输出：[4, 5, 6]
```

#### 练习 9：`reduce()` 方法

给定一个数组 `numbers = [1, 2, 3, 4]`，使用 `reduce()` 方法计算数组的所有元素之和。

```javascript
const numbers = [1, 2, 3, 4];
const totalSum = numbers.reduce((acc, num) => acc + num, 0);
console.log(totalSum); // 输出：10
```
