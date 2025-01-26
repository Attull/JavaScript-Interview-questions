# JavaScript-Interview-questions

### 1. Event Bubbling and Event capturing

In JavaScript, event bubbling and event capturing are two phases of event propagation in the Document Object Model (DOM). They determine the order in which event handlers are triggered when an event occurs on a nested element.

#### Event Bubbling:
* This is the default behavior in JavaScript.
* Then, the event "bubbles" up the DOM tree, triggering event handlers on each ancestor element until it reaches the root of the document.

```html
 <div class="parent">
        <div class="childd">
            <div class="grandChild">

            </div>
        </div>
     </div>
```

```js


const parent =  document.querySelector(".parent")
const childd =  document.querySelector(".childd")
const grandChild =  document.querySelector(".grandChild")


parent.addEventListener('click',(e)=>{
    console.log("Parent")
    
})

childd.addEventListener('click',(e)=>{
    console.log("Child")
    
})

grandChild.addEventListener('click',(e)=>{
    console.log("Grand Child")
    
})

```

#### Event Capturing
* This is the opposite of event bubbling.
* The event starts at the root of the document and "captures" down through ancestor elements until it reaches the target element that triggered the event.

```js
grandChild.addEventListener('click',(e)=>{
    console.log("Grand Child")
},true)   // The 'true' argument enables capturing


```

#### Stopping Propagation:
You can stop the event from bubbling or capturing further by using the stopPropagation() method within the event handler.

```js
grandChild.addEventListener('click',(e)=>{
    console.log("Grand Child")
    e.stopPropagation()
},true)   // The 'true' argument enables capturing
```

### 2. How JavaScript handles Asynchronous task

In JavaScript, the call stack and the event loop are crucial components that manage the execution of code, especially in asynchronous operations.

#### Call Stack:
* The call stack is a data structure that follows the LIFO (Last-In, First-Out) principle.
* When a function is called, it's added to the top of the call stack.
* When the function completes, it's removed from the stack.
* This allows JavaScript to track the execution flow and maintain the order of function calls.

#### Event Loop:
* The event loop is a mechanism that continuously checks the call stack and the task queue (also known as the callback queue).
* When the call stack is empty, the event loop takes the first task from the queue and pushes it onto the call stack for execution. 
* This process enables asynchronous operations in JavaScript, allowing the program to continue running while waiting for tasks like network requests or timers to complete.

How They Work Together:
#### Synchronous Execution:
When JavaScript code is executed, functions are added to the call stack and executed one by one. If a function calls another function, the nested function is added to the stack, and so on.

#### Asynchronous Operations:
When an asynchronous operation (like a setTimeout or an API call) is encountered, it's initiated, and a callback function is registered. The operation is then offloaded to the browser's Web APIs, and the execution continues without waiting for the operation to complete.

#### Callback Queue:
When an asynchronous operation completes, its associated callback function is added to the task queue.

#### Event Loop:
The event loop continuously monitors the call stack. If the call stack is empty, it checks the task queue. If there are tasks in the queue, the event loop takes the first task and pushes it onto the call stack for execution.

### var, let & const

#### Hoisting

Hoisting refers to the process where JavaScript moves declarations to the top of their respective scope

#### Temporal Dead Zone

The Temporal Dead Zone (TDZ) is a concept in JavaScript that refers to a specific period during the execution of a program where a variable exists but cannot be accessed. This period occurs between the start of a scope (function or block) and the point where the variable is declared using the `let` or `const` keywords. 
It will throw a ReferenceError

#### Why is TDZ important?
* Prevents accidental variable usage
* Improves code clarity:

### Currying

Currying is a functional programming technique where a function with multiple arguments is transformed into a series of functions, each taking a single argument.

```js
// your normal function
const add = (a, b) => {
  return a + b;
}

console.log(add(1,2)); // 3

// using currying
const add = (a) => {
  return (b) => {
    return a + b;
  }
}

console.log(add(1)(2)); // 3
```
## JavaScript Event Loop
 Single-Threaded Execution:
 - JavaScript is single-threaded, which means it can only execute one task at a time. This is managed by the call stack, where functions are executed one by one.

 Call Stack:
 - Think of the call stack as a stack of plates. Every time a function is called, a new plate (function) is added to the stack. When the function finishes, the plate is removed from the stack.

 Web APIs:
 - For asynchronous operations like `setTimeout`, DOM events, and HTTP requests, JavaScript relies on Web APIs provided by the browser. These operations are handled outside of the call stack.

 Callback Queue:
 - When an asynchronous operation completes, its callback is placed in the callback queue. This queue waits until the call stack is clear before pushing the next callback onto the stack.

 Event Loop:
 - The event loop is like a manager that constantly checks if the call stack is empty. When it is, the event loop takes the first callback from the callback queue and adds it to the call stack.

 Microtasks Queue:
 - There's also a microtasks queue for tasks like promises. This queue has higher priority than the callback queue. The event loop checks the microtasks queue first, ensuring these tasks are processed before other callbacks.

 Priority Handling:
 - To sum it up, the event loop first checks the microtasks queue. If it's empty, it moves to the callback queue. This ensures that critical tasks, like promises, are handled promptly.

## Explain Asynchronous Operations in JavaScript

JavaScript is a powerful language used to build dynamic web pages and applications. One of its key features is the ability to handle asynchronous operations. But what does that mean?

𝗪𝗵𝗮𝘁 𝗶𝘀 𝗔𝘀𝘆𝗻𝗰𝗵𝗿𝗼𝗻𝗼𝘂𝘀 𝗶𝗻 𝗝𝗮𝘃𝗮𝗦𝗰𝗿𝗶𝗽𝘁?

In JavaScript, asynchronous operations allow your code to start a task and then move on to other tasks before that first task is finished. This is like putting a pot of water on the stove to boil and then chopping vegetables while waiting. You don’t have to stand around waiting for the water to boil, you can do something else.

𝗪𝗵𝘆 𝗶𝘀 𝗔𝘀𝘆𝗻𝗰𝗵𝗿𝗼𝗻𝗼𝘂𝘀 𝗜𝗺𝗽𝗼𝗿𝘁𝗮𝗻𝘁?

Imagine you are using a website and you click a button to load some data. If JavaScript had to wait for this data to load before doing anything else, the website would become unresponsive. By using asynchronous operations, JavaScript can fetch data in the background and keep the website interactive.

𝗛𝗼𝘄 𝗗𝗼𝗲𝘀 𝗝𝗮𝘃𝗮𝗦𝗰𝗿𝗶𝗽𝘁 𝗛𝗮𝗻𝗱𝗹𝗲 𝗔𝘀𝘆𝗻𝗰𝗵𝗿𝗼𝗻𝗼𝘂𝘀 𝗢𝗽𝗲𝗿𝗮𝘁𝗶𝗼𝗻𝘀?

JavaScript handles asynchronous operations mainly through three methods:
1. 𝗖𝗮𝗹𝗹𝗯𝗮𝗰𝗸𝘀: A function that is passed as an argument to another function. Once the main function is done, the callback function is executed. However, using callbacks can sometimes make your code look messy, which is called Callback hell.
2. 𝗣𝗿𝗼𝗺𝗶𝘀𝗲𝘀: Promises provide a cleaner way to handle asynchronous code. A promise represents a value that may be available now, or in the future, or never. You can use .then() to specify what should happen when the promise is fulfilled, and .catch() to handle errors.
3. 𝗔𝘀𝘆𝗻𝗰/𝗔𝘄𝗮𝗶𝘁: This is a newer and more readable way to write asynchronous code. Using async before a function means it will always return a promise. await can be used inside async functions to pause the execution until the promise is resolved.

## W𝐡𝐚𝐭 𝐢𝐬 𝐬𝐡𝐚𝐥𝐥𝐨𝐰 𝐜𝐨𝐩𝐲 𝐚𝐧𝐝 𝐝𝐞𝐞𝐩 𝐜𝐨𝐩𝐲?

𝐒𝐡𝐚𝐥𝐥𝐨𝐰 𝐂𝐨𝐩𝐲: A shallow copy duplicates the immediate values of an object or array. However, if the original contains nested objects or arrays, the references to these nested elements are copied, not the objects themselves. This means changes to nested objects in the copied version will affect the original.

𝐃𝐞𝐞𝐩 𝐂𝐨𝐩𝐲: A deep copy duplicates all levels of an object or array, creating entirely independent copies of all nested objects and arrays. Changes in the deep copy do not affect the original.

## Currying

Currying is a technique where a function takes one argument at a time, returning another function to handle the next argument, and so on, until all arguments are provided. This makes functions more reusable and flexible.

Why Use Currying?

Instead of duplicating code, currying breaks functions into smaller, reusable pieces. This is especially useful in real-world scenarios like applying different tax rates based on location in an e-commerce app.

Example:
```
function applyTax(rate) {
 return function(amount) {
 return amount + amount * rate;
 };
}

const applyIndiaTax = applyTax(18); // 18% tax in India
const applyUSTax = applyTax(7); // 7% tax in the US

console.log(applyIndiaTax(1000)); // 1180
console.log(applyUSTax(1000)); // 1070
```
With currying, you can quickly create reusable tax functions for different regions, keeping your code clean and efficient!

