
# How JavaScript Works Behind the Scenes

## An High-Level Overview of JavaScript

#### What is Javascript?
Javascript Is a High-Level, Object-Oriented, Multi-Paradigm Programming Language.

Javascript Is 
***High-level***: In languages like C, you have to manage the memory yourself. High-level languages abstract away the memory management (apart from doing other things).

***Garbage-collected***: One of the tools that takes memory management away from developers is automatic garbage collection.

***Interpreted or just-in-time compiled***: 

***Multi-paradigm***: Paradigm refers to a style of writing code. This can be imperative or declarative. JS can support multiple styles of writing code, such as, Procedural (organizing code in a very linear way so that the code runs top-to-bottom with functions in between), Object-Oriented, Functional

***Prototype-based object-oriented***
***First-class functions***:functions are treated as regular variables, i.e., we can pass them into other functions, and return them from functions. This is what enables functional programming in JS.

![First-Class-Function.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/First-Class-Function.png)
***Dynamically typed***: In JS we do not assign datatypes to variables. The dataytpes are known only once JS engine executes our code. Also the type of variables can easily be changed by reassigning variables.
***Single-threaded***: JS runs in one single thread.
***Non-blocking Event-Loop***: Long running tasks are executed by the event loop in the "background" and then put back in the main thread once their execution is complete.

## The JavaScript Engine and Runtime
### What is Javascript Engine
JS Engine is, simply put, the code that executes the JS code. Every browser has it's own JS engine. The most well-known JS engine is Google's V8. The V8 engine powers Google Chrome, but also nodeJS. Other browsers have their own JS engines.
- A JS engine contains a call stack and a heap. The Call Stack is where our JS code is executed using something known as the Execution Context. The heap is an unstructured memory pool that stores all the objects that our application needs.

![JS-Engine-and-Runtime.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/JS-Engine-and-Runtime.png)


[What is the difference between Compiled language vs an Interpreted Language on SO](https://stackoverflow.com/questions/3265357/compiled-vs-interpreted-languages)

- Before the code can be run by the target system (think your laptop CPU), it needs to be converted to machine code (sequence of 0s and 1s). So your JS code has to be converted to machine code. Now how is this going to happen? Compilation is the process by which the entire source code (your code) is converted into machine code at once, and written to a binary file that can be executed on any computer. Any application that you run your machine has been already previously compiled into a binary executable.
![Compiled language vs an Interpreted Language 1.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Compiled%20language%20vs%20an%20Interpreted%20Language%201.png)

An interpreted language, on the other hand, consists of an interpreter that runs through the source code and executes it line-by-line. So, basically, the code is read and executed at the same time. JS used to be an interpreted language, but modern JS isn't. This is primarily because interpreted languages are slow, and JS couldn't keep up with the development of the browser.
![Compiled language vs an Interpreted Language 2.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Compiled%20language%20vs%20an%20Interpreted%20Language%202.png)

Modern JS uses a combination of Compilation and Interpretation, which is known as Just-In-Time (JIT) compilation.
![Compiled language vs an Interpreted Language 3.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Compiled%20language%20vs%20an%20Interpreted%20Language%203.png)
- TODO: I still don't understand what is actually happening with the JIT Compilation.
- The first step is parsing the code that reads the JS code and converts it into a datastructure known as the AST (Abstract Syntax Tree). The compilation process takes the generated AST and converts it into machine code. This machine code is executed right away because of the JIT compilation of JS. The machine code that is generated initially is a very un-optimised version of the code just so that the execution can begin as soon as possible. In the background, the machine code is taken and recompiled while the program is already executing. During each iteration of the optimisation, the unoptimised code is swapped for the optimised code - all while the program is already executing!!

![JS-Engine-Compilation-Flow.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/JS-Engine-Compilation-Flow.png)

- A JS Runtime is something that is required to run JS in the browser. It is a combination of JS Engine (discussed above), the Web APIs, and the Callback Queue. The Callback Queue is a datastructure that contains all the callback functions that are ready to be executed. What are callback functions? The functions that you attached to the event listeners are known as callback functions. So when an event happens - like a click - the corresponding callback function will be called.
![JS_Runtime_In_The_Browser.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/JS_Runtime_In_The_Browser.png)

- This is how it happens - when a user clicks on a button, the callback function is added to the callback queue. Then, once the call stack is empty, the callback function is passed to the call stack so that it can be executed. This happens by something known as the Event Loop. The event loop picks up functions from the callback queue and places them in the call stack so that they can be executed. The event loop is basically how javascript's non-blocking concurrency model is implemented.

![JS_Runtime_In_The_Browser_2.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/JS_Runtime_In_The_Browser_2.png)

- Remember that JS can also exist outside of browsers (nodeJS). In that case, the JS runtime will not contain the Web APIs, because the Web APIs are provided by the browser. In this case, the WebAPIs are replaced by C++ bindings and the thread pool.

## Execution Contexts and The Call Stack
### What is an Execution Context?

- Once the code is code is compiled and ready to be executed, a Global Execution Context is created for the top level code. Top-level code here means any code that is not inside any function.
- For example, the name variable is a part of the top-level code. Hence it will be executed in the Global execution Context. Then we have two functions - one expression and one declaration. These functions will be declared so that they can be called later. The point is that - the code inside the function will be executed only when the function is called.
- An Execution Context is defined as an environment in which a piece of JS code is executed. The context stores all the necessary information that is required by a code to be executed - such as local variables or arguments passed to a function.
- In every JS project, there is only one global execution context and this global execution context is where the top level code executes.

![Execution_Context.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Execution_Context.png)

- Now that we have a top-level execution context, we can begin execution of the code. For each function in the code, a new execution context is created that contains all the necessary information that that particular function requires to run. The same also goes for methods because they are just functions attached to objects. All these execution contexts together make up the call stack. Once all the functions have been executed, the JS Engine will wait for the callback function to arrive so that it can begin executing those.

![Execution_Context_2.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Execution_Context_2.png)

What is inside an Execution Context:
- **Variable Environment:** This environment stores all the variables and the function declarations. Apart from this, it also stores a special object called the `arguments` object. This object contains all the arguments that were passed into the function that the current Execution Context belongs to. Remember that each function gets its own execution context as soon as the function is called.
- **Scope Chain:** Apart from the local variables defined inside the function, the Execution Context can also access variables that are defined outside the function. The scope chain consists of references to variables that are outside the current function.
- `this` **keyword** : One important sidenote is that Execution Contexts belonging to the arrow functions do not get their own `this` keyword or `arguments` object. Instead, they use the `this` and `arguments` of their nearest normal function parent.
- Recall, as we discussed earlier, the Call Stack with the Memory Heap forms the JS Engine. The Call Stack is the place where the Execution Contexts get stacked on top of each other to keep track of where we are in the execution. The Execution Context on the top of the stack is the one that is currently running.
![Execution_Context_Stored_In_Call_Stack.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Execution_Context_Stored_In_Call_Stack.png)


## Scope and The Scope Chain

### Scope Concepts
- **Scoping:** How our program's variables are organized and accessed. "Where do variables live?" or "Where can we access a certain variable, and where not?",
- **Lexical scoping:** Scoping is controlled by placement of functions and blocks in the code;
- **Scope:** Space or environment in which a certain variable is declared (variable environment in case of functions). There is global scope, function scope, and block scope;
- **Scope of a variable:** Region of our code where a certain variable can be accessed.


### The 3 types of Scopes

![Scopes_In_JS.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Scopes_In_JS.png)

**What is the Scope Chain?**
- Each function creates it's own scope. Hence, *first()* and *second()* get their own scopes.
- Every scope has access to all of the variables from all of its outer/parent scopes. All of this also applies to function `arguments`. So this is basically how the Scope Chain works - if one scope needs to use a variable but is unable to find it in the current scope, it will look up it's scope chain and see if it can find the variable in one of it's parent scopes. If it can, then it will use that variable. If it can't, then you get an error. This process is also called *variable lookup in scope chain*. Note that a scope cannot look for variables in it's children scopes.
- Note that starting from ES6, the if-block is also able to create it's own scope. But this scope will only work for the ES6 variable types - `let` and `const`. - Take note of the *millenial* variable in the below figure. The variable is declared with the `var` keyword. Hence, it is not scoped to the block, but rather scoped to the parent function, which in this case is *first()*. Hence, unlike the *decade* variable, we see the *millenial* variable in the scope of the *first()* function.

![Scope_Chain.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Scope_Chain.png)

### Scope Chain vs. The Call Stack
- The scope of a function is the same as the Variable Environment in the function's Execution Context. Apart from this, the scope also inherits the scope from all of it's parent scopes because of the scope chain that we discussed above.
- The order of function calls has no effect on the scope chain. What I mean by this is, consider the following:
![ScopeChain_vs_CallStack.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/ScopeChain_vs_CallStack.png)

### Summery
- Scoping asks the question "Where do variables live?" or "Where can we access a certain variable, and where not?";
- There are 3 types of scope in JavaScript: the global scope, scopes defined by functions, and scopes defined by blocks;
- Only let and const variables are block-scoped. Variables declared with var end up in the closest function scope;
- In JavaScript, we have lexical scoping, so the rules of where we can access variables are based on exactly where in the code functions and blocks are written;
- Every scope always has access to all the variables from all its outer scopes. This is the scope chain!
- When a variable is not in the current scope, the engine looks up in the scope chain until it finds the variable it's looking for. This is called variable lookup;
- The scope chain is a one-way street: a scope will never, ever have access to the variables of an inner scope;
- The scope chain in a certain scope is equal to adding together all the variable environments of the all parent scopes;
- The scope chain has nothing to do with the order in which functions were called. It does not affect the scope chain at all!

## Scoping in Practice

```js
function calcAge(birthYear) {
  const age = 2037 - birthYear;

  function printAge() {
    let output = `${firstName}, you are ${age}, born in ${birthYear}`;
    console.log(output); // output: firstName = Jonas → coming from global scope.

	// Block Scope
    if (birthYear >= 1981 && birthYear <= 1996) {
      var millenial = true;
      // Creating NEW variable with same name as outer scope's variable
      const firstName = 'Steven'; // firstName already declared in Global Scope

      // Reasssigning outer scope's variable
      output = 'NEW OUTPUT!'; 

      const str = `Oh, and you're a millenial, ${firstName}`; // output: Steven - This happens because Javascript tries to look the variable name in the current scope.
      console.log(str); // output: Oh, and you're a millenial, xoraus

      function add(a, b) { 
        return a + b; // The scope of this add function is only where it is defined
      }
    }
    console.log(str); // output: // str is not defined
    console.log(millenial); //output: true
    console.log(add(2, 3)); // output: add is not defined. (in strict mode)
    console.log(output); //output: NEW OUTPUT
  }
  printAge();

  return age;
}

const firstName = 'paul';
calcAge(1997);  // output: paul you are 50, born in 1997
console.log(age); // output: age is not defined 
printAge(); // output: printAge is not defined

```
- const and let variables are block scoped.
- so variables declared with the var keyword are function scoped. So they simply ignore the block, because they are not block scoped at all. They're just function scoped.
- that the scope of a variable is the entire region of the code in which the variable is accessible.
- Functions are block scoped in Strict Mode
- So the scope chain isn't necessary at all, if the variable that we're looking for is already in the current scope.

## Variable Environment: Hoisting and The TDZ
- Hoisting: makes some types of variables accessible/usable in the code before they are actually declared. In other words, variables are "lifted" to the top of their scope. Behind the scenes, what actually happens is that, before execution, the code is scanned for variable declarations and for each variable a new property is created in the *variable environment object*
- The practical implementations of hoisting is that you can use a variable in the code BEFORE it is actually declared! The value associated with the hoisted variables also varies - refer the table below.

![Hoisting_In_JS.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Hoisting_In_JS.png)

- function declarations are hoisted - this means that these types of functions can be used/called before they are declared.
- Variables declared with `var` are also hoisted, but the hoisting works differently when compared to functions in the sense that the variables are hoisted, but their value is `undefined` and not the value that they are declared with.
- `let` and `const` variables are not hoisted. Hence these variables cannot be used before they are declared. TDZ stands for the Temporal Dead Zone, which is indicating the region in the code where the variable is in-scope but cannot be used because it has not been declared yet.
- For function expressions and arrow functions, the hoisting depends on whether they were created using `var`, `const`, or `let`. What this means is that function expressions and arrow functions declared with a `var` is hoisted, but to `undefined`. But if they have been declared using `let` or `const`, the functions are not usable before they have been declared in the code - because of the TDZ.
- There is one another difference between variables declared with a `var` and `let`/ `const` - the variables declared with var are added as properties to the global `window` object in JS, whereas the variables declared with `let/const` are not.

![Temporal_Dead_Zone.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Temporal_Dead_Zone.png)

### Hoisting Example
```js
Take a look at this code

test();
 
function test() {
  console.log("Hello");
}

// We can call the test() function before it was declared in code. That's the hoisting in practice.

// Why it's possible?

// JavaScript engine scans the code before executing it and creates a property for each variable or function in the code. For normal variables, it assigns an undefined value, and for functions it assigns a reference to that function in memory. That's why we can call a function, but if we try to access a variable, we will get undefined.

function scope() {
  console.log(var1); // undefined
  console.log(va1); // undefined
 
  var var1 = "Hello";
  var var2 = "Hi";
}
Let me know if you have any questions
```

### Hoisting and TDZ in Practice
```js
// # Hoisting with Variables
console.log(me); // output: Undefined (because of Var)
// console.log(job); // output: Cannot access 'job' before initialization, the origin of this error is that the jobn variable is still in temporal dead zone
// console.log(year); // output: Cannot access 'year' before initialization

var me = 'Jonas';
let job = 'teacher';
const year = 1991;

// Functions
console.log(addDecl(2, 3)); //output: 5 
// console.log(addExpr(2, 3)); // output: Cannot access 'addExpr' before initialization
	console.log(addArrow); // output: Undefined
// console.log(addArrow(2, 3));

function addDecl(a, b) {
  return a + b;
}

const addExpr = function (a, b) {
  return a + b;
};

var addArrow = (a, b) => a + b;

// Example
console.log(undefined);
	if (!numProducts) deleteShoppingCart(); // output: All products deleted because at this moment the numProducts is 'Undefined' because it is declared with 'var' and that's because how the var works with hosting

var numProducts = 10;

function deleteShoppingCart() {
  console.log('All products deleted!');
}

var x = 1; // we get a property of x = 1. we cannot find y or z here in this object and that's because they were declared with let or const
let y = 2;
const z = 3;

console.log(x === window.x); // output: true
console.log(y === window.y); // output: false
console.log(z === window.z); // output: false

```
- variables declared with var, will create a property on the global window object. And that can have some implications in some cases.


## The this Keyword

- The `this` keyword is a special variable that is created for every Execution Context (i.e. for each function). We saw earlier that the `this` keyword is one of the three things that are a part of the Execution Context that is created for every function. In general terms, the `this` keyword takes the value of the "owner" of the function in which the `this` keyword is used.
- The value of `this` is not static and varies depending on the way that the function is called.
- A function can be called in multiple ways.
- A function can be a method - i.e. a function that is present on a object. When we use the `this` keyword in a method, the `this` keyword points to the object calling the method.
- A function can be called separately - like a usual stand-alone function call. In that case, the `this` keyword is `undefined`. But `this` is only in the case when we are using the "strict" mode. If we are not using the strict mode, tehn in that case the `this` keyword is going to point at the global object, which in `this` case is the `window` object.
- Arrow functions are not a way to call functions but they still need to be considered. Arrow functions do not get their own `this` keyword. Instead, if you use the `this` keyword in an arrow function, it is just going to be the `this` keyword of the surrounding/parent function.
- If the function is called as an event listener, then the `this` keyword will point to the DOM Element that the handler function is attached to.

![This_Keyword.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/This_Keyword.png)


## The this Keyword in Practice
```js
'use strict'
// The this Keyword in Practice
console.log(this); // output: Window Object

const calcAge = function (birthYear) {
  console.log(2037 - birthYear);
  console.log(this); // output: Undefined (in case of strict mode)
};
calcAge(1991);

const calcAgeArrow = birthYear => {
  console.log(2037 - birthYear);
  console.log(this); // output: Window (because the arrow function doesn't get the this function So instead the arrow function simply uses the lexical this keyword, which means that it uses the disc keyword of its parent function or of its parents scope.
};
calcAgeArrow(1980);

const jonas = {
  year: 1991,
  calcAge: function () {
    console.log(this); // output: jonas object - The reason that the this keyword will point to Jonas in this case is because jonas was the object calling that method
    console.log(2037 - this.year); // output: 46
  },
};
jonas.calcAge();

const matilda = {
  year: 2017,
};

matilda.calcAge = jonas.calcAge; // method borrowing 
matilda.calcAge(); // output: 20  (this will point to year: 2017) - So even though the method is written here inside of the Jonas object the this keyword will still point to Matilda. If it is Matilda, who calls the method.

const f = jonas.calcAge;
f(); // Cannot read property 'year' of undefined
```
## Regular Functions vs. Arrow Functions
- One important point is that arrow functions should never be used as methods on an object. You should always use function expressions. This is to do with the fact that arrow functions do not get their own `this` keyword, instead they inherit the `this` keyword from their parent scope. This can be a source of bugs.
```js
// Consider another object that uses an arrow function instead of the
// function expression that was used above
const felicia = {
    firstName: 'Felicia',

    // Avoid using arrow functions as methods since they can lead to errors
    greet: () => {
        console.log(this);
        console.log(`Hi ${this.firstName}`);
    },

    // Prefer function expressions as methods instead
    greet2: function () {
        console.log(this); // Now 'this' refers to the object calling the method, which is felicia
        console.log(`Hi ${this.firstName}`);
    }

}
// Like we said, an arrow function does not get it's own 'this' keyword
// instead it adopts the 'this' keyword of it's enclosing scope
// Note that even though the function is defined inside an object, the object is just an object literal ie.
// the object does not get it's own scope. Hence the enclosing scope of the greet function is still the global/window object
// Hence 'this' will refer to the global/window object
// And since there is no 'firstName' property on the window object, `Hi ${this.firstName}` will print undefined.
felicia.greet(); // Prints: undefined
felicia.greet2(); // Prints: 'Hi Felicia'
```
- Another important point is when we have to use functions inside methods.
- Consider the following function inside a method. Why does line 11 print undefined? If you look closely, you can see that the *isMillennial* function is being called as a simple function call. So, even though the function is within a method, it is still a regular function call. And the rule says that inside a normal function call, the `this` keyword is `undefined`.
```js
const gina = {
    firstName: 'Gina',
    birthYear: 1990,

    greet: function () {
        console.log(this); // Prints the object gina
        console.log(`Hi ${this.firstName}`);

        // This is a function expression inside a method
        const isMillenial = function () {
            console.log(this); // Prints: undefined
            // Now this produces an error:
            // Uncaught TypeError: Cannot read property 'birthYear' of undefined
            if (this.birthYear >= 1981 && this.birthYear <= 1996) {
                console.log(`You are also a Millennial!`);
            }
        }

        isMillenial();
    }
}
gina.greet();
```
- One way to get around this problem in solutions prior to ES6 was as follows:
```js
const gina2 = {
    firstName: 'Gina',
    birthYear: 1990,

    greet: function () {
        console.log(this); // Prints the object gina
        console.log(`Hi ${this.firstName}`);

        const self = this; // sometimes the variable 'that' is also used in place of 'self'
        const isMillenial = function () {
            console.log(self); // Prints the object gina
            if (self.birthYear >= 1981 && self.birthYear <= 1996) {
                console.log(`You are also a Millennial!`);
            }
        }
        isMillenial();
    }
}
gina2.greet();
```
- However, starting form ES6, we can use the arrow function to get around this problem. Recall that the arrow function does not have the `this` keyword of its own and instead inherits the `this` keyword of its parent scope. So, we can do this:
- TODO: but we are still calling the *isMillennial()* functio as a normal function inside the *gina3* object. Then shouldn't the `this` keyword be `undefined?`
```js
const gina3 = {
    firstName: 'Gina',
    birthYear: 1990,

    greet: function () {
        console.log(this); // Prints the object gina3
        console.log(`Hi ${this.firstName}`);

        const isMillenial = () => {
            console.log(this); // Prints the object gina3. Because this is inside the arrow function that inherits the parent scope
            if (this.birthYear >= 1981 && this.birthYear <= 1996) {
                console.log(`You are also a Millennial!`);
            }
        }
        isMillenial();
    }
}
gina3.greet();
```
- Another thing is the arguments variable that we discussed earlier:
```js
// arguments Keyword
const sumOfNumbers = function (a, b) {
    console.log(arguments); // This logs the args that are passed in into the function - 10, 20
    return a+b;
}
sumOfNumbers(10, 20);

// Interestingly enough, this function can also be called with more than two parameters
const anotherSummation = function (a, b) {
    console.log(arguments);
    // 'arguments' is an array. Hence we could cycle through each element and do computations on the arguments if required
    return a + b;
};
anotherSummation(2,3,4,5,6);

// However, the arrow function does nto get it's own arguments keyword. Just like the 'this' keyword
const arrowSummation = (a, b) => {
    console.log(arguments); // Uncaught ReferenceError: arguments is not defined
    return a + b;
};
arrowSummation(2,3,4);
```
## Primitives vs. Objects (Primitive vs. Reference Types)
![PrimitivesTypes_vs_ReferenceTypes.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/PrimitivesTypes_vs_ReferenceTypes.png)


```js
let age = 30;
let oldAge = age;
age = 31;
console.log(age);
console.log(oldAge);

const me = {
  name: 'Jonas',
  age: 30,
};
const friend = me;
friend.age = 27;
console.log('Friend:', friend);
console.log('Me', me);
```
Link-Image

## Primitives vs. Objects in Practice
```js
// Primitive types
let lastName = 'Williams';
let oldLastName = lastName;
lastName = 'Davis';
console.log(lastName, oldLastName); // output: Davis Williams

// Reference types
const jessica = {
  firstName: 'Jessica',
  lastName: 'Williams',
  age: 27,
};
const marriedJessica = jessica;
marriedJessica.lastName = 'Davis';
console.log('Before marriage:', jessica); // output: Before marriage: { firstName: 'Jessica', lastName: 'Davis', age: 27 }
console.log('After marriage: ', marriedJessica); // output: After marriage: { firstName: 'Jessica', lastName: 'Davis', age: 27 }

// Copying objects
const jessica2 = {
  firstName: 'Jessica',
  lastName: 'Williams',
  age: 27,
  family: ['Alice', 'Bob'],
};

const jessicaCopy = Object.assign({}, jessica2);
jessicaCopy.lastName = 'Davis';

jessicaCopy.family.push('Mary');
jessicaCopy.family.push('John');

console.log('Before marriage:', jessica2); // family: [ 'Alice', 'Bob', 'Mary', 'John' ]
console.log('After marriage: ', jessicaCopy); // amily: [ 'Alice', 'Bob', 'Mary', 'John' ]
```
- And that's why we say that this object.assign only creates a shallow copy
- However, the family object is a deeply nested object. And so therefore, object.assign did not really, behind the scenes, copy it to the new object.
- Now, a deep clone is what we would need here. Usually, we do something like this using an external library, for example, like LoDash, and this library has a ton of helpful tools and one is of them is for deep cloning.

#### Later in course

- Prototypal Inheritance Object Oriented Programming (00P) With JavaScript
- Event Loop Asynchronous JavaScript: Promises, Async/Await and AJAX
- How the DOM Really Works Advanced DOM and Events

[BACK ⬅️](https://github.com/subhadeeppaul/JavaScript-Notes)
