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
