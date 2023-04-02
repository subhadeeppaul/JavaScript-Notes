
# Data Structures, Modern Operators and Strings

### Destructuring Arrays
- Destructuring is a way of unpacking data from an array or an object into separate variables.
```js
'use strict';

const restaurant = {
  name: 'Classico Italiano',
  location: 'Via Angelo Tavanti 23, Firenze, Italy',
  categories: ['Italian', 'Pizzeria', 'Vegetarian', 'Organic'],
  starterMenu: ['Focaccia', 'Bruschetta', 'Garlic Bread', 'Caprese Salad'],
  mainMenu: ['Pizza', 'Pasta', 'Risotto'],

  // This function is an example of returning two or more than two items from a single function
  order: function (starterIdx, mainIdx) {
    return [this.starterMenu[starterIdx], this.mainMenu[mainIdx]];
  }
};

// Normally you would do something like this:
const myArray = [1,2,3];
const a = myArray[0];
const b = myArray[1];
const c = myArray[2];

// But starting from ES6, you can do this in single line like:
// This means you are declaring 3 variables of type const named 'x', 'y', 'z'.
// This means you cannot later reassign x, y, or z to different values.
const [x, y, z] = myArray;
console.log(a, b, c); // Prints: 1 2 3

// Destructuring does not in any way affect the original array.
console.log(myArray); // Still Prints: [1, 2, 3]

// It is not necessary to extract the entire array into variables. Only a part of the array can be destructured.
const [first, second] = restaurant.categories;
console.log(first, second); // Prints: Italian Pizzeria

// So what if we wanted the first and the third elements instead? We just leave a space for the second element.
let [ctgry1, , ctgry3] = restaurant.categories;
console.log(ctgry1, ctgry3); // Prints: Italian Vegetarian

// Suppose you wanted to swap the values of two variables.
// For eg. in the above, you wanted to swap the 'ctgry1' and 'ctgry3' you would do something like this:
let temp = ctgry1;
ctgry1 = ctgry3;
ctgry3 = temp;
console.log(ctgry1, ctgry3); // Prints: Vegetarian Italian

// But now you can do just this:
// So what we are doing here is basically
// First we are creating a new array by using the [] operator containing the two elements ctgry1 and ctgry3
// Then we are destructuring the array and storing the two elements into the swapped variables. Make sense?
// We are not using let or const here because we are simple reassigning the values associated with the two variables.
[ctgry3, ctgry1] = [ctgry1, ctgry3];
console.log(ctgry1, ctgry3); // Prints: Italian Vegetarian

// We can have a function return an array and then destructure that array
// thus, in effect, having a function that returns multiple values
let [starterItem, mainCourseItem] = restaurant.order(1, 2);
console.log(starterItem, mainCourseItem); // Prints: Bruschetta Risotto

// We can also destructure nested arrays
const nestedArray = [1, 2, [3, 4]];
let [val1, , val3] = nestedArray;
console.log(val1, val3); // Prints: 1, [3,4]
// So if we want to s=destructure the array, we then do:
let [val0, , [nestedVal0, nestedVal1]] = nestedArray;
console.log(val0, nestedVal0, nestedVal1); // Prints: 1,3,4

// We can also set default values for the destructured array
let [p,q,r] = [2,3];
console.log(p,q,r); // Prints: 2 3 undefined
// But now we assign default values for each variable
[p=1,q=1,r=1] = [2,3];
console.log(p,q,r); // Prints: 2 3 1
```

### Destructuring Objects
- Similar to destructuring arrays, we can also destructure objects.

```js
'use strict';

const restaurant = {
  name: 'Classico Italiano',
  location: 'Via Angelo Tavanti 23, Firenze, Italy',
  categories: ['Italian', 'Pizzeria', 'Vegetarian', 'Organic'],
  starterMenu: ['Focaccia', 'Bruschetta', 'Garlic Bread', 'Caprese Salad'],
  mainMenu: ['Pizza', 'Pasta', 'Risotto'],

  // This function is an example of returning two or more than two items from a single function
  order: function (starterIdx, mainIdx) {
    return [this.starterMenu[starterIdx], this.mainMenu[mainIdx]];
  },

  openingHours: {
    thu: {
      open: 12,
      close: 22,
    },
    fri: {
      open: 11,
      close: 23,
    },
    sat: {
      open: 0, // Open 24 hours
      close: 24,
    },
  },
};


// The variables names should exactly match the property names that we want to retrieve from the object
// Unlike destructuring in arrays, we do not need to specify all the properties
// and the properties can also be specified out-of-order.
// Just like arrays, this now creates 3 new variables
const {name, openingHours, categories} = restaurant;
console.log(name, openingHours, categories); // Prints the values from the restaurant object

// We can also change the variable names to be different from the property names
const {name: restaurantName, openingHours: workingHours, categories: tags} = restaurant;
console.log(restaurantName, workingHours, tags);

// Using Default Values

// We can also have default values in case the property that we are trying to read does not exist on an object
// The point we are trying to make here is that:
// If a property does not exist on an object, then we would get 'undefined' as is the case when defining a variable named 'menu'
// However, if a property is not defined, and we have assigned a default value to it, the variable will take the default value instead
// as is the case with the variable 'originalMenu'
// 'starterMenu' is a valid field on the object, and we are changing it's variable name to 'starters'. Hence the default value will not be taken.
const {menu, originalMenu = [], starterMenu: starters = []} = restaurant;
console.log(menu, originalMenu, starters); // Prints: undefined, [], ['Focaccia', 'Bruschetta', 'Garlic Bread', 'Caprese Salad']

// Mutating Variables

// Consider the following example
let amt1 = 100;
let amt2 = 200;
const myObject = {amt1: 1, amt2: 2};

// Now if we try to mutate the variables amt1 and amt2, we will get an error
// {amt1, amt2} = myObject;
// Hence, instead, we have to do this:
({amt1, amt2} = myObject);
console.log(amt1, amt2); // Prints: 1 2

// Dealing with Nested Objects

// Consider the following object
const {fri} = workingHours;
console.log(fri); // Prints: {open: 11, close: 23}
// Now what is we wanted to destructure the object in one line. We will make use of nested objects.
const {fri: {open, close}} = workingHours;
console.log(open, close); // Prints: 11 23

// An application of destructuring objects is when passing in parameters to functions.
// In JS, you can have many parameters being passed into a function, which can make it prone to errors if you miss a parameter
// or change the order of teh parameters or something.
// What you can do instead is box the parameters into an object, that way you can use only the parameters that you need
// and also not mess up the code in case the order changes

// Consider this function
const printPersonDetails = function (name, dob, birthPlace, job, hobbies) {
  console.log(`Hi ${name}, as per our details you are born in ${birthPlace} and have a job as a ${job}.`);
}

// Instead you could pass in an object
const printPersonDetailsUsingObj = function (person) {
  console.log(`Hi ${person.name}, as per our details you are born in ${person.birthPlace} and have a job as a ${person.job}.`);
}

// And then you can destructure the object right in the function call itself
const printPersonDetailsUsingDestrObj = function ({name, dob, birthPlace, job, hobbies}) {
  console.log(`Hi ${name}, as per our details you are born in ${birthPlace} and have a job as a ${job}.`);
}

// We can also specify default values in case the properties are not present in the object being passed in
const printPersonDetailsUsingDestrObjAndDefaults = function ({name, dob = '1/1/2020', birthPlace, job, hobbies}) {
  console.log(`Hi ${name}, as per our details you are born in ${birthPlace} and have a job as a ${job}.`);
}
const alice = {
  name: 'Alice',
  dob: '1/1/1990',
  birthPlace: 'New York',
  job: 'Teacher',
  hobbies: ['rock climbing', 'pottery']
}

printPersonDetailsUsingObj(alice);
printPersonDetailsUsingDestrObj(alice);
```
## The Spread Operator (...)
- We can use the spread operator to unpack an entire array or objects at once.
```js
///////////////////////////////////////
// The Spread Operator (...)

// Suppose we have an existing array, and using that we want to create a new array
const myArray1 = [5,6,7,8];
// The new array is supposed to contain all the numbers from 1 to 8
// We can do this. Also, take note that myArray2 is a new array.(Signified by the use of [] operator to create a new array)
const myArray2 = [1,2,3,4, ...myArray1];
console.log(myArray2); // Prints: [1, 2, 3, 4, 5, 6, 7, 8]
// Note that doing:
const myArray3 = [1,2,3,4,myArray1];
// would have given us nested array. That is not what we want.
console.log(myArray2); // Prints: [1, 2, 3, 4, [5, 6, 7, 8]]

// A second use of the spread operator is to pass multiple arguments to a function.
// For example, in console.log, we can pass in the individual elements of the array
console.log(...myArray2); // Prints: 1 2 3 4 5 6 7 8

// Two use cases of the spread operator are:
// 1) Create shallow copies of arrays
// 2) Merge two or more arrays

// 1) Create shallow copies of arrays
const myArrayCopy = [...myArray2];
console.log(myArrayCopy); // Prints: [1, 2, 3, 4, 5, 6, 7, 8]

// 2) Merge two or more arrays
const myArray4 = [9, 10];
const mergedArray = [...myArray2, ...myArray4];
console.log(mergedArray); // Prints: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// Note that the spread operator does not only work on arrays, instead it works on all iterables.
// Iterables are: arrays, strings, maps, sets. But NOT Objects.

// Since strings are also iterables, we can also use the spread operator with strings
const firstName = 'Alice';
const charsOfName = [...firstName];
console.log(charsOfName); // Prints: ["A", "l", "i", "c", "e"]

// We can also use the spread operator in order to pass multiple args to a function
const cookFood = function (ing1, ing2, ing3) {
  console.log(`Your meal containing ${ing1}, ${ing2}, and ${ing3} is ready`);
}

const ingredients = ['Potatoes', 'Onions', 'Bread'];
// And now, instead of passing in each of the ingredients like ingredients[0], ingredients[1], ingredients[2], we do this:
cookFood(...ingredients); // Prints: Your meal containing Potatoes, Onions, and Bread is ready

// But now, you can also use the spread operator to perform shallow copy of objects
const bob = {
  name: 'Bob',
  dob: '1/1/1990',
  birthPlace: 'New York',
  job: 'Teacher',
  hobbies: ['rock climbing', 'pottery']
};

// Adding properties to objects using the spread operator
const bobAdd = {
  favFood: 'Ramen',
  ...bob,
  favDrink: 'Kombucha'
};
console.log(bobAdd); // Prints: {favFood: "Ramen", name: "Bob", dob: "1/1/1990", birthPlace: "New York", job: "Teacher, ...}

// Shallow copy of objects
const bobClone = {...bobAdd};
console.log(bobClone); // Prints: {favFood: "Ramen", name: "Bob", dob: "1/1/1990", birthPlace: "New York", job: "Teacher, ...}
```
- Spread operator takes all the elements from the array and it also doesn't create new variables. And as a consequence, we can only use it in places where we would otherwise write values separated by commas.
- two important use cases of the spread operator are which is to create shallow copies of arrays, and to merge two arrays together.
- So basically, most of the built-in data structures in JavaScript are now iterables, but except objects.

## Rest Pattern and Parameters
- The Rest pattern is, in a way, the 'opposite' of the spread operator. It uses the same operator, but to condense multiple values into an array.

```js
// Just like the Spread operator, the Rest pattern also have two distinct uses.

// 1) Uses it as destructuring

// We have seen the use of the spread operator on the RHS of the = operator
const anotherArray1 = [1,2,...[3,4,5]];
// Now suppose if we wanted to save the first and second elements of the array in variables of their own,
// but for the remaining values, we wanted to group them into one single array.
// This is how we would do it.
// This is the REST syntax, because it is on the left side of the = operator
const [v1, v2, ...arr1] = anotherArray1;
console.log(v1, v2, arr1); // Prints: 1 2 [3,4,5]

// Similarly we can also use the spread operator with objects
const charlie = {
  name: 'Charlie',
  dob: '1/1/1990',
  birthPlace: 'New York',
  job: 'Teacher',
  hobbies: ['rock climbing', 'pottery']
};
// Suppose we wanted to extract the 'hobbies' and store it into a separate variable
const { hobbies, ...otherDetailsAboutCharlie} = charlie;
console.log(hobbies); // Prints: ["rock climbing", "pottery"]
// Note that otherDetailsAboutCharlie no longer contains the hobbies
console.log(otherDetailsAboutCharlie); // Prints: {name: "Charlie", dob: "1/1/1990", birthPlace: "New York", job: "Teacher"}

// 2) Use it with Function arguments

// The Rest operator in this case collects all of the multiple inputs and passes it in as an array.
// So, in effect, this function can accept any number of parameters
const addMultipleNumbers = function (...numbers) {
  console.log(`Args is: ${numbers} of type ${typeof numbers}`);
  let sum = 0;
  for (let i = 0; i< numbers.length; i++) {
    sum += numbers[i];
  }
  console.log(`The final sum is ${sum}`);
}

// Calling the addMultipleNumbers functions with multiple args
addMultipleNumbers(1,2);
addMultipleNumbers(1,2,3,4,);
addMultipleNumbers(1,2,3,4,5);

// Calling the addMultipleNumbers functions with arrays.
// Note how we have an array give, we are destructuring it by using the spread operator, then passing it into the fn
// where the function is then collecting it as a single array and then summing it over.
const arraysAsArgs = [1,2,3,4,5,6];
addMultipleNumbers(...arraysAsArgs);
// This does not work if you do just this.
// I think what happens is that since in the function definition you are using the ... operator
// and you are passing in an array as an args, it is expecting an array of arrays as an input?
addMultipleNumbers(arraysAsArgs);

// Another example using the Rest parameters

// Consider the following function:
const orderFood = function (mainIngredient, ...otherIngredients) {
  console.log(mainIngredient); // Prints: flour
  console.log(otherIngredients); // Prints: ["oil", "butter"]
}

let ingred1 = 'flour';
let ingred2 = 'oil';
let ingred3 = 'butter';
orderFood(ingred1, ingred2, ingred3);
```
- So the spread operator is used where we would otherwise write values, separated by a comma. On the other hand the rest is pattern is basically used where we would otherwise write variable names separated by commas.

## Short Circuiting (&& and Il)
- The `&&` and `||` operators work very differently in JS when compared to Java.
- Boolean operators can use any datatype as its operands, they can return any datatype, and they do short-circuiting.
- The OR operator `(||)` will return the first 'truthy' value among all of its operands or the last value if all of them are 'falsy'.
- The AND operator `(&&)` will return the first 'falsy' value among all of it's operands or return the last value if all of them are 'truthy'.
- We can use the `OR` operator to set default values.
- We can use the `AND` operator to execute code in the second operand if the first operand is true.

```js
///////////////////////////////////////
// Short Circuiting (&& and ||)

console.log('---- OR ----');
// Use ANY data type, return ANY data type, short-circuiting
console.log(3 || 'Jonas'); // output: 3
console.log('' || 'Jonas'); // output: Jonas
console.log(true || 0); // output: true
console.log(undefined || null); // output: null

console.log(undefined || 0 || '' || 'Hello' || 23 || null); // output: Hello

restaurant.numGuests = 0;
const guests1 = restaurant.numGuests ? restaurant.numGuests : 10;
console.log(guests1); // output: 10

const guests2 = restaurant.numGuests || 10;
console.log(guests2); // output: 

console.log('---- AND ----'); 
console.log(0 && 'Jonas'); // output: false
console.log(7 && 'Jonas'); // output: true

	console.log('Hello' && 23 && null && 'jonas'); // output: null

// Practical example
if (restaurant.orderPizza) {
  restaurant.orderPizza('mushrooms', 'spinach');
}

// above if block can be written as
restaurant.orderPizza && restaurant.orderPizza('mushrooms', 'spinach');

```
- So the OR operator will return the first truthy. value of all the operands, or simply the last value if all of them are falsy.
- On the other hand, the AND operator will return the first falsy value or the last value if all of them are truthy.
- And as for practical applications, we can use the OR operator to set default values, and we can use the AND operator to execute code in the second operand if the first one IS true.

## The Nullish Coalescing Operator (??)

```js
// The Nullish Coalescing Operator
restaurant.numGuests = 0;
const guests = restaurant.numGuests || 10;
console.log(guests);

// Nullish: null and undefined (NOT 0 or '')
const guestCorrect = restaurant.numGuests ?? 10;
console.log(guestCorrect);
```
- The problem was that we wanted 'number of guests' to be zero but because of how OR operator || works the result will be 10 instead of 0.
- In order to solve the problem ES20 introduced 'The Nullish Coalescing Operator (??)'

## Logical Assignment Operators

```js
///////////////////////////////////////
// Logical Assignment Operators
const rest1 = {
  name: 'Capri',
  // numGuests: 20,
  numGuests: 0,
};

const rest2 = {
  name: 'La Piazza',
  owner: 'Giovanni Rossi',
};

// OR assignment operator
// rest1.numGuests = rest1.numGuests || 10;
// rest2.numGuests = rest2.numGuests || 10;
// rest1.numGuests ||= 10;
// rest2.numGuests ||= 10;

// nullish assignment operator (null or undefined)
rest1.numGuests ??= 10;
rest2.numGuests ??= 10;

// AND assignment operator
// rest1.owner = rest1.owner && '<ANONYMOUS>';
// rest2.owner = rest2.owner && '<ANONYMOUS>';
rest1.owner &&= '<ANONYMOUS>';
rest2.owner &&= '<ANONYMOUS>';

console.log(rest1);
console.log(rest2);
```
- Introduced in ES2021
- And so basically, what the logical and assignment operator does is to assign a value to a variable if it is currently truthy.

## Coding Challenge ##1
We're building a football betting app (soccer for my American friends 😅)!

Suppose we get data from a web service about a certain game (below). In this challenge we're gonna work with the data. So here are your tasks:

    1. Create one player array for each team (variables 'players1' and 'players2')
    2. The first player in any player array is the goalkeeper and the others are field players. For Bayern Munich (team 1) create one variable ('gk') with the goalkeeper's name, and one array ('fieldPlayers') with all the remaining 10 field players
    3. Create an array 'allPlayers' containing all players of both teams (22 players)
    4. During the game, Bayern Munich (team 1) used 3 substitute players. So create a new array ('players1Final') containing all the original team1 players plus 'Thiago', 'Coutinho' and 'Perisic'
    5. Based on the game.odds object, create one variable for each odd (called 'team1', 'draw' and 'team2')
    6. Write a function ('printGoals') that receives an arbitrary number of player names (NOT an array) and prints each of them to the console, along with the number of goals that were scored in total (number of player names passed in)
    7. The team with the lower odd is more likely to win. Print to the console which team is more likely to win, WITHOUT using an if/else statement or the ternary operator.

TEST DATA FOR 6: Use players 'Davies', 'Muller', 'Lewandowski' and 'Kimmich'. Then, call the function again with players from game.scored

```js
// 1.
const [players1, players2] = game.players;
console.log(players1, players2);

// 2.
const [gk, ...fieldPlayers] = players1;
console.log(gk, fieldPlayers);

// 3.
const allPlayers = [...players1, ...players2];
console.log(allPlayers);

// 4.
const players1Final = [...players1, 'Thiago', 'Coutinho', 'Periscic'];

// 5.
const {
  odds: { team1, x: draw, team2 },
} = game;
console.log(team1, draw, team2);

// 6.
const printGoals = function (...players) {
  console.log(players);
  console.log(`${players.length} goals were scored`);
};

// printGoals('Davies', 'Muller', 'Lewandowski', 'Kimmich');
// printGoals('Davies', 'Muller');
printGoals(...game.scored);

// 7.
team1 < team2 && console.log('Team 1 is more likely to win');
team1 > team2 && console.log('Team 2 is more likely to win');
```

## Looping Arrays: The for-of Loop
- This is how we can use the new for-of loop in JS.

```js
const eve = {
  name: 'Eve',
  dob: '1/1/1990',
  birthPlace: 'New York',
  job: 'Teacher',
  hobbies: ['rock climbing', 'pottery'],
  friends: ['Alice', 'Bob', 'Charlie', 'Dave', 'Felicia']
};

// Suppose we want to iterate over the friends property of eve
// We can do it without having to use a counter and incrementing it
// One important point is that in case of the for-of loop, the 'continue' and the 'break' keywords will work
// We will look at some other ways of looping in an array in which they won't. So it is an imp distinction to make
for (const friend of eve.friends) {
  console.log(`${friend}`); // Prints the list of friends
}
// Note that in the above example, we cannot access the index that we are in the array currently
// We can access the current index as well - like this:
for (const friend of eve.friends.entries()) {
  console.log(friend);
}
// Prints:
/*
[0, "Alice"]
[1, "Bob"]
[2, "Charlie"]
and so on... The point being that the index of the element is printed along with the element as an array with two elements
*/

// So you can access the element along with the index using:
// Note here how we are using the destructuring operator
for (const [idx, elm] of eve.friends.entries()) {
  console.log(`Friend ${idx}: ${elm}`);
}
// Prints:
/*
Friend 0: Alice
Friend 1: Bob
Friend 2: Charlie
and so on...
*/
```
## Enhanced Object Literals
- An object literal is when you create a new object by using the {} operator. ES6 introduced 3 new ways in which we can make writing object literals easier.

```js
// Instead of writing properties explicitly in the object, we can create objects outside the object and then refer to it
let friends = {
  alice: {
    name: 'Alice Doe',
    phone: '111-111-1111'
  },
  bob: {
    name: 'Bob Doe',
    phone: '222-222-2222'
  },
  charlie: {
    name: 'Charlie Doe',
    phone: '333-333-3333'
  },
}

// 1st Addition:
// And now we are referencing the object
const felicia = {
  name: 'Felicia',
  dob: '1/1/1990',
  birthPlace: 'New York',
  job: 'Teacher',
  hobbies: ['rock climbing', 'pottery'],
  friendsList: friends
};

// No need for creating an additional property. Just writing 'friends' will add a new property to the object with the same name as 'friends'
const george = {
  name: 'George',
  dob: '1/1/1990',
  birthPlace: 'New York',
  job: 'Teacher',
  hobbies: ['rock climbing', 'pottery'],
  friends
};


// 2nd Addition:
// We can now write methods in objects in a shorter way
const hannah = {
  name: 'Hannah',
  dob: '1/1/1990',
  birthPlace: 'New York',
  job: 'Teacher',
  hobbies: ['rock climbing', 'pottery'],
  friends,

  // Older way of writing methods
  printFriends: function() {
    for (const friend of this.friends) {
      console.log(friend);
    }
  },

  // Newer, shorter way of writing methods:
  printFriendsNew() {
    for (const friend of this.friends) {
      console.log(friend);
    }
  }
};

// 3rd Addition
// Instead of just writing the property names, we can now even compute the property names
const days = ['mon', 'tue', 'wed', 'thu', 'fri', 'sat', 'sun'];
const ila = {
  workingHours: {
    // Note how we are specifying the property names in []. We discussed this way back.
    [days[0]]: {
      leave: '8:00am',
      arrive: '3:00pm'
    },
    [days[1]]: {
      leave: '8:00am',
      arrive: '4:00pm'
    },
    // We can also compute the property names
    [`${'w' + 'e' + 'd'}`] : {
      leave: '8:00am',
      arrive: '5:00pm'
    }
  }
}

console.log(ila.workingHours.mon); // Prints: {leave: "8:00am", arrive: "3:00pm"}
console.log(ila.workingHours.tue); // Prints: {leave: "8:00am", arrive: "4:00pm"}
console.log(ila.workingHours.wed); // Prints: {leave: "8:00am", arrive: "5:00pm"}
```
## Optional Chaining (?.)
- The Optional Chaining operator  `?.`  is used to check if variable *immediately* preceding the operator exists or not. By 'exists' we mean the nullish concept and not the truthy/false concept. A value is nullish only if it is either `null` or `undefined`. If the variable preceding the operator is nullish, then the execution of the statement will immediately return with the value of `undefined`. Else, the execution will proceed as normal.

```js
const jake = {
  workingHours: {
    mon: {
      leave: '8:00am',
      arrive: '3:00pm'
    },
    tue: {
      leave: '8:00am',
      arrive: '4:00pm'
    },
    wed : {
      leave: '8:00am',
      arrive: '5:00pm'
    }
  },

  printWorkingHoursFor(day) {
    // console.log(`${this.workingHours}`)
    return `Leave at ${this.workingHours[day].leave} and arrive at ${this.workingHours[day].arrive}`;
  }
};

// Suppose we were trying to find the working hours of jake on friday. There is no property called 'fri' on the jake object
console.log(jake.workingHours.fri); // Prints: undefined
// But suppose we did not know that, and tried to access the 'leave' property on 'fri'
// console.log(jake.workingHours.fri.leave); // Uncaught TypeError: Cannot read property 'leave' of undefined
// So we would like to have a null check for the 'jake.workingHours.fri' property before we access any properties on it

// We could do that by enclosing it in an if-block or in the && operator
if (jake.workingHours.fri) {
  console.log(jake.workingHours.fri.leave);
}
// or:
jake.workingHours.fri && console.log(jake.workingHours.fri.leave);

// But in ES6, we can use the optional chaining operator.
// Only if the property specified just before the ? exists, only then will the next property will be accessed.
// If not, then immediately 'undefined' will be returned.
// Here 'exists' means the 'Nullish' concept that we talked about before. So the 'leave' property will be accessed
// only if the 'fri' property is either null or undefined. Not if it is empty, or 0, or any other such falsy values
console.log(jake.workingHours.fri?.leave); // undefined

// Consider the following example
const daysOfWeek = ['mon', 'tue', 'wed', 'thu', 'fri', 'sat', 'sun'];
for (const day of daysOfWeek) {
  // Note how we are dynamically using the 'day' variable to specify the property name on the object.
  // If we want to use a variable name as the property name, then we have to use the [] notation.
  // and then using the optional chaining operator to access the 'leave' property on the object only if the object
  // jake.workingHours.day is not null
  console.log(`Work starts at ${jake.workingHours[day]?.leave}`);
}
// Prints:
/*
Work starts at 8:00am
Work starts at 8:00am
Work starts at 8:00am
Work starts at undefined
Work starts at undefined
Work starts at undefined
Work starts at undefined
 */

// 2)
// Optional Chaining also works on methods - we can check if a method actually exists before we call it

// In this line we are first checking if the printWorkingHoursFor method is defined on the jake object.
// If it is not defined, then we print 'Method does not exist' using the Null Coalescing Operator
console.log(jake.printWorkingHoursFor?.('tue') ?? 'Method does not exist'); // Prints: 'Leave at 8:00am and arrive at 4:00pm'
console.log(jake.printWorkingHours?.('tue') ?? 'Method does not exist'); // Prints: 'Method does not exist'


// 3)
// Optional Chaining also works on Arrays
const users = [{name: 'Alice', email:'alice@e.com'}];
// Remember that the ?. operator tests if the object immediately preceding the operator exists or not
// And by exist we again mean the nullish concept, and not the falsy-truthy concept
// So here, it will check if the users[0] exists
console.log(users[0]?.name ?? 'Array is empty'); // Prints: 'Alice'
console.log(users[1]?.name ?? 'Array is empty'); // Prints: 'Array is empty'
```
## Looping Objects: Object Keys, Values, and Entries
- We can use the for-of operator to loop through either the keys, values, or both keys and values of an object.

```js
// Previously we used the for-of loop to loop over arrays, and we said that only iterables can be looped over using the for-of loop
// But we can also use the for-of loop to loop over objects

const kristin = {
  workingHours: {
    mon: {
      leave: '8:00am',
      arrive: '3:00pm'
    },
    tue: {
      leave: '8:00am',
      arrive: '4:00pm'
    },
    wed : {
      leave: '8:00am',
      arrive: '5:00pm'
    },
    thu : {
      leave: '8:00am',
      arrive: '5:00pm'
    }
  },

  printWorkingHoursFor(day) {
    // console.log(`${this.workingHours}`)
    return `Leave at ${this.workingHours[day].leave} and arrive at ${this.workingHours[day].arrive}`;
  }
};

// There are three use cases - we can either loop over the keys (property names), or the values in the object, or both keys and values together

// 1) Loop over the keys (property names)
for (const day of Object.keys(kristin.workingHours)) {
  console.log(day);
}
/*
  Prints:
  mon
  tue
  wed
  thu
 */

// So what is exactly going on?
// As you can see, Object.keys prints an array containing the keys of the object. Then we are just looping over the array
// It only creates an array from the top level properties, does not pick up nested properties of the object passed in as an arg
const keysInTheObject = Object.keys(kristin.workingHours);
console.log(keysInTheObject); // Prints: ["mon", "tue", "wed", "thu"]

// 2) Loop over the values

const valuesInTheObject = Object.values(kristin.workingHours);
console.log(valuesInTheObject);
// We get an array of 4 objects
/*
0: {leave: "8:00am", arrive: "3:00pm"}
1: {leave: "8:00am", arrive: "4:00pm"}
2: {leave: "8:00am", arrive: "5:00pm"}
3: {leave: "8:00am", arrive: "5:00pm"}
*/

// Similar to the previous case, we can log the values now
for (const {leave, arrive} of Object.values(kristin.workingHours)) {
  console.log(`Kristin leaves at ${leave} and arrives at ${arrive}`);
}
/*
Prints:
Kristin leaves at 8:00am and arrives at 3:00pm
Kristin leaves at 8:00am and arrives at 4:00pm
Kristin leaves at 8:00am and arrives at 5:00pm
Kristin leaves at 8:00am and arrives at 5:00pm
*/

// 3) Loop over the both property names and the values - so basically entries
const entriesInTheObject = Object.entries(kristin.workingHours);
console.log(entriesInTheObject);
/*
Note that this is an array
[Array(2), Array(2), Array(2), Array(2)]
[["mon", {…}], ["tue", {…}], ["wed", {…}], ["thu", {…}]]
Prints:
  0: (2) ["mon", {…}]
  1: (2) ["tue", {…}]
  2: (2) ["wed", {…}]
  3: (2) ["thu", {…}]
 */

// And we can loop over the entries in the object like this:
// Note the way that we are destructuring the object. The outermost is an array notation [], and not object notation {}
for (const [day, {leave, arrive}] of Object.entries(kristin.workingHours)) {
  console.log(`On ${day}, Kristin leaves at ${leave} and arrives at ${arrive}`);
}
/*
Prints:
On mon, Kristin leaves at 8:00am and arrives at 3:00pm
On tue, Kristin leaves at 8:00am and arrives at 4:00pm
On wed, Kristin leaves at 8:00am and arrives at 5:00pm
On thu, Kristin leaves at 8:00am and arrives at 5:00pm
 */
```

## Coding Challenge ##2
Let's continue with our football betting app!

    1. Loop over the game.scored array and print each player name to the console, along with the goal number (Example: "Goal 1: Lewandowski")
    2. Use a loop to calculate the average odd and log it to the console (We already studied how to calculate averages, you can go check if you don't remember)
    3. Print the 3 odds to the console, but in a nice formatted way, exaclty like this: Odd of victory Bayern Munich: 1.33 Odd of draw: 3.25 Odd of victory Borrussia Dortmund: 6.5

Get the team names directly from the game object, don't hardcode them (except for "draw"). HINT: Note how the odds and the game objects have the same property names  

BONUS: Create an object called 'scorers' which contains the names of the players who scored as properties, and the number of goals as the value. In this game, it will look like this:

```js
{
 Gnarby: 1,
 Hummels: 1,
 Lewandowski: 2
}
```

```js
const game = {
  team1: 'Bayern Munich',
  team2: 'Borrussia Dortmund',
  players: [
    [
      'Neuer',
      'Pavard',
      'Martinez',
      'Alaba',
      'Davies',
      'Kimmich',
      'Goretzka',
      'Coman',
      'Muller',
      'Gnarby',
      'Lewandowski',
    ],
    [
      'Burki',
      'Schulz',
      'Hummels',
      'Akanji',
      'Hakimi',
      'Weigl',
      'Witsel',
      'Hazard',
      'Brandt',
      'Sancho',
      'Gotze',
    ],
  ],
  score: '4:0',
  scored: ['Lewandowski', 'Gnarby', 'Lewandowski', 'Hummels'],
  date: 'Nov 9th, 2037',
  odds: {
    team1: 1.33,
    x: 3.25,
    team2: 6.5,
  },
};
```

***Solution***
```js
// 1.
for (const [i, player] of game.scored.entries())
  console.log(`Goal ${i + 1}: ${player}`);

// 2.
const odds = Object.values(game.odds);
let average = 0;
for (const odd of odds) average += odd;
average /= odds.length;
console.log(average);

// 3.
for (const [team, odd] of Object.entries(game.odds)) {
  const teamStr = team === 'x' ? 'draw' : `victory ${game[team]}`;
  console.log(`Odd of ${teamStr} ${odd}`);
}

// Odd of victory Bayern Munich: 1.33
// Odd of draw: 3.25
// Odd of victory Borrussia Dortmund: 6.5

// BONUS
// So the solution is to loop over the array, and add the array elements as object properties, and then increase the count as we encounter a new occurence of a certain element
const scorers = {};
for (const player of game.scored) {
  scorers[player] ? scorers[player]++ : (scorers[player] = 1);
}
```

## Sets
- In ES6, two new datastructures were added to JS - Sets and Maps.
- A set is a collection of unique values - there can be no duplicate elements in a set. Hence, sets are often used to remove duplicate elements from an array.
- A set can hold mixed datatypes.
- In the args for the constructor of the set, we can pass in any kind of iterable. Since an array is an iterable, it works. Similarly, if you pass in a single string, that would work as well. The resulting set that would be created would contain the unique characters that are present in the string.
```js
const foodItemsArr = ['Pizza', 'Pasta', 'Pork', 'Pasta', 'Plums'];
const foodItemsSet = new Set(foodItemsArr);
console.log(foodItemsSet); // Prints: {"Pizza", "Pasta", "Pork", "Plums"}

// Just like arrays, sets are also iterables
// Remember that strings are also iterables, hence we can also create a set of characters by using a string
const charsInPizza = new Set('Pizza');
console.log(charsInPizza); // Prints: {"P", "i", "z", "a"}

// Prints the size of the array
console.log(charsInPizza.size); // Prints: 4

// Check if an element exists in a set
console.log(charsInPizza.has('P')); // Prints: true
console.log(charsInPizza.has('Q')); // Prints: false

// We can add elements to a set
foodItemsSet.add('Peas');
console.log(foodItemsSet); // Prints: {"Pizza", "Pasta", "Pork", "Plums", "Peas"}

// We can remove elements from a set
foodItemsSet.delete('Plums');
console.log(foodItemsSet); // Prints: {"Pizza", "Pasta", "Pork", "Peas"}

// Delete all the elements from a set
charsInPizza.clear();
console.log(charsInPizza); // Prints: {}

// Since sets are iterable, we can iterate over a set as well
for (const item of foodItemsSet) {
  console.log(item);
}
/*
  Prints:
  Pizza
  Pasta
  Pork
  Peas
*/

// Sets can be used to remove duplicate elements from an array
const groceryList = ['Pizza', 'Pasta', 'Pork', 'Pasta', 'Plums'];
// Now we want to remove the duplicate items from the groceryList
// In the args for the constructur of the set, we pass in any kind of iterable. Since an array is an iterable, it works.
const uniqueItemsInList = new Set(groceryList);
// And now we can store it back into an array.
// Since the spread operator can take in any iterable as an arg, we can simply do this
const groceryListUnique = [...uniqueItemsInList];
console.log(groceryListUnique); // Prints: ["Pizza", "Pasta", "Pork", "Plums"]

// You could just do the entire thing in one line
const uniqueItemsAgain = [...new Set(groceryList)];
console.log(uniqueItemsAgain); // Prints: ["Pizza", "Pasta", "Pork", "Plums"]

```

## Maps: Fundamentals
- Just like an object, the data in a map is stored as key-value pairs. The difference between the two is that in the case of maps, the keys can have any type, whereas in the case of objects, the keys have to be strings. So maps can have an object, an array, or even another map as a key.
- Note that the insertion order is maintained in maps in JS as mentioned [here on SO](https://stackoverflow.com/questions/17696473/how-to-keep-the-sequence-in-javascript-map/50862944#50862944).

```js
const hannah2 = {
    name: 'Hannah',
    dob: '1/1/1990',
    birthPlace: 'New York',
    job: 'Teacher',
    hobbies: ['rock climbing', 'pottery'],
    friends,

    // Older way of writing methods
    printFriends: function () {
        for (const friend of this.friends) {
            console.log(friend);
        }
    },

    // Newer, shorter way of writing methods:
    printFriendsNew() {
        for (const friend of this.friends) {
            console.log(friend);
        }
    }
};
// Create a new map
const laura = new Map();

// To add elements to a map, we use the set method
laura.set('name', 'Laura Doe');
// We can use different datatypes for keys and values
laura.set(1, 'Alice');
laura.set(2, 'Bob');

// Calling the set() method returns the new map. Hence we can chain the set() operations
laura.set('hobbies', ['rock climbing', 'pottery']).set(3, 'Charlie');

// We can also use boolean values as the key
laura.set(true, 'Laura is available');
laura.set(false, 'Laura is Busy');

// If we log the map now, we see the details
console.log(laura);

/*
Prints:
    Map(7){"name" => "Laura Doe", 1 => "Alice", 2 => "Bob", "hobbies" => Array(2), "3" => "Charlie",…}
    [[Entries]]
    0: {"name" => "Laura Doe"}
    1: {1 => "Alice"}
    2: {2 => "Bob"}
    3: {"hobbies" => Array(2)}
    4: {3 => "Charlie"}
    5: {true => "Laura is available"}
    6: {false => "Laura is Busy"}
 */


// To retrieve elements from the map, we use the get() method
console.log(laura.get('name')); // Prints: 'Laura Doe'
console.log(laura.get(true)); // Prints: 'Laura is available'
// Note that the datatype of the key matters
// For eg. this will print 'undefined' because there is no key with string 'true'
console.log(laura.get('true')); // Prints: 'undefined'

// We can also check whether a map has a certain key
console.log(laura.has('hobbies')); // Prints: true
console.log(laura.has('friends')); // Prints: false

// We can also delete elements from the mapp by passing in the respective key as the argument
laura.delete(3);
console.log(laura);
/*
    Prints:
    0: {"name" => "Laura Doe"}
    1: {1 => "Alice"}
    2: {2 => "Bob"}
    3: {"hobbies" => Array(2)}
    4: {true => "Laura is available"}
    5: {false => "Laura is Busy"}
 */

// We cal also use objects/arrays as map keys

// First let us look at the wrong way of doing it:
// We are adding a new element
laura.set([0, 1], 'An Array');
// And now we try to get the same element
console.log(laura.get([0, 1])); // Prints: 'undefined'
// Why? Because recall that objects are stored by their reference.
// SO you need to store the reference once you have created an array.

// So the correct way of doing it is:
const arrayKey = [1,2];
laura.set(arrayKey, 'Another Array');
console.log(laura.get(arrayKey)); // Prints: 'Another Array'

// Just to visually confirm that the array is in fact being stored as the key
console.log(laura);
/*
0: {"name" => "Laura Doe"}
1: {1 => "Alice"}
2: {2 => "Bob"}
3: {"hobbies" => Array(2)}
4: {true => "Laura is available"}
5: {false => "Laura is Busy"}
6: {Array(2) => "An Array"}
    key: (2) [0, 1]
    value: "An Array"
7: {Array(2) => "Another Array"}
    key: (2) [1, 2]
    value: "Another Array"
 */


// You can get the size of a map by doing
console.log(laura.size); // Prints: 6

// We can remove all the elements from the map
laura.clear();
console.log(laura); // Prints: Map(0) {}

```

## Maps: Iterataion
- Instead of using the set method to add elements to a map, you can just add the elements all at once by passing in an array as shown in the example below. This allows us to easily create maps from existing objects.
- Similarly, we can use existing maps to convert them into arrays by using the spread operator.

```js
// There are other ways of populating a new map other than using the set() method that we used previously
const maria = new Map([
    ['name', 'Maria Doe'],
    ['friends', ['Alice', 'Bob', 'Charlie']],
    ['hobbies', ['Stamp Collecting']]
]);

console.log(maria); // Prints: {"name" => "Maria Doe", "friends" => Array(3), "hobbies" => Array(1)}

// Note that the constructor for the Map in the above example takes an array of arrays as an arg.

const kristin2 = {
    workingHours: {
        mon: {
            leave: '8:00am',
            arrive: '3:00pm'
        },
        tue: {
            leave: '8:00am',
            arrive: '4:00pm'
        },
        wed: {
            leave: '8:00am',
            arrive: '5:00pm'
        },
        thu: {
            leave: '8:00am',
            arrive: '5:00pm'
        }
    }
};

// Recall the Object.entries() method that we looked at back in Lecture 113
const kristinActiveHours = Object.entries(kristin2.workingHours);
console.log(kristinActiveHours);
/*
Prints:
0: (2) ["mon", {…}]
1: (2) ["tue", {…}]
2: (2) ["wed", {…}]
3: (2) ["thu", {…}]
 */

// Converting Objects to a Map

// So this gives us an efficient way of converting objects to map
const kristinHoursMap = new Map(kristinActiveHours);
console.log(kristinHoursMap);
/*
Prints:
0: {"mon" => Object}
key: "mon"
value: {leave: "8:00am", arrive: "3:00pm"}
1: {"tue" => Object}
key: "tue"
value: {leave: "8:00am", arrive: "4:00pm"}
2: {"wed" => Object}
key: "wed"
value: {leave: "8:00am", arrive: "5:00pm"}
3: {"thu" => Object}
key: "thu"
value: {leave: "8:00am", arrive: "5:00pm"}
 */

// We can iterate over the map by doing
for (const [day, {leave, arrive}] of kristinHoursMap) {
    console.log(`On ${day}, Kristin2 leaves at ${leave} and arrives at ${arrive}`);
}

/*
Prints:
    On mon, Kristin2 leaves at 8:00am and arrives at 3:00pm
    On tue, Kristin2 leaves at 8:00am and arrives at 4:00pm
    On wed, Kristin2 leaves at 8:00am and arrives at 5:00pm
    On thu, Kristin2 leaves at 8:00am and arrives at 5:00pm
 */


// Converting Map back to Array
// By just using the spread operator and unpacking the map into an array -
console.log([...kristinHoursMap]);
/*
0: (2) ["mon", {…}]
1: (2) ["tue", {…}]
2: (2) ["wed", {…}]
3: (2) ["thu", {…}]
 */

```
## Coding Challenge ##3
Let's continue with our football betting app! This time, we have a map with a log of the events that happened during the game. The values are the events themselves, and the keys are the minutes in which each event happened (a football game has 90 minutes plus some extra time).

    1. Create an array 'events' of the different game events that happened (no duplicates)
    2. After the game has finished, is was found that the yellow card from minute 64 was unfair. So remove this event from the game events log.
    3. Print the following string to the console: "An event happened, on average, every 9 minutes" (keep in mind that a game has 90 minutes)
    4. Loop over the events and log them to the console, marking whether it's in the first half or second half (after 45 min) of the game, like this: [FIRST HALF] 17: ⚽️ GOAL

```js
const gameEvents = new Map([
  [17, '⚽️ GOAL'],
  [36, '🔁 Substitution'],
  [47, '⚽️ GOAL'],
  [61, '🔁 Substitution'],
  [64, '🔶 Yellow card'],
  [69, '🔴 Red card'],
  [70, '🔁 Substitution'],
  [72, '🔁 Substitution'],
  [76, '⚽️ GOAL'],
  [80, '⚽️ GOAL'],
  [92, '🔶 Yellow card'],
]);
```

***Solution***

```js
// 1.
const events = [...new Set(gameEvents.values())];
console.log(events);

// 2.
gameEvents.delete(64);

// 3.
console.log(
  `An event happened, on average, every ${90 / gameEvents.size} minutes`
);
const time = [...gameEvents.keys()].pop();
console.log(time);
console.log(
  `An event happened, on average, every ${time / gameEvents.size} minutes`
);

// 4.
for (const [min, event] of gameEvents) {
  const half = min <= 45 ? 'FIRST' : 'SECOND';
  console.log(`[${half} HALF] ${min}: ${event}`);
}
```

## Working With Strings

```js
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Lecture 120: Working with Strings Part 1
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

const airline = 'TAP Air Portugal';
const plane = 'A320';

console.log(plane[0]); // Prints: 'A'
console.log(plane[1]); // Prints: '3'
console.log(plane[2]); // Prints: '2'
console.log('B737'[0]); // Prints: 'B'

console.log(airline.length); // Prints: 16
console.log('B737'.length); // Prints: 4

console.log(airline.indexOf('r')); // Prints: 6

// Search from the end of the string
console.log(airline.lastIndexOf('r')); // Prints: 10

// Search for the occurrence of the word
console.log(airline.indexOf('portugal')); // Prints: -1. Because it is case-sensitive and string contains 'Portugal' not 'portugal'

// Slice the string starting from index 4 to the end of the string
console.log(airline.slice(4)); // Prints: 'Air Portugal'

// Slice the string from index 4 included, index 7 excluded
console.log(airline.slice(4, 7)); // Prints: 'Air'

// Start from the index 0, right up to the first occurrence of the ' '
console.log(airline.slice(0, airline.indexOf(' '))); // Prints: 'TAP'

// Start from the index AFTER the last index of ' ', right up to the end of the string
console.log(airline.slice(airline.lastIndexOf(' ') + 1)); // Prints: 'Portugal'

// Start from the end of the string. Print the first two characters
console.log(airline.slice(-2)); // Prints: 'al'

// Start from the index 1 print up to the index before the last one
console.log(airline.slice(1, -1)); // Prints: 'AP Air Portuga'

// JS internally changes the type of string by boxing and unboxing as required
console.log(typeof 'JavaScript Strings'); // Prints: string
console.log(typeof new String('JavaScript Strings')); // Prints: object. Warning: Primitive type object wrapper used
console.log(typeof String('JavaScript Strings')); // Prints: string

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Lecture 121: Working with Strings Part 2
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

const anotherAirline = 'TAP Air Portugal';

console.log(anotherAirline.toLowerCase());
console.log(anotherAirline.toUpperCase());

// Comparing emails
const email = 'hello@jonas.io';
const loginEmail = '  Hello@Jonas.Io \n';
// Note that the trim() method will also remove the \n character from the email
const normalizedEmail = loginEmail.toLowerCase().trim();
console.log(normalizedEmail);
console.log(email === normalizedEmail); // Prints: true

// replacing
const priceGB = '288,97£';
// replace() calls can also be chained because replace() returns the resulting string
const priceUS = priceGB.replace('£', '$').replace(',', '.');
console.log(priceUS); // Prints: 288.97$

const announcement = 'All passengers come to boarding door 23. Boarding door 23!';

// Note that the replace() method will replace ONLY the first occurrence of the string
// Here 'door' is the value to be searched, and 'gate' is the value to be replaced
console.log(announcement.replace('door', 'gate'));
// Prints: All passengers come to boarding gate 23. Boarding door 23!

// replaceAll() will replace ALL occurrences of the string
console.log(announcement.replaceAll('door', 'gate'));
// Prints: All passengers come to boarding gate 23. Boarding gate 23!

// We can also use regex to replace the string 'door'
// The string to be searched is placed between / / and g is appended to tell JS to replace everywhere
console.log(announcement.replace(/door/g, 'gate'));

// Booleans
const anotherPlane = 'Airbus A320neo';
console.log(anotherPlane.includes('A320')); // Prints: true
console.log(anotherPlane.includes('Boeing')); // Prints: false
console.log(anotherPlane.startsWith('Airb')); // Prints: true

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Lecture 122: Working with Strings Part 3
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

// Split and join
console.log('a+very+nice+string'.split('+')); // Prints: ["a", "very", "nice", "string"]
console.log('Alice Doe'.split(' ')); // Prints: ["Alice", "Doe"]

// We can split and store the results directly using destructuring
const [fName, lName] = 'Alice Doe'.split(' ');

// We can join strings:
const newName = ['Ms.', fName, lName].join(' ');
console.log(newName); // Prints: Ms. Alice Doe

// Changing the joiner
const newName2 = ['Ms.', fName, lName].join('_');
console.log(newName2); // Prints: Ms._Alice_Doe

// Capitalize just the first letter of every word of a name
const capitalizeName = function (name) {
    const splitName = name.toLowerCase().split(' ');
    const capitalizedNameArr = [];
    for (const partialName of splitName) {
        capitalizedNameArr.push(partialName[0].toUpperCase() + partialName.slice(1));
    }
    return capitalizedNameArr.join(' ');
}
console.log(capitalizeName('jessica ann smith davis')); // Prints: Jessica Ann Smith Davis

// Padding
// Adding characters to the beginning or the end of the string until the string is of a desired length
const message = 'Go to gate 23!';
console.log(message.padStart(20, '+')); // Prints: ++++++Go to gate 23!
console.log(message.padEnd(20, '+')); // Prints: Go to gate 23!++++++

// First pad the string on the left to 20, then pad the resultant padded string on the right till 30
console.log(message.padStart(20, '+').padEnd(30, '-')); // Prints: ++++++Go to gate 23!---------

// Repeat a string 
const message2 = 'Bad weather...';
console.log(message2.repeat(5));
// Prints: Bad weather...Bad weather...Bad weather...Bad weather...Bad weather...
```

## Coding Challenge ##4
Write a program that receives a list of variable names written in underscore_case and convert them to camelCase.

The input will come from a textarea inserted into the DOM (see code below), and conversion will happen when the button is pressed.

THIS TEST DATA (pasted to textarea)

```js
underscore_case
	first_name
Some_Variable
	calculate_AGE
delayed_departure
```

SHOULD PRODUCE THIS OUTPUT (5 separate console.log outputs)

```js
underscoreCase      ✅
firstName           ✅✅
someVariable        ✅✅✅
calculateAge        ✅✅✅✅
delayedDeparture    ✅✅✅✅✅
```
HINT 1: Remember which character defines a new line in the textarea 😉 
HINT 2: The solution only needs to work for a variable made out of 2 words, like a_b 
HINT 3: Start without worrying about the ✅. Tackle that only after you have the variable name conversion working 😉 
HINT 4: This challenge is difficult on purpose, so start watching the solution in case you're stuck. Then pause and continue!

Afterwards, test with your own test data!

***SOlution***
```js
document.body.append(document.createElement('textarea'));
document.body.append(document.createElement('button'));

document.querySelector('button').addEventListener('click', function () {
  const text = document.querySelector('textarea').value;
  const rows = text.split('\n');

  for (const [i, row] of rows.entries()) {
    const [first, second] = row.toLowerCase().trim().split('_');

    const output = `${first}${second.replace(
      second[0],
      second[0].toUpperCase()
    )}`;
    console.log(`${output.padEnd(20)}${'✅'.repeat(i + 1)}`);
  }
});
```

## String Methods Practice

```js
///////////////////////////////////////
// String Methods Practice

const flights = '_Delayed_Departure;fao93766109;txl2133758440;11:25+_Arrival;bru0943384722;fao93766109;11:45+_Delayed_Arrival;hel7439299980;fao93766109;12:05+_Departure;fao93766109;lis2323639855;12:30';

// 🔴 Delayed Departure from FAO to TXL (11h25)
//              Arrival from BRU to FAO (11h45)
//   🔴 Delayed Arrival from HEL to FAO (12h05)
//            Departure from FAO to LIS (12h30)

const getCode = str => str.slice(0, 3).toUpperCase();

for (const flight of flights.split('+')) {
  const [type, from, to, time] = flight.split(';');
  const output = `${type.startsWith('_Delayed') ? '🔴' : ''}${type.replaceAll(
    '_',
    ' '
  )} ${getCode(from)} ${getCode(to)} (${time.replace(':', 'h')})`.padStart(36);
  console.log(output);
}
```

[BACK ⬅️](https://github.com/subhadeeppaul/JavaScript-Notes)
