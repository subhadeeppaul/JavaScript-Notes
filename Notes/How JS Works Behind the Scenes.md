
# How JavaScript Works Behind the Scenes

## An High-Level Overview of JavaScript

#### What is Javascript?
Javascript Is a High-Level, Object-Oriented, Multi-Paradigm Programming Language.

Javascript Is a High-Level Prototype-Based Object-Oriented Multi-Paradigm Interpreted or Just-in-Time Compiled Dynamic| Single-Threaded Garbage-Collected Programming Language With First-Class Functions and a Non-Blocking Event Loop Concurrency Model

***High-level***
Link-Image

***Garbage-collected***
Link-Image

***Interpreted or just-in-time compiled***
Link-Image

***Multi-paradigm***
Link-Image

***Prototype-based object-oriented***
Link-Image

***First-class functions***
Link-Image

***Dynamic***
Link-Image

***Single-threaded & Non-blocking event loop***
Link-Image


## The JavaScript Engine and Runtime
### What is Javascript Engine
Link-Image

- So a JavaScript engine is simply a computer program that executes JavaScript code.
- Now every browser has its own JavaScript engine but probably the most well known engine is Google's V-Eight.
- So any JavaScript engine always contains a call stack and a heap. The call stack is where our code is actually executed using something called execution contexts. Then the heap is an unstructured memory pool which stores all the objects that our application needs.

### Compilation vs Interpretation
Link-Image

### Just in Time Compilation of Javascript
Link-Image

### Runtime in Browser
Link-Image

### Runtime in NodeJs
Link-Image

## Execution Contexts and The Call Stack
### What is an Execution Context?

Link-Image

But now what exactly is an execution context? Well, an execution context is an abstract concept. But I define it basically as an environment in which a piece of JavaScript is executed. a It's like a box that stores all the necessary information for some code to be executed. Such as local variables or arguments passed into a function. So, JavaScript code always runs inside an execution context.

Now, in any JavaScript project, no matter how large it is, there is only ever one global execution context. It's always there as the default context, and it's where top-level code will execute.

### Execution Context in Detail

Link-Image

Because remember each function gets its own execution context as soon as the function is called. So basically all the variables that are somehow declared inside a function, will end up in its variable environment. However, a function can also access variables outside of the function and this works because of something called the scope chain.

Scope chain basically consists of references to variables that are located outside of the current function. And to keep track of the scope chain, it is stored in each execution context.

Execution contexts belonging to arrow functions, do not get their own arguments keyword, nor do they get the this keyword, okay? So, basically arrow functions don't have the arguments object and the this keyword. Instead, they can use the arguments object, and the this keyword from their closest regular function parent.

### The Call Stack
Link-Image

JavaScript has only one thread of execution. And so it can only do one thing at a time.

So like to use the analogy of the call stack being like a map for the JavaScript engine. Because the call stack ensures that the order of execution never gets lost.

## Scope and The Scope Chain

### Scope Concepts
- **Scoping:** How our program's variables are organized and accessed. "Where do variables live?" or "Where can we access a certain variable, and where not?",
- **Lexical scoping:** Scoping is controlled by placement of functions and blocks in the code;
- **Scope:** Space or environment in which a certain variable is declared (variable environment in case of functions). There is global scope, function scope, and block scope;
- **Scope of a variable:** Region of our code where a certain variable can be accessed.


### The 3 types of Scopes

Link-Image

### Scope Chain vs. The Call Stack
Link-Image

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

const firstName = 'xoraus';
calcAge(1997);  // output: xoraus you are 50, born in 1997
console.log(age); // output: age is not defined 
printAge(); // output: printAge is not defined

```
- const and let variables are block scoped.
- so variables declared with the var keyword are function scoped. So they simply ignore the block, because they are not block scoped at all. They're just function scoped.
- that the scope of a variable is the entire region of the code in which the variable is accessible.
- Functions are block scoped in Strict Mode
- So the scope chain isn't necessary at all, if the variable that we're looking for is already in the current scope.

## Variable Environment: Hoisting and The TDZ
Link-Image

- So we learned that an execution context always contains three parts. A variable environment, the scope chain in the in current context, and the this keyword.
- So in JavaScript we have a mechanism called hoisting. And hoisting basically make some types of variables accessible, or let's say usable in the code before they are actually declared in the code. Now, many people simply define hoisting by saying that variables are magically lifted off moved to the top of their scope for example, to the top of a function. And that is actually what hoisting looks like on the surface.
- Instead, behind the scenes the code is basically scanned for variable declarations before it is executed. So this happens during the so-called creation phase of the execution context that we talked about before. Then for each variable that is found is in the code, a new property is created in a variable environment object. And that's how hoisting really works. Now, hoisting does not work the same for all variable types.
- This means that a function expression or arrow function created with var is hoisted to undefined. But if created with let or const, it's not usable before it's declared in a code because of the Temporal Dead Zone so again, just like normal variables. And is this is actually the reason that we cannot use function expressions before we write them in the code, unlike function declarations.

Link-Image

- So to recap, basically each and every let and const variable get their own Temporal Dead Zone that starts at the beginning of the scope until the line where it is defined. And the variable is only safe to use after the TDZ, so the Temporal Dead Zone.
- Alright, now what is actually the need for JavaScript to have a Temporal Dead Zone? Well, the main reason that the TDZ was introduced in ES6 is that the behavior I described before makes it way easier to avoid and catch errors. Because using a variable that is set to undefined before it's actually declared can cause serious bugs which might be hard to find.
- So accessing variables before declaration is bad practice and should be avoided. And the best way to avoid it iS by simply getting an error.
- A second and smaller reason why the TDZ exists is to make const variables actually work the way they are supposed to. So as you know, we can't reassign const variables. it So it will not be possible to set them to undefined first and then assign their real value later.
- Now, if hoisting creates so many problems, why does it exist in the first place? I get this question all the time. And so let's quickly talk about that here. So the creator of JavaScript basically implemented hoisting so that we can use function declarations before we use them. Because this is essential for some programming techniques, such as mutual recursion. Some people also think that it makes code a lot more readable. Now, the fact that it also works for var declarations is because that was the only way hoisting could be implemented at the time. So the hoisting of var variables is basically just a byproduct of hoisting functions.

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

Link-Image

- Instead, if you use 'the this variable' in an arrow function, it will simply be the this keyword of the surrounding function. So of the parent function and in technical terms, this is called the 'lexical this keyword,' because it simply gets picked up from the outer lexical scope of the arrow function.
- It's also important to know what the, this keyword is not. So this will never point to the function in which we are using it. Also, the this keyword will never point to the variable environment of the function. And these are two pretty common misconceptions

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
```js
// Regular Functions vs. Arrow Functions
// var firstName = 'Matilda';

const jonas = {
  firstName: 'Jonas',
  year: 1991,
  calcAge: function () {
    // console.log(this);
    console.log(2037 - this.year);

    // Solution 1
    // const self = this; // self or that
    // const isMillenial = function () {
    //   console.log(self);
    //   console.log(self.year >= 1981 && self.year <= 1996);
    // };

    // Solution 2
    const isMillenial = () => {
      console.log(this);
      console.log(this.year >= 1981 && this.year <= 1996);
    };
    isMillenial(); 
  },

  greet: () => {
    console.log(this); //output: Window
    console.log(`Hey ${this.firstName}`); //output: Matilda
  },
};
jonas.greet(); // output: Hey Undefined - (using the this keyword from it's parent's this keyword)
jonas.calcAge();

// arguments keyword
const addExpr = function (a, b) {
  console.log(arguments);
  return a + b;
};
addExpr(2, 5);
addExpr(2, 5, 8, 12);

var addArrow = (a, b) => {
  console.log(arguments);
  return a + b;
};
addArrow(2, 5, 8);
```
- Now, just like the this keyword, the arguments keyword is only available in regular functions.

## Primitives vs. Objects (Primitive vs. Reference Types)
Link-Image

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