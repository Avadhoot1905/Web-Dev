part of [[TypeScript]] and [[JavaScript]]
# What are Async functions?

We use **`async` functions** in JavaScript when we want to handle asynchronous operations more easily, especially when dealing with promises. Asynchronous operations are tasks that don't run immediately and may take some time to complete (e.g., fetching data from an API, reading a file, or performing I/O operations). 

Here’s a breakdown of when to use `async` functions:

### 1. **Fetching Data from APIs or Servers**
When you need to retrieve data from an external source, such as a server or an API, the operation is asynchronous because it takes time for the server to respond. Using an `async` function allows you to wait for the server response without blocking other code execution.

**Example:**
```javascript
async function fetchData() {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    console.log(data);
}
```
Here, **`fetch()`** is an asynchronous function that returns a promise. The **`await`** keyword waits for the promise to resolve, and only then does the function proceed to the next line.

### 2. **Handling Promises More Readably**
Instead of using the `.then()` and `.catch()` chaining that comes with promises, `async` functions let you write asynchronous code in a synchronous-like way, which makes it easier to read and maintain.

**Without `async`/`await` (using promises directly):**
```javascript
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

**With `async`/`await`:**
```javascript
async function getData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```
This is much cleaner and avoids deeply nested promise chains (also known as "callback hell").

### 3. **When You Need to Wait for Multiple Asynchronous Operations**
If you have multiple asynchronous operations that depend on one another, you can use `async` functions to run them in sequence or parallel.

- **In Sequence:**  
You can use multiple `await` statements to ensure each operation completes before the next one starts.

    ```javascript
    async function fetchUserAndPosts() {
        const user = await fetch('/api/user');
        const posts = await fetch(`/api/posts/${user.id}`);
        console.log(posts);
    }
    ```

- **In Parallel:**  
You can run asynchronous operations in parallel by using `Promise.all()` inside an `async` function.

    ```javascript
    async function fetchUserAndPosts() {
        const [user, posts] = await Promise.all([
            fetch('/api/user'),
            fetch('/api/posts')
        ]);
        console.log(user, posts);
    }
    ```

### 4. **When Working with `setTimeout`, `setInterval`, or Other Timers**
`async` functions can be useful when dealing with timers or delays. Instead of using a callback, you can wrap the timer in a promise and `await` its resolution.

**Example with `setTimeout`:**
```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function runWithDelay() {
    console.log('Start');
    await delay(2000);  // Wait for 2 seconds
    console.log('After 2 seconds');
}
```

### 5. **Performing File/Database Operations in Node.js**
When working with I/O operations in Node.js (e.g., reading or writing files, querying a database), those tasks are asynchronous. You can use `async`/`await` to handle these operations cleanly.

**Example (Node.js with `fs.promises`):**
```javascript
const fs = require('fs').promises;

async function readFileContent() {
    try {
        const data = await fs.readFile('file.txt', 'utf8');
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

### 6. **When You Need Error Handling in Asynchronous Code**
With `async` functions, error handling becomes simpler through `try`/`catch` blocks, instead of relying on `.catch()` with promises.

**Example:**
```javascript
async function loadData() {
    try {
        const data = await fetchData();
        console.log(data);
    } catch (error) {
        console.error('Error fetching data:', error);
    }
}
```
In this case, any errors during the async operation are caught by the `catch` block, ensuring that the program can handle errors gracefully.

### Conclusion
- **Use `async` functions** when you need to handle asynchronous operations such as network requests, file I/O, or timers.
- They make your code cleaner and more readable by allowing you to use the `await` keyword, which avoids messy promise chains.
- You can handle errors more effectively with `try`/`catch` in `async` functions.
- They allow you to run asynchronous operations in sequence or parallel depending on the use case.

----
# What are Promises?

Simply put:

A **promise** in JavaScript is like a **guarantee** that you’ll get a result from an asynchronous task in the future (like waiting for data from a server). It could either be a **success** (you get what you want) or a **failure** (something went wrong).

### Simple explanation:

1. **Pending**: The promise is waiting for the task to finish (like you're waiting for food at a restaurant).
2. **Fulfilled**: The task was successful, and you get the result (the food arrives!).
3. **Rejected**: Something went wrong, and the task failed (the food didn’t arrive, or there was an issue with your order).

### Example:

Imagine you're ordering a pizza:

- You place an order (promise created).
- While you wait, the promise is **pending**.
- If the pizza arrives, the promise is **fulfilled**, and you enjoy the pizza.
- If there’s a problem (like the pizza burns), the promise is **rejected**.

### Using Promises:

You can handle these outcomes using `.then()` (if the promise is fulfilled) or `.catch()` (if it's rejected):

```javascript
let pizzaPromise = new Promise((resolve, reject) => {
    let pizzaArrived = true;

    if (pizzaArrived) {
        resolve('Pizza is here!');
    } else {
        reject('No pizza, something went wrong.');
    }
});

pizzaPromise
    .then((message) => {
        console.log(message); // Pizza is here!
    })
    .catch((error) => {
        console.log(error); // No pizza, something went wrong.
    });
```

### Why promises are useful:
Promises help you **wait** for something to finish (like a pizza order or data download) without stopping the rest of your code from running. When the task is done, you can **handle** the result (whether it’s good or bad).

Technically put:

We use **`async` functions** in JavaScript when we want to handle asynchronous operations more easily, especially when dealing with promises. Asynchronous operations are tasks that don't run immediately and may take some time to complete (e.g., fetching data from an API, reading a file, or performing I/O operations). 

Here’s a breakdown of when to use `async` functions:

### 1. **Fetching Data from APIs or Servers**
When you need to retrieve data from an external source, such as a server or an API, the operation is asynchronous because it takes time for the server to respond. Using an `async` function allows you to wait for the server response without blocking other code execution.

**Example:**
```javascript
async function fetchData() {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    console.log(data);
}
```
Here, **`fetch()`** is an asynchronous function that returns a promise. The **`await`** keyword waits for the promise to resolve, and only then does the function proceed to the next line.

### 2. **Handling Promises More Readably**
Instead of using the `.then()` and `.catch()` chaining that comes with promises, `async` functions let you write asynchronous code in a synchronous-like way, which makes it easier to read and maintain.

**Without `async`/`await` (using promises directly):**
```javascript
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

**With `async`/`await`:**
```javascript
async function getData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```
This is much cleaner and avoids deeply nested promise chains (also known as "callback hell").

### 3. **When You Need to Wait for Multiple Asynchronous Operations**
If you have multiple asynchronous operations that depend on one another, you can use `async` functions to run them in sequence or parallel.

- **In Sequence:**  
You can use multiple `await` statements to ensure each operation completes before the next one starts.

    ```javascript
    async function fetchUserAndPosts() {
        const user = await fetch('/api/user');
        const posts = await fetch(`/api/posts/${user.id}`);
        console.log(posts);
    }
    ```

- **In Parallel:**  
You can run asynchronous operations in parallel by using `Promise.all()` inside an `async` function.

    ```javascript
    async function fetchUserAndPosts() {
        const [user, posts] = await Promise.all([
            fetch('/api/user'),
            fetch('/api/posts')
        ]);
        console.log(user, posts);
    }
    ```

### 4. **When Working with `setTimeout`, `setInterval`, or Other Timers**
`async` functions can be useful when dealing with timers or delays. Instead of using a callback, you can wrap the timer in a promise and `await` its resolution.

**Example with `setTimeout`:**
```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function runWithDelay() {
    console.log('Start');
    await delay(2000);  // Wait for 2 seconds
    console.log('After 2 seconds');
}
```

### 5. **Performing File/Database Operations in Node.js**
When working with I/O operations in Node.js (e.g., reading or writing files, querying a database), those tasks are asynchronous. You can use `async`/`await` to handle these operations cleanly.

**Example (Node.js with `fs.promises`):**
```javascript
const fs = require('fs').promises;

async function readFileContent() {
    try {
        const data = await fs.readFile('file.txt', 'utf8');
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

### 6. **When You Need Error Handling in Asynchronous Code**
With `async` functions, error handling becomes simpler through `try`/`catch` blocks, instead of relying on `.catch()` with promises.

**Example:**
```javascript
async function loadData() {
    try {
        const data = await fetchData();
        console.log(data);
    } catch (error) {
        console.error('Error fetching data:', error);
    }
}
```
In this case, any errors during the async operation are caught by the `catch` block, ensuring that the program can handle errors gracefully.

### Conclusion
- **Use `async` functions** when you need to handle asynchronous operations such as network requests, file I/O, or timers.
- They make your code cleaner and more readable by allowing you to use the `await` keyword, which avoids messy promise chains.
- You can handle errors more effectively with `try`/`catch` in `async` functions.
- They allow you to run asynchronous operations in sequence or parallel depending on the use case.

