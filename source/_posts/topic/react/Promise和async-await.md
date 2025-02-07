---
title: Promise和async/await
tags: []
categories: []
permalink: posts/react/03.html
excerpt: ""
poster:
  topic: null
  headline: null
  caption: null
  color: null
abbrlink: 69d2da81
date: 2025-02-07 15:15:02
updated: 2025-02-07 15:15:02
topic:
banner:
references:
---

## **1️⃣ Promise**

**`Promise`** 是 JavaScript 中用于处理异步操作的一种机制。它表示一个可能在未来某个时间点完成或失败的操作。`Promise` 有三种状态：

- **`Pending`**（等待中）：异步操作尚未完成。
- **`Fulfilled`**（已完成）：异步操作成功完成。
- **`Rejected`**（已拒绝）：异步操作失败。

### **Promise 的语法**

```javascript
const promise = new Promise((resolve, reject) => {
  // 异步操作
  const success = true; // 假设异步操作的结果
  if (success) {
    resolve("操作成功！"); // 操作成功，返回结果
  } else {
    reject("操作失败！"); // 操作失败，返回错误
  }
});
```

### **使用 `then()` 和 `catch()` 处理 Promise**

```javascript
const promise = new Promise((resolve, reject) => {
  const success = true;
  if (success) {
    resolve("操作成功！");
  } else {
    reject("操作失败！");
  }
});

promise
  .then((result) => {
    console.log(result); // 输出：操作成功！
  })
  .catch((error) => {
    console.log(error); // 输出：操作失败！
  });
```

### **Promise 链式调用**

```javascript
new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000);
})
  .then((result) => {
    console.log(result); // 输出：1
    return result + 1;
  })
  .then((result) => {
    console.log(result); // 输出：2
    return result + 1;
  })
  .then((result) => {
    console.log(result); // 输出：3
  })
  .catch((error) => {
    console.error(error);
  });
```

---

## **2️⃣ async/await**

**`async/await`** 是基于 `Promise` 的语法糖，使得异步代码的书写更简洁、直观和易于维护。它让异步代码看起来像同步代码一样，避免了回调函数和 `.then()` 链式调用的复杂性。

### **`async` 函数**

`async` 用来声明一个函数是异步的，它总是返回一个 `Promise`。

```javascript
async function example() {
  return "Hello, world!";
}

example().then((result) => console.log(result)); // 输出：Hello, world!
```

### **`await` 关键字**

`await` 只能在 `async` 函数内部使用。它会等待一个 `Promise` 完成并返回其结果。如果 `Promise` 被拒绝，`await` 会抛出错误（类似于同步代码中的异常）。

```javascript
async function fetchData() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  const data = await response.json();
  console.log(data); // 打印获取的数据
}

fetchData();
```

### **`async/await` 的错误处理**

与同步代码类似，我们可以使用 `try/catch` 来捕获异步操作中的错误。

```javascript
async function fetchData() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts");
    if (!response.ok) {
      throw new Error("网络请求失败");
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("错误：", error.message);
  }
}

fetchData();
```

### **`async/await` 与 Promise 链式调用的对比**

- **Promise**：

  ```javascript
  fetch("https://jsonplaceholder.typicode.com/posts")
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error(error));
  ```

- **async/await**：

  ```javascript
  async function fetchData() {
    try {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/posts"
      );
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error(error);
    }
  }

  fetchData();
  ```

通过 **`async/await`**，代码看起来更简洁，类似同步的流畅执行，不需要 `.then()` 链式调用。

---

## **3️⃣ Promise.all() 和 Promise.allSettled()**

### **`Promise.all()`**

`Promise.all()` 用来处理多个并发的异步操作，等待所有的 `Promise` 完成后再执行。它返回一个新的 `Promise`，当所有输入的 `Promise` 成功时，返回一个包含所有结果的数组。如果有一个 `Promise` 被拒绝，`Promise.all()` 会立即拒绝，并返回该错误。

```javascript
const promise1 = Promise.resolve(1);
const promise2 = Promise.resolve(2);
const promise3 = Promise.resolve(3);

Promise.all([promise1, promise2, promise3])
  .then((results) => {
    console.log(results); // 输出：[1, 2, 3]
  })
  .catch((error) => {
    console.error(error);
  });
```

### **`Promise.allSettled()`**

`Promise.allSettled()` 会等待所有的 `Promise` 完成（无论是成功还是失败），并返回每个 `Promise` 的结果。

```javascript
const promise1 = Promise.resolve(1);
const promise2 = Promise.reject("Error!");
const promise3 = Promise.resolve(3);

Promise.allSettled([promise1, promise2, promise3]).then((results) => {
  console.log(results);
  // 输出：
  // [
  //   { status: 'fulfilled', value: 1 },
  //   { status: 'rejected', reason: 'Error!' },
  //   { status: 'fulfilled', value: 3 }
  // ]
});
```

---

## **4️⃣ 异步操作的进阶技巧**

### **并发请求与异步限制**

当你有多个异步请求时，可能希望限制并发请求的数量。例如，使用 **`Promise.all()`** 发送多个并发请求，而不是等待一个请求完成后才发送下一个。

```javascript
const urls = [
  "https://jsonplaceholder.typicode.com/posts/1",
  "https://jsonplaceholder.typicode.com/posts/2",
  "https://jsonplaceholder.typicode.com/posts/3",
];

async function fetchUrls() {
  try {
    const responses = await Promise.all(urls.map((url) => fetch(url)));
    const data = await Promise.all(
      responses.map((response) => response.json())
    );
    console.log(data);
  } catch (error) {
    console.error("请求失败：", error);
  }
}

fetchUrls();
```

---

## 总结

- **Promise** 是处理异步操作的基础，通过 `.then()` 和 `.catch()` 来处理异步结果。
- **async/await** 是基于 **Promise** 的语法糖，使得异步代码更像同步代码，更容易理解和维护。
- **Promise.all()** 和 **Promise.allSettled()** 用于并发处理多个异步操作。



