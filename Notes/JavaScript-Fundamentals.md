# JavaScript Fundamentals Part 1

## Hello World

```js
console.log("Hello World");
```

## A brief introduction to Javascript
*JavaScript* was initially created to “make web pages alive”.

The programs in this language are called scripts. They can be written right in a web page’s HTML and run automatically as the page loads.

Scripts are provided and executed as plain text. They don’t need special preparation or compilation to run.


## Linking a JavaScript File

```html
<body>
  <script>
    console.log("Hello World");
  </script>
  Hello Everyone
</body>
```
**Best Practice:** The best practice is to put JavaScript <script> tags just before the closing </body> tag rather than in the <head> section of your HTML. The reason for this is that HTML loads from top to bottom. The head loads first, then the body, and then everything inside the body.

## Values and Variables

```js
console.log("Subhadeep");
console.log(23);

let firstName = "Paul";
console.log(firstName);
console.log(firstName);
console.log(firstName);
```

## Variable name conventions

```js
let jonas_matilda = "JM";
let $function = 27;

let person = "jonas";
let PI = 3.1415;

let myFirstJob = "Coder";
let myCurrentJob = "Teacher";

let job1 = "programmer";
let job2 = "teacher";

console.log(myFirstJob);
```


## Data Types
Data types specify what kind of data can be stored and manipulated within a program.

In *JavaScript*, we have the following data types available.
*Primitive Data Types* and 
*Non-Primitive Data Types*

*Note:* We can use the JavaScript **typeof** operator to find the type of a JavaScript variable.
It returns the type of a variable or an expression.

**Primitive DataTypes:** Primitive data types are immutable meaning not able to be changed.

- Number
- String
- Boolean
- Undefined
- Null
these are the primitive types in JavaScript.

- *Numbers:* 10, -3, 2.6, 3.484, 100, 1000 etc.

```js
console.log(49);
console.log(1.33);
console.log(-5);
console.log(0);
console.log(-0);

console.log(typeof 2.47);

```

- *Strings:* "Hello"

```js
console.log("This is a String");
console.log('This is a String');
console.log(`This is a String`);

console.log(typeof "Hello");
```

- *Boolean:* True or False
```js
console.log(true);
console.log(false);

console.log(typeof true);
```
- *Undefined:* Something not defiend yet but may be defiend later.

When a variable is first declared in JS, it is 'undefined' and it's type is also 'undefined'.
So basically 'undefined' is BOTH the value as well as the type of the value!!
```js
var age;
console.log(age);
console.log(typeof age);

var salary = Undefined;
console.log(salary);
```

- *Null:* Represent empty value.

Note the following though. 'null' is again both a type as well as a value, just like 'undefined'.
So typeof undefined returns undefined, but typeof null returns object.
So the following makes no sense. This is normally considered as a bug in JS (?)

```js
var company = null;
console.log(company);

console.log(typeof undefined);
console.log(typeof null); 
```

**Non-Primitive:** Types which are a composition of other types.
                    e.g. Object

- *Objects:* If we have to somehow store Key-Value pairs, then we can use objects.
```js 
<key,value>

var user = {
    name : "Paul";
    company : "XYZ";
    age : 24;
}
console.log(user);


Note: Key will be unique
```
**let-const-var :**
There are 3 different ways of defining variables in JS - let, const, var.

We will be coming back to these later in the course.

**let** can be used when you want to 'mutate' a variable, i.e. assign it a value only to reassign it later

```js
let firstName = "Jane";
firstName = "Jack";
```
**const** is used when the value assigned to that variable cannot be reassigned - immutable

```js
const yearOfBirth = 2020;
```
```
yearOfBirth = 2021; //Error: Attempt to assign to const or readonly variable.
```


For the same reason, creating a const variable without assigning a value to it is invalid.
```js
const yearOfDeath; //const variable without initializer is not allowed
```

We don't even need to define variables at all, we can directly write the name of the variable and be done with it.

But this is a very bad idea, because in that case JS will create a property on the global object (?)

```js
middleName = "Vesuvius";
```








## Basic Operator
**`Math Operator`**
```js
const now = 2037;
const agePaul = now - 1991;
const ageSarah = now - 2018;

console.log(agePaul, ageSarah);
console.log(agePaul * 2, agePaul 10, 2 ** 3);

// 2 ** 3 means 2 to the power of 3 = 2 * 2 * 2

const firstName = 'Subhadeep';
const lastName = 'Paul';

console.log(firstName + ' ' + lastName);

```
**`Assignment operators`**

```js
let x = 10 + 5; // output: 15

x += 10; // x = x + 10 - Output: 25

x *= 4; // x = x * 4 - Output: 100

x++; // x = x + 1
x--; // x = x - 1
x--;

console.log(x);
```

**`Comparison operators`**
```js
console.log(agePaul > ageSarah); //  >, <, >=, <=
console.log(ageSarah >= 18);  // Output: true

const isFullAge = ageSarah >= 18;

console.log(now - 1991 > now - 2018);
```
## Operator Precedence 
```js
const now = 2037;
const agePaul = now - 1991;
const ageSarah = now - 2018;

console.log(now - 1991 > now - 2018);

let x, y;

x = y = 25 - 10 - 5; // Output: x = y = 10, x = 10 - Assignment works from right to left

console.log(x, y);

const averageAge = (agePaul + ageSarah) 2;

console.log(agePaul, ageSarah, averageAge);
```

## Coding Challenge 1

Mark and John are trying to compare their BMI (Body Mass Index), which is calculated using the formula: BMI = mass / height ** 2 = mass / (height * height). (mass in kg and height in meter).
    
    1. Store Mark's and John's mass and height in variables
    2. Calculate both their BMIs using the formula (you can even implement both versions)
    3. Create a boolean variable 'markHigherBMI' containing information about whether Mark has a higher BMI than John.

 
TEST DATA 1: Marks weights 78 kg and is 1.69 m tall. John 
weights 92 kg and is 1.95 m tall.

TEST DATA 2: Marks weights 95 kg and is 1.88 m tall. John weights 85 kg and is 1.76 m tall.

*Solution*

```js
const massMark = 95;
const heightMark = 1.88;

const massJohn = 85;
const heightJohn = 1.76;

const BMIMark = massMark / heightMark ** 2;
const BMIJohn = massJohn / (heightJohn * heightJohn);

const markHigherBMI = BMIMark > BMIJohn;
console.log(BMIMark, BMIJohn, markHigherBMI);
```

## String and Template Literals

 ```js
 let currYear = 2020;
let introYear = 1995;

let message1 = "Javascript is " + (currYear - introYear) + " years old!";
console.log(message1);

// Alternatively you could use Template Literals. Note how currYear and introYear are being used

let message2 = `Javascript is ${currYear - introYear} years old! The current year is ${currYear}.`;
console.log(message2);

// You can also use template strings to write multi-line strings
console.log(`This is a
    multiline string
    in JavaScript`);
```


## Taking Decisions: if else Statements

```js
const age = 15;
if (age >= 18) {
  console.log('Sarah can start driving license 🚗');
} else {
  const yearsLeft = 18 - age;
  console.log(`Sarah is too young. Wait another ${yearsLeft} years :)`);
}

const birthYear = 2012;

let century;
if (birthYear <= 2000) {
  century = 20;
} else {
  century = 21;
}
console.log(century);
```

## Coding Challenge ##2

Use the BMI example from Challenge #1, and the code you already wrote, and improve it:

    1. Print a nice output to the console, saying who has the higher BMI. The message can be either "Mark's BMI is higher than John's!" or "John's BMI is higher than Mark's!"
    2. Use a template literal to include the BMI values in the outputs. Example: "Mark's BMI (28.3) is higher than John's (23.9)!"

#### Solution

```js
const massMark = 78;
const heightMark = 1.69;

const massJohn = 92;
const heightJohn = 1.95;


const massMark = 95;
const heightMark = 1.88;

const massJohn = 85;
const heightJohn = 1.76;

const BMIMark = massMark heightMark ** 2;
const BMIJohn = massJohn (heightJohn * heightJohn);

console.log(BMIMark, BMIJohn);

if (BMIMark > BMIJohn) {
  console.log(`Mark's BMI (${BMIMark}) is higher than John's (${BMIJohn})!`)
} else {
  console.log(`John's BMI (${BMIJohn}) is higher than Marks's (${BMIMark})!`)
}
```


## Type Conversion and Type Coercion

**Type Conversion or Explicit Conversion:**
The conversion takes place manually or explicitly by typing the method or function
  name before converting the values, it is known as Explicit Conversion.

```js
// This won't work obviously

let currentYear = "2020";
console.log("In 10 years, it will be " + currentYear + 10); // Prints: In 10 years, it will be 202010
console.log(currentYear + 10); // Prints: 202010

// Hence we have to do this instead
console.log("In 10 years, it will be " + Number(currentYear) + 10); // Prints: In 10 years, it will be 202010
console.log(Number(currentYear) + 10); // Prints:2030

// What if we try to convert something to number that is not really a number
console.log(Number("PAUL25")); // Prints: NaN

// The 'NaN' is generated. JS gives us a NaN value when an operation involving numbers fails to generate a value that is a Number
// Strangely enough, the typeof NaN is a Number
console.log(typeof NaN); // Prints: number

// Similarly, we can convert Numbers to String
console.log(String(23), 23); // You can see that the two values are different because they will be differently colored in the console
```

**Type Coercion or Implicit Coercion:**
Type coercion is when JavaScript automatically converts types behind the scenes for us.
So basically, type coercion happens whenever an operator is dealing with two values that have different types.

```js
For eg. when the '+' operator is given a number and a string, it will convert the number to string

console.log("In 10 years, it will be " + currentYear + 10); // Prints: In 10 years, it will be 202010

console.log('23' - '10' - 3); // Prints: 10. Because in '-' operator case, JS converts the Strings to numbers

console.log('23' + '10' + 3); // Prints: 23103. Like we discussed, '+' converts numbers to string. Hence, concatenation happens

console.log('23' * '2'); // Prints: 46. '*' operator also converts Strings to Numbers

console.log('46' / '2'); // Prints: 23. '/' operator also converts Strings to Numbers

console.log('46' > '2'); // Prints: true. '>' operator also converts Strings to Numbers

// So the anomaly is the '+' operator that converts numbers to strings. All others, convert String to numbers.
console.log('23' + '10' - 3); // Prints: 2307. Like we discussed, '+' converts numbers to string. Hence, concatenation happens
console.log('23' - '10' + 3); // Prints: 16.
console.log('23' - '10' + '3'); // Prints: 133.
console.log(2 + 3 + 4 + '5'); // Prints: 95
```


## Truthy and Falsy Values
```js
// In JS, we have 5 'falsy' values: 0, '' (the empty string),undefined, null, NaN
// What this means is that any value that is not one of the above values is going to be converted into 'true' if we convert it into a Boolean type variable. Only the above 5 values will be converted to false on conversion to boolean values

console.log(Boolean(0)); // Prints: false
console.log(Boolean(undefined)); // Prints: false
console.log(Boolean('TEST')); // Prints: true
console.log(Boolean({})); // Input is an empty object. Prints: true

// The way that we use the truthiness of a variable is by using if-else statements.
// So for instance, I can write this:
let salary = 0;
if (salary) {
    console.log("Do not spend it on Pizza only");
} else {
    console.log("What will you do now?"); // This block is triggered because '0' is a falsy type value
}

// Another way to use this is if the variable is defined or null
let height;
if (height) {
    console.log("Height is defined");
} else {
    console.log("Height is undefined"); // This block is triggered. But note that this block will also be triggered if height is 0.
}
```
## Equality Operators: == vs. ===

```js
const age = '18';
if (age === 18) console.log('You just became an adult :D (strict)'); // output: true (strict equality doesn't perform type coercion)
if (age == 18) console.log('You just became an adult :D (loose)'); // Lose equality does the type coercion therefore output: true (the string '18' will be converted to number before checking) 

const favourite = Number(prompt("What's your favourite number?"));
console.log(favourite);
console.log(typeof favourite);

if (favourite === 23) { // 22 === 23 -> FALSE
  console.log('Cool! 23 is an amzaing number!')
} else if (favourite === 7) {
  console.log('7 is also a cool number')
} else if (favourite === 9) {
  console.log('9 is also a cool number')
} else {
  console.log('Number is not 23 or 7 or 9')
}

if (favourite !== 23) console.log('Why not 23?');
```
So as a general rule for clean code, avoid the loose equality operator as much as you can. So when comparing values, always use strict equality with the three equal signs.

## Logical Operators

```js
const hasDriversLicense = true; // A
const hasGoodVision = true; // B

console.log(hasDriversLicense && hasGoodVision); // output: true
console.log(hasDriversLicense || hasGoodVision); // output: true
console.log(!hasDriversLicense); // output: false

// if (hasDriversLicense && hasGoodVision) {
//   console.log('Sarah is able to drive!');
// } else {
//   console.log('Someone else should drive...');
// }

const isTired = false; // C
console.log(hasDriversLicense && hasGoodVision && isTired); output: false

if (hasDriversLicense && hasGoodVision && !isTired) {
  console.log('Sarah is able to drive!'); 
} else {
  console.log('Someone else should drive...');
}
// output: Sarah is able to drive! 
```
The NOT operator actually has proceedings over the OR and AND operators.


## Coding Challenge ##3

There are two gymnastics teams, Dolphins and Koalas. They compete against each other 3 times. The winner with the highest average score wins the a trophy!

    1. Calculate the average score for each team, using the test data below
    2. Compare the team's average scores to determine the winner of the competition, and print it to the console. Don't forget that there can be a draw, so test for that as well (draw means they have the same average score).
    3. BONUS 1: Include a requirement for a minimum score of 100. With this rule, a team only wins if it has a higher score than the other team, and the same time a score of at least 100 points. HINT: Use a logical operator to test for minimum score, as well as multiple else-if blocks 😉
    4. BONUS 2: Minimum score also applies to a draw! So a draw only happens when both teams have the same score and both have a score greater or equal 100 points. Otherwise, no team wins the trophy.

TEST DATA: Dolphins score 96, 108 and 89. Koalas score 88, 91 and 110 TEST DATA BONUS 1: Dolphins score 97, 112 and 101. Koalas score 109, 95 and 123 TEST DATA BONUS 2: Dolphins score 97, 112 and 101. Koalas score 109, 95 and 106


**Solution**

```js
const scoreDolphins = (96 + 108 + 89) / 3;
const scoreKoalas = (88 + 91 + 110) / 3;

console.log(scoreDolphins, scoreKoalas);

if (scoreDolphins > scoreKoalas) {
  console.log('Dolphins win the trophy 🏆');
} else if (scoreKoalas > scoreDolphins) {
  console.log('Koalas win the trophy 🏆');
} else if (scoreDolphins === scoreKoalas) {
  console.log('Both win the trophy!');
}
```

**Bonus 1**
```js
const scoreDolphins = (97 + 112 + 80) 3;
const scoreKoalas = (109 + 95 + 50) 3;

console.log(scoreDolphins, scoreKoalas);

if (scoreDolphins > scoreKoalas && scoreDolphins >= 100) {
  console.log('Dolphins win the trophy 🏆');
} else if (scoreKoalas > scoreDolphins && scoreKoalas >= 100) {
  console.log('Koalas win the trophy 🏆');
} else if (scoreDolphins === scoreKoalas && scoreDolphins >= 100 && scoreKoalas >= 100) {
console.log('Both win the trophy!');
} else {
console.log('No one wins the trophy 😭');
}
```
## The switch Statement

```js
const day = 'friday';

switch (day) {
  case 'monday': // day === 'monday'
    console.log('Plan course structure');
    console.log('Go to coding meetup');
    break;
  case 'tuesday':
    console.log('Prepare theory videos');
    break;
  case 'wednesday':
  case 'thursday':
    console.log('Write code examples');
    break;
  case 'friday':
    console.log('Record videos');
    break;
  case 'saturday':
  case 'sunday':
    console.log('Enjoy the weekend :D');
    break;
  default:
    console.log('Not a valid day!');
}

if (day === 'monday') {
  console.log('Plan course structure');
  console.log('Go to coding meetup');
} else if (day === 'tuesday') {
  console.log('Prepare theory videos');
} else if (day === 'wednesday' || day === 'thursday') {
  console.log('Write code examples');
} else if (day === 'friday') {
  console.log('Record videos');
} else if (day === 'saturday' || day === 'sunday') {
  console.log('Enjoy the weekend :D');
} else {
  console.log('Not a valid day!');
}
```


## Statements and Expressions

```js
3 + 4 // output: 7 - an expression
1991
true && false && !false

// Following is a Statement
if (50 > 10) {
  const str = '50 is bigger';
}

const me = 'Paul';
console.log(`I'm ${2050 - 1997} years old ${me}`); // In javascript literals we can use expressions but not statements.
```
- an expression is a piece of code that produces a value.
- statements are like full sentences that translate our actions.


## The Conditional (Ternary) Operator

```js
const age = 23;
// age >= 18 ? console.log('I like to drink wine 🍷') : console.log('I like to drink water 💧');

const drink = age >= 18 ? 'Sharbat-e-Jaam 🍷' : 'water 💧';
console.log(drink);

let drink2;
if (age >= 18) {
  drink2 = 'Sharbat-e-Jaam 🍷';
} else {
  drink2 = 'water 💧';
}
console.log(drink2);

console.log(`I like to drink ${age >= 18 ? 'Sharbat-e-Jaam 🍷' : 'water 💧'}`);
```
## Coding Challenge ##4

Steven wants to build a very simple tip calculator for whenever he goes eating in a restaurant. In his country, it's usual to tip 15% if the bill value is between 50 and 300. If the value is different, the tip is 20%.

     1. Your task is to calculate the tip, depending on the bill value. Create a variable called 'tip' for this. It's not allowed to use an if else statement 😅 (If it's easier for you, you can start with an if else statement, and then try to convert it to a ternary operator!)
     2.Print a string to the console containing the bill value, the tip, and the final value (bill + tip). Example: 'The bill was 275, the tip was 41.25, and the total value 316.25'

TEST DATA: Test for bill values 275, 40 and 430

HINT: To calculate 20% of a value, simply multiply it by 20/100 = 0.2 HINT: Value X is between 50 and 300, if it's >= 50 && <= 300 😉

```js
const bill = 275;
const tip = (bill >= 50 && bill <= 300) ? 0.15 * bill : 0.20 * bill;

const totalValue = bill + tip;

console.log(`The bill was ${bill}, the tip was ${tip}, and the total value ${bill + tip}`);
```


[BACK ⬅️](https://github.com/subhadeeppaul/JavaScript-Notes)
