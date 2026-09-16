## JavaScript Execution, Asynchronous JavaScript and Promises

### 1. How does JavaScript execute code?

It creates execution context, pushes all variable with undefined value and normal functions with defination on
top of scope and then executes code line by line.

JavaScript executes synchronous code using the **Call Stack**.

```text
JavaScript Code
      then
   Call Stack
      then
Execution
```

---

### 2. What is diff between Sync & Async ?

Code executes one statement at a time and waits for each statement to finish.

#### Synchronous

```js
console.log("A");
console.log("B");
console.log("C");
```

Output:

```text
A
B
C
```

#### Asynchronous

Long-running operations can be started without blocking the execution of other JavaScript code.

```js
setTimeout(() => {
    console.log("B");
}, 1000);

console.log("A");
```

Output:

```text
A
B
```

---

### 3. What are the ways to make the code Async?


Common ways:

- Callbacks
- Promises
- async/await
- Timers such as setTimeout
- Browser APIs
- Node.js asynchronous APIs

---

### 4. What are Web Browser APIs?

Browser APIs are features provided by the browser that JavaScript can use.

Examples:

- setTimeout()
- fetch()
- DOM APIs
- Event listeners
- Geolocation
- Web Storage

They perform operations outside the JavaScript call stack.

---

### 5. What is the Event Loop?

The Event Loop manages the Call Stack, Web APIs, and queues.

Simplified flow:

```text
JavaScript
    then
Call Stack
    then
Web API
    then
Callback Queue
    then
Event Loop
    then
Call Stack
```

The Event Loop checks whether the Call Stack is empty and then moves ready callbacks to the Call Stack.

Promise callbacks use the Microtask Queue, which is processed before normal task/callback queues.

---

### 6. What is Callback Hell?

Callback Hell happens when multiple asynchronous operations depend on each other and callbacks become deeply nested.

```js
first(() => {
    second(() => {
        third(() => {
            fourth(() => {});
        });
    });
});
```

It makes code difficult to read, maintain, and handle errors.

---

### 7. What is Inversion of Control?

When we pass a callback to another function, we give that function control over when and how our callback is executed.

```js
doSomething(() => {
    console.log("Done");
});
```

We don't control when `doSomething()` calls our callback.

This is called Inversion of Control.

---


### 8. What is a Promise?

A Promise represents the eventual result of an asynchronous operation.

A Promise has three states:

```text
Pending
   ↓
Fulfilled
```

or

```text
Pending
   ↓
Rejected
```

---

### 9. How to create a Promise?

```js
const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("Success");
    }, 1000);
});
```

- resolve() → fulfills the Promise
- reject() → rejects the Promise

---

### 10. What are different states of a Promise -pending, fulfilled, rejected


#### Pending

Operation is still running.

#### Fulfilled

Operation completed successfully.

#### Rejected

Operation failed.

A Promise cannot change its state after it becomes fulfilled or rejected.

---

### 11. How to consume an existing Promise?

Use `.then()`, `.catch()`, and `.finally()`.

```js
promise
    .then(result => {
        console.log(result);
    })
    .catch(error => {
        console.log(error);
    });
```

We can also use async await to consume a promise.

---

### 12. How to chain Promises using .then() ?

.then() returns a new Promise, allowing chaining.

```js
getUser()
    .then(user => getOrders(user))
    .then(orders => console.log(orders));
```

---

### 13. How to handle errors in a promise chain using .catch


```js
getUser()
    .then(user => getOrders(user))
    .then(orders => console.log(orders))
    .catch(error => console.log(error));
```

A .catch() can handle rejection from earlier promises in the chain.

---

### 14. finally() in a Promise Chain

finally() executes whether the Promise is fulfilled or rejected.

```js
promise
    .then(result => console.log(result))
    .catch(error => console.log(error))
    .finally(() => {
        console.log("Operation finished");
    });
```

---

### 15. What happens when an Error gets thrown inside .then when there is a .catch ?


```js
Promise.resolve()
    .then(() => {
        throw new Error("Something went wrong");
    })
    .catch(error => {
        console.log(error.message);
    });
```

Output:

```text
Something went wrong
```

The thrown error rejects the Promise returned by `.then()`, and `.catch()` handles it.

---

### 16. Error thrown inside `.then()` without `.catch()` ?

```js
Promise.resolve()
    .then(() => {
        throw new Error("Error");
    });
```

There is no handler for the rejection, so it becomes an unhandled rejection.

---

### 17. Why place `.catch()` towards the end?

```js
first()
    .then(second)
    .then(third)
    .then(fourth)
    .catch(handleError);
```

A final `.catch()` can handle errors from multiple previous steps in the chain.

---

### 18. How to consume multiple promises by chaining?

```js
getUser()
    .then(user => getOrders(user))
    .then(orders => getPayment(orders))
    .then(payment => console.log(payment))
    .catch(error => console.log(error));
```

Each operation starts after the previous operation completes.

---


### 19. How to consume multiple promises by Promise.all?

Use `Promise.all()` when operations can run independently.

```js
const result = await Promise.all([
    getUsers(),
    getProducts(),
    getOrders()
]);

console.log(result);
```

It fulfills when **all promises fulfill**.

If any Promise rejects, `Promise.all()` rejects.

---

### 20. How to do error handling when using promises?

Use:

```js
promise
    .then(result => {})
    .catch(error => {})
    .finally(() => {});
```

With `async/await`:

```js
try {
    const result = await promise;
} catch (error) {
    console.log(error);
}
```

---

### 21. Why is error handling the most important part of using a promise?

Asynchronous operations can fail because of:

* Network errors
* File errors
* Invalid data
* API errors
* Database errors

Without error handling, failures can become unhandled rejections or crash the application.

---

### 22. How to promisify an asynchronous callbacks based function - eg. setTimeout, fs.readFile

#### Promisifying `setTimeout`


```js
function delay(ms) {
    return new Promise(resolve => {
        console.log("inside promise")
        setTimeout(resolve, ms);
    });
}

delay(1000).then(() => {
    console.log("Done");
});
```

---

#### Promisifying `fs.readFile`

```js
function readFilePromise(path) {
    return new Promise((resolve, reject) => {
        fs.readFile(path, "utf8", (error, data) => {
            if (error) {
                reject(error);
            } else {
                resolve(data);
            }
        });
    });
}
```

---


### 24. `Promise.resolve()`

Creates an already fulfilled Promise.

```js
Promise.resolve("Success")
    .then(result => console.log(result));
```

---

### 25. `Promise.reject()`

Creates an already rejected Promise.

```js
Promise.reject("Error")
    .catch(error => console.log(error));
```

---

### 26. `Promise.all()`

Waits for all Promises to fulfill.

```js
Promise.all([p1, p2, p3])
    .then(results => console.log(results));
```

If one rejects, the returned Promise rejects.

---

### 27. `Promise.allSettled()`

Waits for **all Promises to finish**, regardless of success or failure.

```js
Promise.allSettled([p1, p2, p3])
    .then(results => console.log(results));
```

Example result:

```js
[
    { status: "fulfilled", value: "A" },
    { status: "rejected", reason: "Error" }
]
```

---

### 28. `Promise.any()`

Returns the first Promise that **fulfills**.

```js
Promise.any([p1, p2, p3])
    .then(result => console.log(result));
```

If all Promises reject, it rejects with `AggregateError`.

---

### 29. `Promise.race()`

Returns the first Promise that **settles** — fulfilled or rejected.

```js
Promise.race([p1, p2, p3])
    .then(result => console.log(result))
    .catch(error => console.log(error));
```

---

```text
all         --> all must succeed
allSettled  --> everyone reports
any         --> first success
race        --> first result
```



### REFERENCES:

## References

- MDN Web Docs — JavaScript Promises  
  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises

- MDN Web Docs — Promise  
  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

- MDN Web Docs — Promise.all()  
  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all

- MDN Web Docs — Promise.race()  
  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race

- MDN Web Docs — Asynchronous JavaScript  
  https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Async_JS

- Node.js Documentation — File System  
  https://nodejs.org/api/fs.html

- ChaiWithCode (Youtube)
  https://youtube.com/playlist?list=PLu71SKxNbfoBuX3f4EOACle2y-tRC5Q37&si=X8eLrbzJGHupYXeE
