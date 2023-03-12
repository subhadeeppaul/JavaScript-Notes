
# 2. JavaScript Fundamentals Part 2

## Activating Strict Mode

```js
  'use strict'; // to activate strict mode to 
```

- Always put strict mode in the beginning of the file
- It makes it easier for developer to avoid accidental errors.

First, strict mode forbids us to do certain things and second, it will actually create visible errors for us in certain situations in which without strict mode JavaScript will simply fail silently without letting us know that we did a mistake.

```js
'use strict';

let hasDriversLicense = false;
const passTest = true;

if (passTest) hasDriversLicense = true; // if in  hasDriver(s)License s is missing the code will behave  unexpectedly
if (hasDriversLicense) console.log('I can drive :D');

// const interface = 'Audio'; // Uncaught SyntaxError: Missing initializer in const declaration
// const private = 534; // Uncaught SyntaxError: Missing initializer in const declaration
```





## Functions
```js
// A function that does not return anything (return type is 'undefined')

function logger() {
  console.log('My name is paul');
}

// calling / running / invoking function
logger(); // output: My name is paul
logger(); // output: My name is paul
logger(); // output: My name is paul

// A function with a return type

function fruitProcessor(apples, oranges) {
  const juice = `Juice with ${apples} apples and ${oranges} oranges.`;
  return juice;
}

const appleJuice = fruitProcessor(10, 5);
console.log(appleJuice);1

const appleOrangeJuice = fruitProcessor(4, 8);
console.log(appleOrangeJuice);

const num = Number('6833');
```

Clean Code - DRY Principle that is Don't Repeat Yourself

## Function Declarations vs. Expressions

There are 3 types of ways in which you can declare functions:
- Function Declaration
- Function Expression
- Arrow Function

```js
//There are 2 ways in which a function can be defined. Consider the following 2 functions for calculating age for example

// Using Function declaration
function calcAge1(currYear, birthYear) {
    return currYear - birthYear;
}

// Using Function Expression
// There is another way that we can define functions. This is a function without a name - which is why it is called
// an "Anonymous Function". Here, the function itself is being stored in a variable.
const calcAge2 = function (currYear, birthYear) {
    return currYear - birthYear;
}

// Note how the 2 functions are being called. There is no difference basically.
console.log(calcAge1(2020, 1989));
console.log(calcAge2(2020, 1989));

// Note that a function declaration can be called before the function definition.
// But a function expression MUST be called only AFTER it has been defined.

// Function is being called BEFORE it is defined. Perfectly fine.
console.log(calcAge3(2020, 1989));
function calcAge3(currYear, birthYear) {
    return currYear - birthYear;
}

// Function is being called before it is defined.
// Error: Uncaught ReferenceError: Cannot access 'calcAge4' before initialization
// console.log(calcAge4(2020, 1989));
const calcAge4 = function (currYear, birthYear) {
    return currYear - birthYear;
}
```
- The parameter is a kind of placeholder in the function and the argument is then the actual value that we use to fill in that placeholder that is the parameter.
- In Javascript functions are just values


## Arrow Functions
An arrow function is a shorter way to write a function expression.

```js
const calcAge5 = function (currYear, birthYear) {
    return currYear - birthYear;
}

// This can be written in arrow functions as: Note that the return is implicit in this case
const calcAge6 = (currYear, birthYear) => currYear - birthYear;
// Function is again called as the same way:
calcAge6(2020, 1989);

// When the function body contains more than one line, the function is written as follows.
// Note the explicit return statement that was omitted previously
const calcAge7 = (currYear, birthYear) => {
    console.log("Calculating age..");
    return currYear - birthYear;
}

```
- Arrow function does not get the 'this' keyword




## Coding challenge 1

Back to the two gymnastics teams, the Dolphins and the Koalas! There is a new gymnastics discipline, which works differently. Each team competes 3 times, and then the average of the 3 scores is calculated (so one average score per team). A team ONLY wins if it has at least DOUBLE the average score of the other team. Otherwise, no team wins!

    1.Create an arrow function 'calcAverage' to calculate the average of 3 scores.
    2.Use the function to calculate the average for both teams.
    3. Create a function 'checkWinner' that takes the average score of each team as parameters ('avgDolhins' and 'avgKoalas'), and then logs the winner to the console, together with the victory points, according to the rule above. Example: "Koalas win (30 vs. 13)".
    4. Use the 'checkWinner' function to determine the winner for both DATA 1 and DATA 2.
    5. Ignore draws this time.

TEST DATA 1: Dolphins score 44, 23 and 71. Koalas score 65, 54 and 49 TEST DATA 2: Dolphins score 85, 54 and 41. Koalas score 23, 34 and 27

HINT: To calculate average of 3 values, add them all together and divide by 3 HINT: To check if number A is at least double number B, check for A >= 2 * B. Apply this to the team's average scores 😉

*Solution*
```js
calcAverage = (scoreA, scoreB, scoreC) => (scoreA, scoreB, scoreC) / 3

const teamDolphinAvg = Math.floor(calcAverage(85,54,41));
const teamKoalaAvg = Math.floor(calcAverage(23,34,27));

console.log(teamDolphinAvg,teamKoalaAvg)

function checkWinner(teamDolphinAvg,teamKoalaAvg) {
 if (teamDolphinAvg >= 2 * teamKoalaAvg) {
	 console.log(`Dolphins win 🏆 ${teamDolphinAvg} vs ${teamKoalaAvg}`)
 } else if (teamKoalaAvg >= 2 * teamDolphinAvg) {
	 console.log(`Koalas win 🏆 ${teamKoalaAvg} vs. ${teamDolphinAvg}`)
 } else {
	 console.log(`No body won :(`)
 }
}

checkWinner(800,351)

// Test 2
scoreDolphins = calcAverage(85, 54, 41);
scoreKoalas = calcAverage(23, 34, 27);
console.log(scoreDolphins, scoreKoalas);
checkWinner(scoreDolphins, scoreKoalas);

```


## Introduction to Arrays

```js
// A new array can be created in the following two ways
const friends = ["Alice", "Bob", "Charlie"]; // Array Literal syntax
const years = new Array(1991, 1992, 1993, 2020); // Array Function Syntax

// We can fetch elements from the array using the following:
console.log(friends[0], friends[1], friends[2], friends[3]); // Prints: Alice Bob Charlie undefined
// Check the length of the array using:
console.log(friends.length);
// Mutate the elements of the array
friends[2] = "Claire";
friends[3] = "Dave"; // Note how we can add elements to the array
console.log(friends); // Prints: ["Alice", "Bob", "Claire", "Dave"]
friends[5] = "Eve"; // We skipped index 4 to see what would be added to the array. It's 'empty'
console.log(friends); // Prints: ["Alice", "Bob", "Claire", "Dave", empty, "Eve"]
console.log(typeof friends[4]); // and the type Prints: undefined

// Note that even though we defined the friends variable as const, we are still able to change the contents of the array
// This is because only primitive values are immutable, but array is not a primitive value.
// Hence, the contents of the friends array can change, but if you try to point the variable friends to a different array,
// then you will see an error:
// friends = []; // Attempt to assign to const or readonly variable

// An array can also hold values of different types at the same time
// Consider the following array that is supposed to store all the values related to one person
const friendsOfAlice = ["Bob", "Charlie", "Dave"];
const alice = ["Alice", "Doe", 21, friendsOfAlice]
console.log(alice); // Prints: ["Alice", "Doe", 21, Array(3)]


```


## Basic Array Operations (Methods)

```js

// Add elements to the end of the array. push returns the length of the array resulting after pushing the element.
const friendsOfBob = ["Alice", "Charlie", "Dave"];
friendsOfBob.push("Eve");
console.log(friendsOfBob); // Prints: ["Alice", "Charlie", "Dave", "Eve"]

// Add elements to the beginning of the array. Like the push, unshift also returns the length of the resulting array.
friendsOfBob.unshift("Anna");
console.log(friendsOfBob); // Prints: ["Anna", "Alice", "Charlie", "Dave", "Eve"]

// Remove the last element of the array. Returns the removed element.
let removedElement = friendsOfBob.pop();
console.log(friendsOfBob); // Prints: ["Anna", "Alice", "Charlie", "Dave"]
console.log(removedElement); // Prints: Eve

// Remove the first element of the array
removedElement = friendsOfBob.shift();
console.log(friendsOfBob); // Prints: ["Alice", "Charlie", "Dave"]
console.log(removedElement); // Prints: Anna

// Find the index at which a particular element is at
let idx = friendsOfBob.indexOf("Dave");
console.log(idx); // Prints: 2
// If the element is not present, it prints -1
idx = friendsOfBob.indexOf("Eve");
console.log(idx); // Prints: -1

// Find if an element exists in the array.
let elementExists = friendsOfBob.includes("Dave");
console.log(elementExists); // Prints: true
elementExists = friendsOfBob.includes("Eve");
console.log(elementExists); // Prints: false
// Note that includes method uses a strict equality for this check.
let allTheYears = [2012, 2016, 2020];
console.log(allTheYears.includes(2020)); // Prints: true
console.log(allTheYears.includes("2020")); // Prints: false - because the array contains number type, and not string

```
## Coding Challenge ##2

Ahmed is still building his tip calculator, using the same rules as before: Tip 15% of the bill if the bill value is between 50 and 300, and if the value is different, the tip is 20%.

- Write a function 'calcTip' that takes any bill value as an input and returns the corresponding tip, calculated based on the rules above (you can check out the code from first tip calculator challenge if you need to). Use the function type you like the most. Test the function using a bill value of 100.

- And now let's use arrays! So create an array 'bills' containing the test data below.
- Create an array 'tips' containing the tip value for each bill, calculated from the function you created before.

- BONUS: Create an array 'total' containing the total values, so the bill + tip.

TEST DATA: 125, 555 and 44

HINT: Remember that an array needs a value in each position, and that value can actually be the returned value of a function! So you can just call a function as array values (so don't store the tip values in separate variables first, but right in the new array)

```js
const calcTip = function (bill) {
  return bill >= 50 && bill <= 300 ? bill * 0.15 : bill * 0.2;
}
// const calcTip = bill => bill >= 50 && bill <= 300 ? bill * 0.15 : bill * 0.2;

const bills = [125, 555, 44];
const tips = [calcTip(bills[0]), calcTip(bills[1]), calcTip(bills[2])];
const totals = [bills[0] + tips[0], bills[1] + tips[1], bills[2] + tips[2]];

console.log(bills, tips, totals);
```


## Introduction to Objects

```js
// In JS, we define an object as a collection of key-value pairs
// Each of the keys are also called 'properties'. So we can say that the bob object contains 4 properties
// There are many ways to create an object - this is called Object Literal Syntax
// One of the differences between objects and arrays is that in an object, the order of the properties does not matter
// when we are trying to retrieve them
let bob = {
    firstName: "Bob",
    lastName: "Doe",
    age: 21,
    friends: ["Alice", "Charlie", "Dave"]
};
console.log(bob); // Prints: {firstName: "Bob", lastName: "Doe", age: 21, friends: Array(3)}

// You can also use this to get a more visually appealing view of the object:
console.table(bob);
```
## Dot vs Bracket Notation
There are two ways in which you can retrieve the properties from an object

```js
console.log(bob.firstName); // Prints: Bob
console.log(bob["firstName"]); // Prints: Bob
```
```js
// The difference between the two methods is that in the second case, you can replace the string with an expression.
// Recall that an expression is something that returns a value, hence we can use that computed value as the key. Like:
// The advantage of using the [] notation to access the property of an object is that you can take an input from the
// end user, store that value in a variable, and then use that variable to fetch the corresponding value from the object
const stringName = "Name";
console.log(bob["last" + stringName]); // Prints: Doe

// The result of trying to access a property on an object that is not defined is 'undefined'
console.log(bob.job); // Prints: undefined

// You can also use the dot operator and the Bracket notations to ADD properties to an object as well
bob.job = "Painter";
bob["hobbies"] = ["Accounting", "Journalism"];
console.log(bob);

// Combining all that stuff together.
// Note that bob.friends.length works because the dot operator executes from left-to-right.
// Hence, bob.friends executes first, which results in an array, and then we call the length property on that array
// thus giving us the length.
console.log(`${bob.firstName} has ${bob.friends.length} friends, the first of which is ${bob.friends[0]}.`);
// Prints: Bob has 3 friends, the first of which is Alice.


```


## Object Methods

```js
// So we learnt that object, just like arrays, can hold different types of data. These types of data can be primitives, arrays, or even
// other objects themselves. Now let us take it one step further.
// Recall from the Functions section where we discussed that functions are just another type of value.
// And is a function is just a value, it means that we can create a key-value pair where a function is just another value.
// And that then means that we can add functions to objects. So let's see how:

let charlie = {
    firstName: "Charlie",
    lastName: "Doe",
    birthYear: 1990,
    friends: ["Alice", "Bob", "Dave"],
    hasDriversLicense: true,

    // And now we add the function.
    // Any function that is attached to an Object is known as a 'Method'
    calcAge: function(currYear, birthYear){
        return currYear - birthYear;
    },

    /*
    The above function is pretty similar to just writing this, which is what we were doing earlier.
    The only difference now is that instead of writing the function as a variable, we are writing it as a property.
    const calcAge = function(currYear, birthYear){
        return currYear - birthYear;
    }
    But defining a function inside the object like this will not work. It will produce a syntax error.
    Because this is a Function Declaration. What we are looking for is a Function Expression.
    function calcAge2(currYear, birthYear){
        return currYear - birthYear;
    }
    */
};

// And now we can call this function as follows. Note both the ways that we are calling the function:
console.log(charlie.calcAge(2020, charlie.birthYear));
console.log(charlie["calcAge"](2020, charlie.birthYear));

// But we do not want to access the birthYear variable through the charlie reference.
// In every method, JS gives us access to a special variable called 'this'.
// So what we can do is, read the variable directly:
let anotherCharlie = {
    firstName: "Charlie",
    lastName: "Doe",
    birthYear: 1990,
    friends: ["Alice", "Bob", "Dave"],
    hasDriversLicense: true,

    // We are reading the birthYear property directly through the 'this' reference
    calcAge: function(currYear){
        return currYear - this.birthYear;
    },
};

console.log(anotherCharlie.calcAge(2020));

// What we can also do is store the result of the calculation of the age in a new property in the object itself
anotherCharlie = {
    firstName: "Charlie",
    lastName: "Doe",
    birthYear: 1990,
    friends: ["Alice", "Bob", "Dave"],
    hasDriversLicense: true,

    calcAge: function(currYear){
        // We are creating a new property and storing the result of the calculation
        this.age = currYear - this.birthYear;
        return this.age;
    },
};

console.log(`Using property: ${anotherCharlie.age}`); // Prints: Using property: undefined (because the property has not been created yet)
console.log(`Using function: ${anotherCharlie.calcAge(2020)}`); // Prints: Using function: 30
console.log(`Using property: ${anotherCharlie.age}`); // Prints: Using property: 30



```


## Coding Challenge ##3

Let's go back to Mark and John comparing their BMIs! This time, let's use objects to implement the calculations! Remember: BMI = mass / height ** 2 = mass / (height * height). (mass in kg and height in meter).
- For each of them, create an object with properties for their full name, mass, and height (Mark Miller and John Smith)
- Create a 'calcBMI' method on each object to calculate the BMI (the same method on both objects). Store the BMI value to a property, and also return it from the method.
- Log to the console who has the higher BMI, together with the full name and the respective BMI. Example: "John Smith's BMI (28.3) is higher than Mark Miller's (23.9)!"

TEST DATA: Marks weights 78 kg and is 1.69 m tall. John weights 92 kg and is 1.95 m tall.

```js
const mark = {
  fullName: 'Mark Miller',
  mass: 78,
  height: 1.69,
  calcBMI: function () {
    this.bmi = this.mass / this.height ** 2;
    return this.bmi;
  }
};

const john = {
  fullName: 'John Smith',
  mass: 92,
  height: 1.95,
  calcBMI: function () {
    this.bmi = this.mass / this.height ** 2;
    return this.bmi;
  }
};

mark.calcBMI();
john.calcBMI();

console.log(mark.bmi, john.bmi);

// "John Smith's BMI (28.3) is higher than Mark Miller's (23.9)!"

if (mark.bmi > john.bmi) {
  console.log(`${mark.fullName}'s BMI (${mark.bmi}) is higher than ${john.fullName}'s BMI (${john.bmi})`)
} else if (john.bmi > mark.bmi) {
  console.log(`${john.fullName}'s BMI (${john.bmi}) is higher than ${mark.fullName}'s BMI (${mark.bmi})`)
}
```



## Iteration: The for Loop

```js
// console.log('Lifting weights repetition 1 🏋️‍♀️');
// console.log('Lifting weights repetition 2 🏋️‍♀️');
// console.log('Lifting weights repetition 3 🏋️‍♀️');
// console.log('Lifting weights repetition 4 🏋️‍♀️');
// console.log('Lifting weights repetition 5 🏋️‍♀️');
// console.log('Lifting weights repetition 6 🏋️‍♀️');
// console.log('Lifting weights repetition 7 🏋️‍♀️');
// console.log('Lifting weights repetition 8 🏋️‍♀️');
// console.log('Lifting weights repetition 9 🏋️‍♀️');
// console.log('Lifting weights repetition 10 🏋️‍♀️');

// for loop keeps running while condition is TRUE
for (let rep = 1; rep <= 30; rep++) {
  console.log(`Lifting weights repetition ${rep} 🏋️‍♀️`);
}
```


## Looping Arrays, Breaking and Continuing

```js
const jonas = [
  'Jonas',
  'Schmedtmann',
  2037 - 1991,
  'teacher',
  ['Michael', 'Peter', 'Steven'],
  true
];
const types = [];

// console.log(jonas[0])
// console.log(jonas[1])
// ...
// console.log(jonas[4])
// jonas[5] does NOT exist

for (let i = 0; i < jonas.length; i++) {
  // Reading from jonas array
  console.log(jonas[i], typeof jonas[i]);

  // Filling types array
  // types[i] = typeof jonas[i];
  types.push(typeof jonas[i]);
}

console.log(types);

const years = [1991, 2007, 1969, 2020];
const ages = [];

for (let i = 0; i < years.length; i++) {
  ages.push(2037 - years[i]);
}
console.log(ages);

// continue and break
console.log('--- ONLY STRINGS ---')
for (let i = 0; i < jonas.length; i++) {
  if (typeof jonas[i] !== 'string') continue;

  console.log(jonas[i], typeof jonas[i]);
}

console.log('--- BREAK WITH NUMBER ---')
for (let i = 0; i < jonas.length; i++) {
  if (typeof jonas[i] === 'number') break;

  console.log(jonas[i], typeof jonas[i]);
}
```

## Looping Backwards and Loops in Loops

```js
const jonas = [
  'Jonas',
  'Schmedtmann',
  2037 - 1991,
  'teacher',
  ['Michael', 'Peter', 'Steven'],
  true
];

// 0, 1, ..., 4
// 4, 3, ..., 0

for (let i = jonas.length - 1; i >= 0; i--) {
  console.log(i, jonas[i]);
}

for (let exercise = 1; exercise < 4; exercise++) {
  console.log(`-------- Starting exercise ${exercise}`);

  for (let rep = 1; rep < 6; rep++) {
    console.log(`Exercise ${exercise}: Lifting weight repetition ${rep} 🏋️‍♀️`);
  }
}
```

## The while Loop

```js
  for (let rep = 1; rep <= 10; rep++) {
  console.log(`Lifting weights repetition ${rep} 🏋️‍♀️`);
}

let rep = 1;
while (rep <= 10) {
  // console.log(`WHILE: Lifting weights repetition ${rep} 🏋️‍♀️`);
  rep++;
}

let dice = Math.trunc(Math.random() * 6) + 1;

while (dice !== 6) {
  console.log(`You rolled a ${dice}`);
  dice = Math.trunc(Math.random() * 6) + 1;
  if (dice === 6) console.log('Loop is about to end...');
}
```


## Coding Challenge ##4

Let's improve Steven's tip calculator even more, this time using loops!
- Create an array 'bills' containing all 10 test bill values
- Create empty arrays for the tips and the totals ('tips' and 'totals')
- Use the 'calcTip' function we wrote before (no need to repeat) to calculate tips and total values (bill + tip) for every bill value in the bills array. Use a for loop to perform the 10 calculations!

TEST DATA: 22, 295, 176, 440, 37, 105, 10, 1100, 86 and 52.

HINT: Call calcTip in the loop and use the push method to add values to the tips and totals arrays 😉

**BONUS:** Write a function 'calcAverage' which takes an array called 'arr' as an argument. This function calculates the average of all numbers in the given array. This is a DIFFICULT challenge (we haven't done this before)! Here is how to solve it: 4.1. First, you will need to add up all values in the array. To do the addition, start by creating a variable 'sum' that starts at 0. Then loop over the array using a for loop. In each iteration, add the current value to the 'sum' variable. This way, by the end of the loop, you have all values added together 4.2. To calculate the average, divide the sum you calculated before by the length of the array (because that's the number of elements) 4.3. Call the function with the 'totals' array

```js
const calcTip = function (bill) {
  return bill >= 50 && bill <= 300 ? bill * 0.15 : bill * 0.2;
}
const bills = [22, 295, 176, 440, 37, 105, 10, 1100, 86, 52];
const tips = [];
const totals = [];

for (let i = 0; i < bills.length; i++) {
  const tip = calcTip(bills[i]);
  tips.push(tip);
  totals.push(tip + bills[i]);
}
console.log(bills, tips, totals);

const calcAverage = function (arr) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) {
    // sum = sum + arr[i];
    sum += arr[i];
  }
  return sum / arr.length;
}
console.log(calcAverage([2, 3, 7]));
console.log(calcAverage(totals));
console.log(calcAverage(tips));
```

[BACK ⬅️](https://github.com/subhadeeppaul/JavaScript-Notes)

