
# A Closer Look at Functions
- ES6 introduced Default Parameters
## Default Parameters
```js
///////////////////////////////////////
// Default Parameters
// Consider the following code where we are creating a new
const bookings = [];

const createBooking = function (flightNum, numPassengers, price) {

    // We are creating a new object using the enhanced literal syntax
    // where we do not have to specify key value pairs like:
    // const newBooking = {
    //     flightNum: flightNum,
    //     numPassengers: numPassengers,
    //     price: price
    // }

    const newBooking = {
        flightNum,
        numPassengers,
        price
    }
    console.log(newBooking);
    bookings.push(newBooking);
}

// Recall that we can call the createBooking() function with lesser num of args
createBooking('LH123'); // Prints: {flightNum: "LH123", numPassengers: undefined, price: undefined}

// What we would like is to use default values when no parameters are specified for the args
// We add default params by changing the function declaration
const createBookingNew = function (flightNum, numPassengers = 1, price = 199.99) {

    const newBooking = {
        flightNum,
        numPassengers,
        price
    }
    console.log(newBooking);
    bookings.push(newBooking);
}

createBookingNew('LH123'); // Prints: {flightNum: "LH123", numPassengers: 1, price: 199.99}
// An obviously we can override these defaults
createBookingNew('LH123', 2, 400); // Prints: {flightNum: "LH123", numPassengers: 2, price: 400}

// But another thing that we can do with default parameters is use the value of the previously supplied params to calculate them
// Note how we are using the value of the numPassengers to calculate the price
const createBookingNew2 = function (flightNum, numPassengers = 1, price = 199.99 * numPassengers) {

    const newBooking = {
        flightNum,
        numPassengers,
        price
    }
    console.log(newBooking);
    bookings.push(newBooking);
}
// The price is being calculated using the args passed in.
createBookingNew2('LH123', 10); // Prints: {flightNum: "LH123", numPassengers: 10, price: 1999.9}

// One thing to note is that you cannot use a param in the default value calc befor the param has been defined
// So you cannot do this:
const createBookingNew3 = function (flightNum, price = 199.99 * numPassengers, numPassengers = 1 ) {

    const newBooking = {
        flightNum,
        numPassengers,
        price
    }
    console.log(newBooking);
    bookings.push(newBooking);
}

// Note we are passing in 'undefined' as the param to the second arg. This is the same as not passing in an arg.
// Uncaught ReferenceError: Cannot access 'numPassengers' before initialization
createBookingNew3('LH123', undefined, 5); // Error
```
- Default function parameters allow named parameters to be initialized with default values if no value or undefined is passed.
- In JavaScript, function parameters default to `undefined`. However, it's often useful to set a different default value.
- Sometimes, you can use the terms argument and parameter interchangeably. However, by definition, parameters are what you specify in the [function declaration](https://www.javascripttutorial.net/javascript-function/) whereas the arguments are what you pass into the function.

## How Passing Arguments Works: Value vs. Reference

- Passing a primitive type to a function is really just the same as creating a copy like this, outside of the function. So the value is simply copied. On the other hand, when we pass an object to a function, it is really just like copying an object like this. And so whatever we change in a copy will also happen in the original.
- In JavaScript, you can pass by value and by reference. The main difference between the two is that passing by value happens when assigning primitives while passing by reference when assigning objects.
- In JavaScript primitive types are passed around as values: meaning that each time a value is assigned, a copy of that value is created.
- On the other side objects (including plain objects, array, functions, class instances) are references. If you modify the object, then all variables that reference that object are going to see the change.
- The comparison operator distinguishes comparing values and references. 2 variables holding references are equal only if they reference exactly the same object, but 2 variables holding values are equal if they simply have 2 same values no matter where the value originates: from a variable, literal, etc.

[Pass-By-Reference](https://stackoverflow.com/questions/13104494/does-javascript-pass-by-reference)

```js
///////////////////////////////////////
// How Passing Arguments Works: Values vs. Reference
const flight = 'LH234';
const jonas = {
  name: 'Jonas Schmedtmann',
  passport: 24739479284,
};

const checkIn = function (flightNum, passenger) {
  // We are changing the flightNum
  flightNum = 'LH999';
  // And we are also changing the name of the passenger
  passenger.name = 'Mr. ' + passenger.name;

  if (passenger.passport === 24739479284) {
    alert('Checked in');
  } else {
    alert('Wrong passport!');
  }
};

// checkIn(flight, jonas); // this will modify the jonas object
// Note that the flight remains unchanged because the value was copied
// console.log(flight); // Prints: LH234
// But the name changes, because the 'name' field is within an object, and objects are passed by reference
// (well the value of their reference is copied and passed in by value)
// So JS only has pass-by-value.
// This is in contrast to other languages like C++ where the primitives can also be passed by their reference
//console.log(jonas); // Prints: {name: "Mr. Jonas Schmedtmann", passport: 24739479284}

// Is the same as doing...
// const flightNum = flight;
// const passenger = jonas;

const newPassport = function (person) {
  person.passport = Math.trunc(Math.random() * 100000000000);
};

newPassport(jonas);
checkIn(flight, jonas);
```
## First-Class and Higher-Order Functions

- A programming language is said to have First-class functions when functions in that language are treated like any other variable. For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.
- **First-class** functions are JavaScript functions that can behave like variables. They can also be parsed as arguments to higher-order functions.
- **Higher-order** functions are functions that return a function or take in a function as an argument.
- So, first class functions is just a feature that a programming language either has or does not have. All it means is that all functions are values. There are no first class functions in practice, It's just a concept.
- Any difference between First Class Function and High Order Function - [Stackoverflow](https://stackoverflow.com/questions/10141124/any-difference-between-first-class-function-and-high-order-function)

  - There is a difference. When you say that a language has first-class functions, it means that the language treats functions as values – that you can assign a function into a variable, pass it around etc. Higher-order functions are functions that work on other functions, meaning that they take one or more functions as an argument and can also return a function.
  - The “higher-order” concept can be applied to functions in general, like functions in the mathematical sense. The “first-class” concept only has to do with functions in programming languages. It’s seldom used when referring to a function, such as “a first-class function”. It’s much more common to say that “a language has/hasn’t first-class function support”.
  - The two things are closely related, as it’s hard to imagine a language with first-class functions that would not also support higher-order functions, and conversely a language with higher-order functions but without first-class function support.

![HigherOrderFunctions.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/HigherOrderFunctions.png)


## Functions Accepting Callback Functions
- Higher-Order Function examples and how they are used in JS:
```js
// Two functions that will passed into the higher-order fn as args
const oneWord = function (str) {
    return str.replace(/ /g, '').toLowerCase();
};

const upperFirstWord = function (str) {
    const [first, ...others] = str.split(' ');
    return [first.toUpperCase(), ...others].join(' ');
};

// This is a higher-order function:
// because it is a functions accepting callback functions
const transformer = function (str, fn) {
    console.log(`Original string: ${str}`);

    // Note how we are calling the function
    const returnedVal = fn(str);
    console.log(`Transformed string: ${returnedVal}`);
    // Transformed string: JAVASCRIPT is the best!
    // Transformed string: javascriptisthebest!

    // Since functions are objects, functions can have methods of their own. Functions can even have properties
    // fn.name is one such property that returns the name of the function
    console.log(`Transformed by: ${fn.name}`);
    // Transformed by: upperFirstWord
    // Transformed by: oneWord

};

// We call the higher-order fn as follows:
transformer('JavaScript is the best!', upperFirstWord);
transformer('JavaScript is the best!', oneWord);

// JS uses callbacks all the time.
const high5 = function () {
    console.log('👋');
};
// Here, the addEventListener() is just like the transformer() function we wrote above
// and the high5 function is the callback function like the oneWord/upperFirstWord function
// On it's own, the addEventListener would have no idea what do do when a 'click' event occurred.
// It is the callback function that actually executes the required functionality.
// Hence callback functions are described as a means of implementing abstractions. Where addEventListener is more of a 
// 'higher-order' (hence the name) of abstraction
// and the high5() method is more of a lower level of abstraction.
document.body.addEventListener('click', high5);
```

## Functions Returning Functions

```js
///////////////////////////////////////
// Functions Returning Functions
const greet = function (greeting) {
  return function (name) {
    console.log(`${greeting} ${name}`);
  };
};

// Since 'greet' returns a function, 'greeterhey' is also a function
const greeterHey = greet('Hey');

// And hence we can call 'greeterHey' with args of its own
greeterHey('Jonas');
greeterHey('Steven');

// And we can also do something like this.
// greet('Hello') returns a function in which we then pass 'Charlie'
greet('Hello')('Charlie'); // Prints: Hello Charlie

// You can even rewrite the greet() function using just the arrow notation
const greetArr = greeting => name => console.log(`${greeting} ${name}`);

const greetArrowFn = greetArrow('Hey there');
greetArrowFn('Dave'); // Prints: Hey there Dave
```

## The call and apply Methods

- The `apply()/call()` method calls the specified function with a given `this` value, and `arguments` provided as an array.
- The `call()` method takes arguments separately. \
  The `apply()` method takes arguments as an array.

```js
///////////////////////////////////////
// The call and apply Methods

// Recall how the 'this' keyword worked in the case of simple objects
const alice = {
    name: 'Alice Doe',
    age: 21,
    birthYear: 1990,
    friends: [],
    addFriend(newFriend) {
        // The 'this' keyword will point to the object which called this method
        this.friends.push(newFriend);
        console.log(`${this.name} made a new friend named ${newFriend}`);
    },
    addFriendAndAge(newFriend, age) {
        this.friends.push(newFriend);
        console.log(`${this.name} made a new friend named ${newFriend} whose age is ${age}`);
    }
}

alice.addFriend('Bob Doe');

// Now suppose we wanted to create a new person named Bob.
// Bob would have the same property names as Alice.
// It would also have a addFriend() method.
// But we do not want to duplicate the method again for the Bob object.
const bob = {
    name: 'Bob Doe',
    age: 22,
    birthYear: 1989,
    friends: []
}

// Instead, what we do is we store the method from the alice object in an external variable and then reuse the function
const addNewFriendExt = alice.addFriend;

// Remember, if we tried to call the addNewFriendExt function here, we would have an error because this is an external function
// and like we had seen earlier, for a regular function call, the 'this' keyword is 'undefined'
addNewFriendExt('Alice'); // Uncaught TypeError: Cannot read property 'friends' of undefined

// So now the question is
// how do we tell JS explicitly which object it should refer to when using the addNewFriendExt() method?
// The requirement is: if we want to add a friend to the alice object, the 'this' keyword should refer to the 'alice' object
// and if we want to add a friend to the bob object, the 'this' keyword should refer to the 'bob' object

// There are 3 options: call, apply, bind

// 1) call

// Recall that functions are objects, and objects have methods.
// Hence we can access the 'call' method on a function
// The first argument in the call method is object that we want the 'this' keyword to point to.
// All the args after the first one are the args of the original function on which we are calling the 'call' method
addNewFriendExt.call(alice, 'Charlie Doe');
addNewFriendExt.call(bob, 'Dave Doe');

console.log(alice.friends); // Prints: ["Bob Doe", "Charlie Doe"]
console.log(bob.friends); // Prints: ["Dave Doe"]

// Note this method: addNewFriendExt.call(bob, 'Dave Doe');
// So the important point to consider is, even though we had the 'this' keyword inside the 'alice' object,
// we still managed to manually override the 'this' keyword by calling the function using the 'call' method and passing
// in our own 'this' variable

// Similar we can do this for any other object
const charlie = {
    name: 'Charlie Doe',
    age: 23,
    birthYear: 1988,
    friends: []
}
addNewFriendExt.call(charlie, 'Alice Doe'); // Prints: Charlie Doe made a new friend named Alice Doe
console.log(charlie.friends); // Prints: ["Alice Doe"]

// 2) apply

// This is similar to the call method we discussed above, except that the args to the function are provided as an array
const addFriendAndAgeExt = alice.addFriendAndAge;
addFriendAndAgeExt.call(charlie, 'Bob Doe', 21); // Prints: Charlie Doe made a new friend named Bob Doe whose age is 21
// Using apply, it would be:
addFriendAndAgeExt.apply(charlie, ['Dave Doe', 22]); // Prints: Charlie Doe made a new friend named Dave Doe whose age is 22

// But we avoid using this, as we can do just this:
const friendDetails = ['Eve Doe', 21];
addFriendAndAgeExt.call(charlie, ...friendDetails); // Prints: Charlie Doe made a new friend named Eve Doe whose age is 21

```

## The bind Method

- The `bind()` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
- In an event handler function, this keyword always points to the element on which that handler is attached to.
- Partial applications means that we can preset parameters.

```js
// Just like the 'call' and the 'apply' method, the 'bind' method allows us to set the 'this' keyword for any function call
// The difference is that, unlike the call and apply methods, bind does not immediately call the function.
// Instead, it returns a new function where the 'this' keyword is bound.
const dave = {
    name: 'Dave Doe',
    age: 23,
    birthYear: 1988,
    friends: [],

    addFriendAndGender(newFriend, gender) {
        this.friends.push(newFriend);
        console.log(`${this.name} made a new friend named ${newFriend} with gender ${gender}`);
    }
};

const addAnotherFriend = dave.addFriendAndGender;

const eve = {
    name: 'Eve Doe',
    age: 23,
    birthYear: 1988,
    friends: []
}
// We are using the bind method to set 'this' keyword to eve.
// Note that this will not call the 'addAnotherFriend' function.
// Instead it will return a new function where the 'this' keyword will always be set 'eve'
const addFriendForEve = addAnotherFriend.bind(eve);

// And we can call this function like:
addFriendForEve('Felicia', 'female');
// Prints: Eve Doe made a new friend named Felicia with gender female
// We no longer have to specify the 'this' keyword separately now!
// And we can test this:
console.log(eve.friends); // Prints: ["Felicia"]

// Notice how in the 'call' method, apart from the 'this', we could pass in args for the functions.
// We can do the same for 'bind' method as well.
// Now in this case, the name of the friend is fixed as 'Alex'
const addFriendsForEveNamedAlex = addAnotherFriend.bind(eve, 'Alex');
// And we call the function as follows, passing ONLY the second args now.
addFriendsForEveNamedAlex('female'); // Prints: Eve Doe made a new friend named Alex with gender female

// This kind of technique where we pre-set a part of the args beforehand is known as 'Partial Application'.

// Using the bind technique with Event Listeners
const lufthansa = {
    airline: 'Lufthansa',
    iataCode: 'LH',
    bookings: [],
    // book: function() {}
    book(flightNum, name) {
        console.log(
            `${name} booked a seat on ${this.airline} flight ${this.iataCode}${flightNum}`
        );
        this.bookings.push({ flight: `${this.iataCode}${flightNum}`, name });
    },
};

// Add a new property to the lufthansa object called 'planes'. This means that the company currently has 300 planes
lufthansa.planes = 300;
// Whenever you buy a plane, your number of planes is incremented by 1
lufthansa.buyPlane = function () {
    console.log(this);
    this.planes++;
    console.log(this.planes);
}
// So the intention is that whenever a user clicks on the 'Buy Planes' button, the buyPlane method should be called and increment
// the count of planes by 1 and log it to the console.
// But now, when we click on the button, the 'this' keyword logs: <button class="buy">Buy new plane 🛩</button>
// document.querySelector('.buy').addEventListener('click', lufthansa.buyPlane);


// Why does the 'this' keyword log the element, and not the 'lufthansa' object.
// In L96 we read that:
// If the function is called as an event listener, then the 'this' keyword will point to the DOM Element that the handler function is attached to.
// So this is expected behavior.
// In order to get around this problem, we now have to manually assign the 'this' keyword to this function so that we get the intended behavior.
// But which way should we follow? Should we use call, apply, or bind.
// ONLY bind allows us to manually assign the 'this' keyword without immediately calling the function.
// And since this is a callback function, that is what we want to happen
// Hence we use the 'bind' method in this case
// And we replace the above even listener with the following:
document.querySelector('.buy').addEventListener('click', lufthansa.buyPlane.bind(lufthansa));
// And now we get the correct behavior
// And we see that the 'this' logs:
// {airline: "Lufthansa", iataCode: "LH", bookings: Array(0), planes: 300, book: ƒ...}
// which is what we intended
```

## Coding Challenge ##1
Let's build a simple poll app!

A poll has a question, an array of options from which people can choose, and an array with the number of replies for each option. This data is stored in the starter object below.

Here are your tasks:

  - 1  Create a method called 'registerNewAnswer' on the 'poll' object. The method does 2 things:
  - 1.1 Display a prompt window for the user to input the number of the selected option. The prompt should look like this:
  - What is your favourite programming language?
    - 0: JavaScript
    - 1: Python
    - 2: Rust
    - 3: C++
    - (Write option number)
  - 1.2 Based on the input number, update the answers array. For example, if the option is 3, increase the value AT POSITION 3 of the array by 1. Make sure to check if the input is a number and if the number makes sense (e.g answer 52 wouldn't make sense, right?)
  - 2 Call this method whenever the user clicks the "Answer poll" button.
  - 3 Create a method 'displayResults' which displays the poll results. The method takes a string as an input (called 'type'), which can be either 'string' or 'array'. If type is 'array', simply display the results array as it is, using console.log(). This should be the default option. If type is 'string', display a string like "Poll results are 13, 2, 4, 1".
  - 4 Run the 'displayResults' method at the end of each 'registerNewAnswer' method call.

HINT: Use many of the tools you learned about in this and the last section 😉

BONUS: Use the 'displayResults' method to display the 2 arrays in the test data. Use both the 'array' and the 'string' option. Do NOT put the arrays in the poll object! So what shoud the this keyword look like in this situation?

BONUS TEST DATA 1: [5, 2, 3] BONUS TEST DATA 2: [1, 5, 3, 9, 6, 1]

```js
const poll = {
  question: 'What is your favourite programming language?',
  options: ['0: JavaScript', '1: Python', '2: Rust', '3: C++'],
  // This generates [0, 0, 0, 0]. More in the next section 😃
  answers: new Array(4).fill(0),
  registerNewAnswer() {
    // Get answer
    const answer = Number(
      prompt(
        `${this.question}\n${this.options.join('\n')}\n(Write option number)`
      )
    );
    console.log(answer);

    // Register answer
    typeof answer === 'number' &&
      answer < this.answers.length &&
      this.answers[answer]++;

    this.displayResults();
    this.displayResults('string');
  },

  displayResults(type = 'array') {
    if (type === 'array') {
      console.log(this.answers);
    } else if (type === 'string') {
      // Poll results are 13, 2, 4, 1
      console.log(`Poll results are ${this.answers.join(', ')}`);
    }
  },
};

document
  .querySelector('.poll')
  .addEventListener('click', poll.registerNewAnswer.bind(poll));

poll.displayResults.call({ answers: [5, 2, 3] }, 'string');
poll.displayResults.call({ answers: [1, 5, 3, 9, 6, 1] }, 'string');
poll.displayResults.call({ answers: [1, 5, 3, 9, 6, 1] });

// [5, 2, 3]
// [1, 5, 3, 9, 6, 1]
```

## Immediately Invoked Function Expressions (IIFE)
- Sometimes in JS, we need a function that is only executed once, and never executed again. We need this to implement something known as aync await.

```js
// We transform the function statement that we have into an expression by wrapping it in braces - '()'
// And then we call the function immediately by appending the ()
// This pattern is known as the Immediately Invoked Function Expressions (IIFE)
(
    function () {
        console.log('This method will be executed only once');
    }
)(); // Prints: This method will be executed only once
```

- Alternatively, you can use the arrow syntax to create an IIFE as follows:

```js
(() => {
    // Code that runs in your function
})()
```
- The parentheses surrounding the function definition lets JavaScript know that it will process a function expression. The last pair of parentheses invoke the function.

> When to Use an IIFE?

The most common use cases for IIFEs are:

- Aliasing global variables
- Creating private variables and functions
- Asynchronous functions in loops

```js
// The same can be done with arrow functions as well
const v = () => console.log('Inside the arrow function');
v(); // This can be called any number of times that you want

// Remove the variable assignment, convert it into an expression, call it immediately
(
    () => console.log('Inside the arrow function that can only be called once')
)(); // Prints: Inside the arrow function that can only be called once

// Just fiddling around to see if this works. And it does!
(console.log)('Does this work'); //  Prints: Does this work

// Why was this done?
// So that we can avoid overwriting our local variables by global variables that may be defined having the same name
// For example:
(
    function () {
        console.log('This method will be executed only once');
        const privateVariable = 21;
    }
)();

// The privateVariable declared above will not be accessible over here:
console.log(privateVariable); // Uncaught ReferenceError: privateVariable is not defined
// And hence, this pattern can be used to perform encapsulation

// If your concern is just protecting scopes, then you do not need to follow the IFFE pattern.
// You can just do this:
{
    const oneName = 'Ein name';
    let twoName = 'Du name';
    var threeName = 'Three name';
}

console.log(oneName); // Uncaught ReferenceError: oneName is not defined
console.log(twoName); // Uncaught ReferenceError: twoName is not defined
console.log(threeName); // Prints: Three name

```
[more on IIFE](https://stackabuse.com/javascripts-immediately-invoked-function-expressions/)

## Closures

- A closure is a function which has access to the variable from another function’s scope. This is accomplished by creating a function inside a function.
- A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
- JavaScript variables can belong to the local or global scope. Global variables can be made local (private) with closures.
- [Closures in Javascript for beginners](https://www.codingame.com/playgrounds/6516/closures-in-javascript-for-beginners)

```js
///////////////////////////////////////
// Closures
// Consider the following function that returns a function
const secureBooking = function () {
    let numOfPassengers = 0;
    return function () {
        numOfPassengers++;
        console.log(`${numOfPassengers} number of passengers.`);
    }
}

// Now let us call this function:
const booker = secureBooking();

// And then we call booker. And then this happens:
booker(); // Prints: 1 number of passengers.
booker(); // Prints: 2 number of passengers.
booker(); // Prints: 3 number of passengers.

// So the question is:
// how can the booker function, that is defined in the global scope, access the numOfPassengers variable defined in the child scope
// of the secureBooking function? Not only access, but also store and then change the values each time it is called.
// Also, numOfPassengers is defined as a local variable in the secureBooking function.
// The normal understanding is that once a function finishes its execution, the local variables to the function can no longer be accessed.
// But in this case we can access and change the values of the variable -
// even after the function secureBooking has returned - through the booker function
```
- Any function always has access to the variable environment of the execution context in which the function was created, even after that execution context is gone.

![Closures.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Closures.png)

- We can access the closure of a variable by doing:
```js
// We can log the variables stored in the closure like this:
console.dir(booker);
```
- And now if look into the console, you will see something like this. Note that when the name of a property is enclosed in `[[ ]]`, as shown below, it means that the property is an internal property that cannot be accessed by us through the code.

![Closures_Logged.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Closures_Logged.png)


## More Closure Examples
- a closure always makes sure that a function does not lose the connection to the variables that were present at its birthplace.
- closure does in fact have priority over the scope chain.

```js
///////////////////////////////////////
// More Closure Examples
// Example 1: the closure of a function can be re-assigned

let f;

const g = function () {
    const a = 23;
    f = function () {
        console.log(a * 2);
    };
};

g();

// So even though the f variable has been defined outside of the g function,
// it still closes over the variable environment in the g function
f(); // Prints: 46

const h = function () {
    const b = 7;
    f = function () {
        console.log(b * 2);
    };
};

// Reassigning the f variable by calling the h() function
h();
f(); // Prints: 14
// So, in effect, the SAME f variable has been assigned to two different functions with two different variable environments


// Example 2: Showing usage of closures in a Timer.

// Note: We do not need to always return a function in order to see a closure in action.
const boardPassengers = function (n, wait) {
    const perGroup = n / 3;

    setTimeout(function () {
        console.log(`n = ${n} passengers`); // Prints: n = 180 passengers. As was passed in the fn arg. And not 1000, as is defined in the parent scope
        console.log(`There are 3 groups, each with ${perGroup} passengers`);
    }, wait * 1000);

    console.log(`Will start boarding in ${wait} seconds`);
};
boardPassengers(180, 5);

// Showing that the variables declared in the closure take priority over the variables declared in the parent scope
const perGroup = 1000;

// Example 3: Using Closures in IFFE
(function () {
    const header = document.querySelector('h1');
    header.style.color = 'red';

    document.querySelector('body').addEventListener('click', function () {
        header.style.color = 'blue';
    });
})();
```

## Coding Challenge ##2

This is more of a thinking challenge than a coding challenge 🤓

Take the IIFE below and at the end of the function, attach an event listener that changes the color of the selected h1 element ('header') to blue, each time the BODY element is clicked. Do NOT select the h1 element again!

And now explain to YOURSELF (or someone around you) WHY this worked! Take all the time you need. Think about WHEN exactly the callback function is executed, and what that means for the variables involved in this example.e

```js
(function () {
  const header = document.querySelector('h1');
  header.style.color = 'red';
  document.querySelector('body').addEventListener('click', function () {
    header.style.color = 'blue';
  });
})();

```

[BACK ⬅️](https://github.com/subhadeeppaul/JavaScript-Notes)
