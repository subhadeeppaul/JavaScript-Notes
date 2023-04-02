
# Working With Arrays
- Arrays are objects, and as we have seen, objects can have functions of their own that are called methods. There are several methods that are defined on the array object.

## Simple Array Methods

```js
// Array Declaration
let dogs = ["Bulldog", "Beagle", "Labrador"]; 
let dogs = new Array("Bulldog", "Beagle", "Labrador");  // declaration

alert(dogs[1]);             // access value at index, first item being [0]
dogs[0] = "Bull Terier";    // change the first item

for (let i = 0; i < dogs.length; i++) {     // parsing with array.length
console.log(dogs[i]);
}
```

## Methods
```js
dogs.toString();                        // convert to string: results "Bulldog,Beagle,Labrador"
dogs.join(" * ");                       // join: "Bulldog * Beagle * Labrador"
dogs.pop();                             // remove last element
dogs.push("Chihuahua");                 // add new element to the end
dogs[dogs.length] = "Chihuahua";        // the same as push
dogs.shift();                           // remove first element
dogs.unshift("Chihuahua");              // add new element to the beginning
delete dogs[0];                         // change element to undefined (not recommended)
dogs.splice(2, 0, "Pug", "Boxer");      // add elements (where, how many to remove, element list)
let animals = dogs.concat(cats,birds);  // join two arrays (dogs followed by cats and birds)
dogs.slice(1,4);                        // elements from [1] to [4-1]
dogs.sort();                            // sort string alphabetically
dogs.reverse();                         // sort string in descending order
x.sort(function(a, b){return a - b});   // numeric sort
x.sort(function(a, b){return b - a});   // numeric descending sort
highest = x[0];                         // first item in sorted array is the lowest (or highest) value
x.sort(function(a, b){return 0.5 - Math.random()});     // random order sort
```
- **pop():** This method is used for removing the last element of an array.
- **push():** This method is used for adding a new element at the very end of an array.
- **concat():** This method is used for joining various arrays into a single array.
- **reverse():** This method is used for reversing the order of the elements in an array.
- **shift():** This method is used for removing the first element of an array.
- **slice():** This method is used for pulling a copy of a part of an array into a new array.
- **splice():** This method is used for adding elements in a particular way and position.
- **toString():** This method is used for converting the array elements into strings.
- **unshift():** This method is used for adding new elements at the beginning of the array.
- **valueOf():** This method is used for returning the primitive value of the given object.
- **indexOf():** This method is used for returning the first index at which a given element is found in an array.
- **lastIndexOf():** This method is used for returning the final index at which a given element appears in an array.
- **join():** This method is used for combining elements of an array into one single string and then returning it.
- **sort():** This method is used for sorting the array elements based on some condition.
concat, copyWithin, every, fill, filter, find, findIndex, forEach, indexOf, isArray, join, lastIndexOf, map, pop, push, reduce, reduceRight, reverse, shift, slice, some, sort, splice, toString, unshift, valueOf

```js
/////////////////////////////////////////////////
// Simple Array Methods
let arr = ['a', 'b', 'c', 'd', 'e'];

// SLICE: Extract part of the array WITHOUT changing the original array (i.e. returns a new array)
console.log(arr.slice(2)); // Prints: ["c", "d", "e"]
console.log(arr.slice(2, 4)); // Prints: ["c", "d"]
console.log(arr.slice(-2)); // Prints: ["d", "e"]
console.log(arr.slice(-1)); // Prints: ["e"]
console.log(arr.slice(1, -2)); // Prints: ["b", "c"]
console.log(arr.slice()); // Prints: ["a", "b", "c", "d", "e"] i.e. returns a shallow copy of the original array
console.log([...arr]); // But this method of creating a shallow copy is much easier

console.log(arr); // Prints: ["a", "b", "c", "d", "e"]. i.e. original array is not mutated in any way


// SPLICE: MUTATES THE ORIGINAL ARRAY. Functionally, it is same as slice().
// console.log(arr.splice(2)); // Prints: ["c", "d", "e"]
// But now, notice what happens to our original array. The above extracted elements are basically gone from the original array
console.log(arr); // Prints: ["a", "b"]
// Hence the splice() method is normally used for deleting one or more elements from the array
// One common use case is to remove the last element from an array
console.log(arr.splice(-1));// Prints: ["b"]
console.log(arr); // Prints: ["a"]


// Note that the second args of the splice() method is the number of elements that should be deleted
arr = ['a', 'b', 'c', 'd', 'e'];
console.log(arr.splice(2, 2)); // Prints: ["c", "d"]
console.log(arr); // Prints: ["a", "b", "e"]

// REVERSE: MUTATES THE ORIGINAL ARRAY. Reverses the array
arr = ['a', 'b', 'c', 'd', 'e'];
const arr2 = ['j', 'i', 'h', 'g', 'f'];
console.log(arr2.reverse()); // Prints: ["f", "g", "h", "i", "j"]
console.log(arr2); // Prints: ["f", "g", "h", "i", "j"]. The original array is mutated


// CONCAT: Join two arrays. Does not change either of the two inout arrays.
const letters = arr.concat(arr2);
console.log(letters); // Prints: ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j"]
// But we can also concat two arrays using this:
console.log([...arr, ...arr2]);


// JOIN: join all the elements of an array using the specified separator
console.log(letters.join(' - ')); // Prints: a - b - c - d - e - f - g - h - i - j
console.log(typeof letters.join(' - ')); // Note that the type of the result after join is a string

------------------------------------------------------------------

// Just for the sake of completion - we ahve already looked at these methods earlier

// push: Add elements to the end of the array.
arr = ['a', 'b', 'c', 'd', 'e'];
console.log(arr.push('f')); // Prints: 6. Because it returns the size of the resulting array
console.log(arr); // Prints: ["a", "b", "c", "d", "e", "f"]

// unshift: Add elements to the beginning of the array.
arr = ['b', 'c', 'd', 'e'];
console.log(arr.unshift('a')); // Prints: 5. Because it returns the size of the resulting array
console.log(arr); // Prints: ["a", "b", "c", "d", "e", "f"]

// pop: Removes the last element of the array. Returns the removed element.
arr = ['a', 'b', 'c', 'd', 'e'];
console.log(arr.pop()); // Prints: 'e'
console.log(arr); // Prints: ["a", "b", "c", "d"]

// shift: Remove the first element of the array.
arr = ['a', 'b', 'c', 'd', 'e'];
console.log(arr.shift()); // Prints: 'a'
console.log(arr); // Prints: ["b", "c", "d", "e"]

// indexof: Find the index at which a particular element is at
arr = ['a', 'b', 'c', 'd', 'e'];
console.log(arr.indexOf('c')); // Prints: 2
console.log(arr.indexOf('f')); // Prints: -1

// includes: Find if the element exists in an array
arr = ['a', 'b', 'c', 'd', 'e'];
console.log(arr.includes('c')); // Prints: true
console.log(arr.includes('f')); // Prints: false



```
## The new at Method - ES-2022
```js
///////////////////////////////////////
// The new at Method
const arr = [23, 11, 64];
console.log(arr[0]);
console.log(arr.at(0));

// getting last array element
console.log(arr[arr.length - 1]);
console.log(arr.slice(-1)[0]);
console.log(arr.at(-1));

console.log('jonas'.at(0));
console.log('jonas'.at(-1));
```
## Looping Arrays: forEach

- We can loop over arrays using either the `for-of` loop that we looked at earlier. Or we can use the `forEach` loop.
- The difference between the two is that you can use keywords like `break` and `continue` to break out of a `for-of` loop, but you cannot do that with a `forEach` loop. The `forEach` loop will be executed for each element in the collection by default.


```js
// Arrow function
forEach((element) => { /* … */ })
forEach((element, index) => { /* … */ })
forEach((element, index, array) => { /* … */ })

// Callback function
forEach(callbackFn)
forEach(callbackFn, thisArg)

// Inline callback function
forEach(function(element) { /* … */ })
forEach(function(element, index) { /* … */ })
forEach(function(element, index, array){ /* … */ })
forEach(function(element, index, array) { /* … */ }, thisArg)
```
- **Note:** There is no way to stop or break a forEach() loop other than by throwing an exception. If you need such behavior, the forEach() method is the wrong tool.
- **Note:** forEach expects a synchronous function. forEach does not wait for promises. Make sure you are aware of the implications while using promises (or async functions) as forEach callback.

```js
///////////////////////////////////////
// Looping Arrays: forEach
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300];

// for (const movement of movements) {
for (const [i, movement] of movements.entries()) {
  if (movement > 0) {
    console.log(`Movement ${i + 1}: You deposited ${movement}`);
  } else {
    console.log(`Movement ${i + 1}: You withdrew ${Math.abs(movement)}`);
  }
}

console.log('---- FOREACH ----');
movements.forEach(function (mov, i, arr) {
  if (mov > 0) {
    console.log(`Movement ${i + 1}: You deposited ${mov}`);
  } else {
    console.log(`Movement ${i + 1}: You withdrew ${Math.abs(mov)}`);
  }
});
// 0: function(200)
// 1: function(450)
// 2: function(400)
// ...
```
- **ForEach** exclusively belong to the royal family of Arrays. The forEach method was introduced with lineage to the prototypal inheritance of Array object! Needless to say, the forEach clause works only with those data structure which are Arrays. The method basically iterates over the elements of the array and executes a callback function [basically some executable function/ fun activity].
- **The for-of loop** is adequately new to the JS world and packs in super-powers! Voilaaaaaaa! The for-of loop creates a loop iterating over iterable member objects. The list is an extensive one such as Array, Map, Set, String, TypedArray etc

```js
let friends = ['Alice', 'Bob', 'Charlie', 'Dave', 'Eve'];

// We saw earlier how to loop over an iterable using a for-of loop
for (const friend of friends) {
    console.log(`Friend's name: ${friend}`);
}
// And we could access the index in a for-of loop using:
for (const [i, friend] of friends.entries()) {
    if (friend === 'Alice') continue;
    console.log(`${i}: Friend's name: ${friend}`);
}

// Instead, we can use a forEach loop, that uses a callback function.
// forEach, in this case, is an example of a higher-order function because it accepts another function as an arg
// The callback fn in the forEach method accepts 3 parameters:
// 1) the element of the array itself
// 2) the index of the element
// 3) the entire original array
// Just like in previous method, we can pass in only part of the parameters that are required, and that would work as well
friends.forEach(function (friend, index, arr) {
    // if (friend === 'Alice') break; Cannot use 'break' or 'continue' within a forEach loop
    console.log(`${index} - Friend's name in forEach: ${friend}`);
})

/*
0 - Friend's name in forEach: Alice
1 - Friend's name in forEach: Bob
2 - Friend's name in forEach: Charlie
3 - Friend's name in forEach: Dave
4 - Friend's name in forEach: Eve
*/

```

## forEach With Maps and Sets
- The Map.forEach method is used to loop over the map with the given function and executes the given function over each key-value pair.
- Syntax:
```js
myMap.forEach(callback, value, key, thisArg)
```
- **Parameters:** This method accepts four parameters as mentioned above and described below:
    - **callback:** This is the function that executes on each function call.
    - **value:** This is the value for each iteration.
    - **key:** This is the key to reach iteration.
    - **thisArg:** This is the value to use as this when executing callback.
- **Returns:** It returns the undefined value.

```js
///////////////////////////////////////
// forEach With Maps and Sets
// Map
const currencies = new Map([
  ['USD', 'United States dollar'],
  ['EUR', 'Euro'],
  ['GBP', 'Pound sterling'],
]);

currencies.forEach(function (value, key, map) {
  console.log(`${key}: ${value}`);
});

/*
Prints:
Symbol: USD, stands for United States dollar
Symbol: EUR, stands for Euro
Symbol: GBP, stands for Pound sterling
 */

// Set
const currenciesUnique = new Set(['USD', 'GBP', 'USD', 'EUR', 'EUR']);
console.log(currenciesUnique);
// Since there are no keys in a set, the 'value' args is passed in as the 'key' arg as well
currenciesUnique.forEach(function (value, key, map) {
  console.log(`${key}: ${value}`);
});

/*
Prints:
USD: USD
GBP: GBP
EUR: EUR
 */

// In JS we have a convention, we can use '_' to denote a throwaway variable. Hence the above can be rewritten as:
currenciesUnique.forEach(function (value, _, map) {
    console.log(`${value}`);
});
```
## Creating DOM Elements

- Instead of working with global variables, start passing the data that function needs actually into that function.
- The `insertAdjacentHTML()` method of the `Element` interface parses the specified text as HTML or XML and inserts the resulting nodes into the DOM tree at a specified position.
```js
// Syntax
insertAdjacentHTML(position, text)
```
- The [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element) property innerHTML gets or sets the HTML or XML markup contained within the element.
- To insert the HTML into the document rather than replace the contents of an element, use the method [insertAdjacentHTML()](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML).

```js
// We can dynamically generate HTML elements
const alice = {
    name: 'Alice Doe',
    age: 21,
    birthYear: 1990,
    friends: ['Bob', 'Charlie', 'Dave', 'Eve'],
}

// First, select the div that you want to insert the html into
const movementContainer = document.querySelector('.movements');

const displayFriendsFor = function (person) {

    // This is an important method
    // This returns the entire inner html inside the movementContainer
    console.log(movementContainer.innerHTML);

    /*
    Prints:
    <div class="movements__row">
          <div class="movements__type movements__type--deposit">2 deposit</div>
          <div class="movements__date">3 days ago</div>
          <div class="movements__value">4 000€</div>
        </div>
        <div class="movements__row">
          <div class="movements__type movements__type--withdrawal">
            1 withdrawal
          </div>
          <div class="movements__date">24/01/2037</div>
          <div class="movements__value">-378€</div>
    </div>
     */

    // We looked at a similar property called 'textContent' earlier. That returned only the text, innerHTML returns the entire HTML
    console.log(movementContainer.textContent);
    /*
    Prints:
    2 deposit
          3 days ago
          4 000€
            1 withdrawal
          24/01/2037
          -378€
     */

    // Here, we are using it as a setter, removing the existing HTML.
    movementContainer.innerHTML = '';
    console.log(movementContainer.innerHTML); // Prints the empty string

    // Now we loop over each of the friends, adding a new div containing the friend name into selected element
    person.friends.forEach(
        function (friend, idx) {
            const html = `<div class="movements__row">Friend ${idx + 1}: ${friend}</div>`;
            // We use the insertAdjacentHTML to add HTML
            // 'afterbegin' denotes the position where you want to insert HTML.
            // There are 4 different places where html can be inserted, check MDN
            movementContainer.insertAdjacentHTML("afterbegin", html);
        })
}

displayFriendsFor(alice);
```

## Coding Challenge #1
Julia and Kate are doing a study on dogs. So each of them asked 5 dog owners about their dog's age, and stored the data into an array (one array for each). For now, they are just interested in knowing whether a dog is an adult or a puppy. A dog is an adult if it is at least 3 years old, and it's a puppy if it's less than 3 years old.

Create a function 'checkDogs', which accepts 2 arrays of dog's ages ('dogsJulia' and 'dogsKate'), and does the following things:

    1. Julia found out that the owners of the FIRST and the LAST TWO dogs actually have cats, not dogs! So create a shallow copy of Julia's array, and remove the cat ages from that copied array (because it's a bad practice to mutate function parameters)
    2. Create an array with both Julia's (corrected) and Kate's data
    3. For each remaining dog, log to the console whether it's an adult ("Dog number 1 is an adult, and is 5 years old") or a puppy ("Dog number 2 is still a puppy 🐶")
    4. Run the function for both test datasets

HINT: Use tools from all lectures in this section so far 😉

TEST DATA 1: Julia's data [3, 5, 2, 12, 7], Kate's data [4, 1, 15, 8, 3] TEST DATA 2: Julia's data [9, 16, 6, 8, 3], Kate's data [10, 5, 6, 1, 4]

```js
const DogsJulia = [3, 5, 2, 12, 7];
const DogsKate = [10, 5, 6, 1, 4];

const checkDogs = function (dogsJulia, dogsKate) {
  let dogsJuliaCorrected = dogsJulia;
  dogsJuliaCorrected.shift();
  dogsJuliaCorrected.splice(-2);

  const totalDogs = dogsJuliaCorrected.concat(dogsKate);

  totalDogs.forEach(function (age, i) {
    age > 3
      ? console.log(`Dog number ${i + 1} is Adult and ${age} years old `)
      : console.log(`Dog number ${i + 1} is Puppy and ${age} years old `);
  });
};
checkDogs(DogsJulia, DogsKate);
```

# Data Transformations: map, filter, reduce
- This image shows what each of these methods do on a high level:

![Map_Filter_Reduce.png]([https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/Map_Filter_Reduce.png))


## The `map` method
- The `map` method returns a new array. It does not mutate the original array.
- For every element in the original array, the callback function passed into the map method is executed on that element. The result is stored in a new array, and that array is returned as the result.
- A rule of thumb is that the `forEach` method is used in case you want to produce side-effects. Use the `map` method when you want to follow a functional paradigm where you return a new array and do nto mutate the state of any existing objects.
```js
///////////////////////////////////////
// The map Method
// Suppose the given problem is to convert an array containing values in Euros to values in Dollars
const movements = [100, 150, 200, 250, -300];
const eurToUsd = 1.1;

// This is what we would do if we were using a simple for loop
const movementsUSDfor = [];
for (const mov of movements) {
    movementsUSDfor.push(mov * eurToUsd);
}
console.log(movementsUSDfor);

// But using the map we can just do this.
// the map() calls a defined callback function on each element of an array,
// and returns a new array that contains the results.
// Just like the forEach method, the callback function in the map method also accepts the same 3 parameters
// currElement, index, entire array
// Here we are making use of only the current element
const movementsUSD = movements.map(function (mov) {
    return mov * eurToUsd;
});
// Note that the returned value is an array
console.log(movementsUSD); // Prints: [110.00000000000001, 165, 220.00000000000003, 275, 330]

// We can also just use the arrow function as the callback
const movementsUSDArr = movements.map(mov => mov * eurToUsd);
console.log(movementsUSDArr); // Prints: [110.00000000000001, 165, 220.00000000000003, 275, 330]


// You can return a completely different array
const movementsDescriptions = movements.map(
    (mov, i) =>
        `Movement ${i + 1}: You ${mov > 0 ? 'deposited' : 'withdrew'} ${Math.abs(
            mov
        )}`
);

const movementDescriptions2 = movements.map(function (mov, idx) {
    if (mov > 0) {
        return `Movement ${idx + 1}: You deposited ${mov}`
    } else {
        return `Movement ${idx + 1}: You withdrew ${Math.abs(mov)}`
    }
})

console.log(movementDescriptions2);
// Prints:
// ["Movement 1: You deposited 100", "Movement 2: You deposited 150", "Movement 3: You deposited 200", "Movement 4: You deposited 250", "Movement 5: You withdrew 300"]

```
- forEach creates *Side Effects*
    - Basically a side-effect means something is mutating/changing existing data. Like changing a value in an existing array.
    - Basically anything that 'changes' existing data instead of cloning / returning new values is a 'side effect'

```js
// Example of Side Effect
const arr = [1, 2, 3];
 
function sideEffect() {
  arr.pop();
}
 
sideEffect();
console.log(arr); // [1, 2] Mutates the original array.
```
## Computing Usernames
- each function should actually receive the data that it should work with, instead of using a global variable.

```js
// Data
const account1 = {
    owner: 'Jonas Schmedtmann',
    movements: [200, 450, -400, 3000, -650, -130, 70, 1300],
    interestRate: 1.2, // %
    pin: 1111,
};

const account2 = {
    owner: 'Jessica Davis',
    movements: [5000, 3400, -150, -790, -3210, -1000, 8500, -30],
    interestRate: 1.5,
    pin: 2222,
};

const account3 = {
    owner: 'Steven Thomas Williams',
    movements: [200, -200, 340, -300, -20, 50, 400, -460],
    interestRate: 0.7,
    pin: 3333,
};

const account4 = {
    owner: 'Sarah Smith',
    movements: [430, 1000, 700, 50, 90],
    interestRate: 1,
    pin: 4444,
};

const accounts = [account1, account2, account3, account4];

// The requirement is as follows:
// Convert each of the names of the owners to their initials and return a new array
// Input: accounts
// Output: ['js', 'jd', 'stw', 'ss']
const userName = accounts.map(function (account, idx) {
    return account.owner.toLowerCase().split(' ')
        .map(function (name) {
            return name[0];
        })
        .join('');
});
console.log(userName); // Prints: ["js", "jd", "stw", "ss"]

// Rewriting the above as an arrow function
const userNameArr = accounts.map( account => {
    return account.owner.toLowerCase().split(' ')
        .map(name => name[0])
        .join('');
});
console.log(userNameArr);  // Prints: ["js", "jd", "stw", "ss"]
```
### The filter Method
- The filter method is used to return a new array that contains only those elements from the original array that have passed a specific condition.
- Just like the map method, the filter method also accepts a callback function, and just like the callback function in the map method, the callback function in the filter method also accepts three args, namely - currentElement, index, entire array.
```js
///////////////////////////////////////
// The filter Method
const transactions = [200, -200, 340, -300, -20, 50, 400, -460];
const deposits = transactions.filter(amt => amt > 0);
console.log(deposits); // Prints: [200, 340, 50, 400]
// Original array is not modified in any way
console.log(transactions); // Prints: [200, -200, 340, -300, -20, 50, 400, -460]
```
### The Reduce Method
- The `reduce` method is used to compute a single value using all the values in the original array.
- The callback function that is passed into the `reduce` method is different compared to the ones passed to `map` or `forEach`. In the callback for the `reduce` method, the first parameter is the *accumulator*. This accumulator stores the value that will be finally returned from the `reduce` function. So, for example, if we are using the reduce method to calculate the sum of all the elements in an array, then the *accumulator* would simply return the final sum.
- The `reduce` method also accepts a second argument which is the starting value of the *accumulator*.
```js
///////////////////////////////////////
// The reduce Method
// Note that the callback function of the reduce method accepts the 'accumulator' as the first args
// The reduce function, on the other hand, accepts a second args which is the starting value of the 'accumulator'
// In this case, we are passing in the initial value as 0, as can be seen from the second args
let values = [200, -200, 340, -300, -20, 50, 400, -460];
const sum = values.reduce(function (acc, currElmnt, idx, arr) {
    console.log(`In Iteration ${idx}: acc is: ${acc}`);
    return acc + currElmnt;
}, 0);
console.log(sum); // Returns: 10
/*
In Iteration 0: acc is: 0
In Iteration 1: acc is: 200
In Iteration 2: acc is: 0
In Iteration 3: acc is: 340
In Iteration 4: acc is: 40
In Iteration 5: acc is: 20
In Iteration 6: acc is: 70
In Iteration 7: acc is: 470
 */

// Now you can see the difference when we pass in a non-zero value as the starting point of the accumulator
const sum2 = values.reduce(function (acc, currElmnt, idx, arr) {
    console.log(`In Iteration ${idx}: acc is: ${acc}`);
    return acc + currElmnt;
}, 100);
console.log(sum2); // Returns: 110
/*
Prints:
In Iteration 0: acc is: 100
In Iteration 2: acc is: 100
In Iteration 3: acc is: 440
In Iteration 4: acc is: 140
In Iteration 1: acc is: 300
In Iteration 5: acc is: 120
In Iteration 6: acc is: 170
In Iteration 7: acc is: 570
 */

// Calculate the maximum value in the array
// Can you see exactly how this code is working now?????
// Calls the specified callback function for all the elements in an array.
// The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.
// The reduce method calls the callbackfn one time for each element in the array.
// If initialValue is specified, it is used as the initial value to start the accumulation.
// The first call to the callbackfn function provides this value as an argument instead of an array value.
values = [200, -200, 340, -300, -20, 50, 400, -460];
const maxValue = values.reduce((maxVal, currElmnt) => {

    console.log(`Start of loop maxVal: ${maxVal}, currElmnt: ${currElmnt}`);
    // Remember that in each iteration we have to somehow return the acc so that it can be used in the next iteration
    if (maxVal < currElmnt) {
        return currElmnt;
    } else {
        return maxVal;
    }
}, values[0]);

console.log(`The max value is: ${maxValue}`);
```
## Coding Challenge #2
Let's go back to Julia and Kate's study about dogs. This time, they want to convert dog ages to human ages and calculate the average age of the dogs in their study.

Create a function 'calcAverageHumanAge', which accepts an arrays of dog's ages ('ages'), and does the following things in order:

    1. Calculate the dog age in human years using the following formula: if the dog is <= 2 years old, humanAge = 2 * dogAge. If the dog is > 2 years old, humanAge = 16 + dogAge * 4.
    2. Exclude all dogs that are less than 18 human years old (which is the same as keeping dogs that are at least 18 years old)
    3. Calculate the average human age of all adult dogs (you should already know from other challenges how we calculate averages 😉)
    4. Run the function for both test datasets
TEST DATA 1: [5, 2, 4, 1, 15, 8, 3] TEST DATA 2: [16, 6, 10, 5, 6, 1, 4]

```js
const calcAverageHumanAge = function (ages) {
  const humanAges = ages.map(age => (age <= 2 ? 2 * age : 16 + age * 4));
  const adults = humanAges.filter(age => age >= 18);
  console.log(humanAges);
  console.log(adults);

  // const average = adults.reduce((acc, age) => acc + age, 0) / adults.length;

  const average = adults.reduce(
    (acc, age, i, arr) => acc + age / arr.length,
    0
  );

  // 2 3. (2+3)/2 = 2.5 === 2/2+3/2 = 2.5

  return average;
};
const avg1 = calcAverageHumanAge([5, 2, 4, 1, 15, 8, 3]);
const avg2 = calcAverageHumanAge([16, 6, 10, 5, 6, 1, 4]);
console.log(avg1, avg2);
```
## The Magic of Chaining Methods
- How do we debug code that is in the pipeline:

```js
// Suppose we have the following requirement:
// filter out all the -ve values
// convert values to usd
// calculate the sum
values = [200, -200, 340, -300, -20, 50, 400, -460];

const finalSum = values.filter(amt => amt > 0)
    .map(amt => amt * 1.2)
    .reduce((sum, amt) => sum + amt, 0);

console.log(finalSum);

// But now if there was an error, how would we debug?
// This is where the use case of passing the original array as an args comes in
// We can rewrite the original function as:
const finalSumDebug = values
    .filter((amt, _, arr) => {
        console.log(`Inside filter the input array is: ${arr}`);
        return amt > 0;
    })
    .map((amt, _, arr) => {
        console.log(`Inside map the input array is: ${arr}`);
        return amt * 1.2
    })
    .reduce((sum, amt, _, arr) => {
        console.log(`Inside reduce the input array is: ${arr}`);
        return sum + amt
    }, 0);

/*
The important point to note here is that on each step of the pipeline,
the array that is being passed into the next stage, is the one that was generated after the previous stage.
In this way, we can keep track of how the arrays are being modified by each step of the pipeline
Inside filter the input array is: 200,-200,340,-300,-20,50,400,-460
Inside filter the input array is: 200,-200,340,-300,-20,50,400,-460
Inside filter the input array is: 200,-200,340,-300,-20,50,400,-460
Inside filter the input array is: 200,-200,340,-300,-20,50,400,-460
Inside filter the input array is: 200,-200,340,-300,-20,50,400,-460
Inside filter the input array is: 200,-200,340,-300,-20,50,400,-460
Inside filter the input array is: 200,-200,340,-300,-20,50,400,-460
Inside filter the input array is: 200,-200,340,-300,-20,50,400,-460
Inside map the input array is: 200,340,50,400
Inside map the input array is: 200,340,50,400
Inside map the input array is: 200,340,50,400
Inside map the input array is: 200,340,50,400
Inside reduce the input array is: 240,408,60,480
Inside reduce the input array is: 240,408,60,480
Inside reduce the input array is: 240,408,60,480
 */
```
## Coding Challenge #3
Rewrite the 'calcAverageHumanAge' function from the previous challenge, but this time as an arrow function, and using chaining!

TEST DATA 1: [5, 2, 4, 1, 15, 8, 3] TEST DATA 2: [16, 6, 10, 5, 6, 1, 4]
```js
const calcAverageHumanAge = ages =>
  ages
    .map(age => (age <= 2 ? 2 * age : 16 + age * 4))
    .filter(age => age >= 18)
    .reduce((acc, age, i, arr) => acc + age / arr.length, 0);
// adults.length

const avg1 = calcAverageHumanAge([5, 2, 4, 1, 15, 8, 3]);
const avg2 = calcAverageHumanAge([16, 6, 10, 5, 6, 1, 4]);
console.log(avg1, avg2);
```
## The Find Method
- The find method returns the element based on the condition that is specified in the callback function. Note that if multiple elements of the array satisfy the given condition, then in that case the find method will return the first element that satisfies the condition.

```js
values = [200, -200, 340, -300, -20, 50, 400, -460];

// Returns the value of the first element in the array where predicate is true, and undefined otherwise.
const firstNegValue = values.find(val => val < 0);
console.log(firstNegValue); // Prints: -200
```
## The findIndex Method
- Returns the index of the first element in the array where predicate is true, and -1 otherwise.
```js
values = [200, -200, 340, -300, -20, 50, 400, -460];
console.log(values.findIndex(val => val === 400)); // Prints: 6
console.log(values.findIndex(val => val < 0)); // Prints: 1
console.log(values.findIndex(val => val > 500)); // Prints: -1
```

## some and every
- `some` Determines whether the specified callback function returns true for any element of an array.
- `every` Determines whether all the members of an array satisfy the specified test.
```js
values = [200, -200, 340, -300, -20, 50, 400, -460];
// We can search whether an element exists or not by using 'includes'
console.log(values.includes(340)); // Prints: true

// some

// The problem with this method is that it only searches for exact matches. We use the 'some' method to search for other conditions
// Suppose we want to check if a particular array contains any positive values or not
console.log(values.some(val => val >= 0)); // Prints: true

// every

// Determines whether all the members of an array satisfy the specified test.
console.log(values.every(amt => amt >= 0)); // Prints: false
values = [200, 340, 50, 400];
console.log(values.every(amt => amt >= 0)); // Prints: true
```
## flat and flatMap
- `flat` Returns a new array with all sub-array elements concatenated into it recursively up to the specified depth.
- `flatMap` Calls a defined callback function on each element of an array. Then, flattens the result into a new array. This is identical to a `map` followed by `flat` with depth.
- The `flatMap` method calls the callback function one time for each element in the array
```js
// Consider the following nested structure of arrays
// Thus flat() allows us to flatten nested arrays into a single array
let arr1 = [[1, 2, 3], [4, 5], [6], 7, 8];
console.log(arr1.flat()); // Prints: [1, 2, 3, 4, 5, 6, 7, 8]

// But suppose we have an even deeper nested structure of arrays
let arr3 = [[1, [2, 3]], [4, 5], [6, [7, 8]], 9];
console.log(arr3.flat()); // Prints: [1, Array(2), 4, 5, 6, Array(2), 9]

// SO now we needed to go one level deeper
// We can pass in an args that controls how deep we can go. Hence this works now:
console.log(arr3.flat(2)); // Prints: [1, 2, 3, 4, 5, 6, 7, 8, 9]

// The default value of the depth parameter is 1.
// Setting a value deeper than the actual nesting has no effect. It still prints the correct value
console.log(arr3.flat(3)); // Prints: [1, 2, 3, 4, 5, 6, 7, 8, 9]

// Consider the following Data
let acct1 = {
    owner: 'Jonas Schmedtmann',
    movements: [200, 450, -400, 3000, -650, -130, 70, 1300],
    interestRate: 1.2, // %
    pin: 1111,
};

let acct2 = {
    owner: 'Jessica Davis',
    movements: [5000, 3400, -150, -790, -3210, -1000, 8500, -30],
    interestRate: 1.5,
    pin: 2222,
};

let acct3 = {
    owner: 'Steven Thomas Williams',
    movements: [200, -200, 340, -300, -20, 50, 400, -460],
    interestRate: 0.7,
    pin: 3333,
};

let acct4 = {
    owner: 'Sarah Smith',
    movements: [430, 1000, 700, 50, 90],
    interestRate: 1,
    pin: 4444,
};

const accts = [acct1, acct3, acct3, acct4];

// Problem statement is -
// we want to calculate the sum of movements for all of the accounts
const totalSum = accts.map(acct => acct.movements)
    .flat()
    .reduce((sum, value) => sum + value, 0);

console.log(totalSum); // Prints: 6130

// As it turns out, using a map() and then flattening the result is a pretty common operation
// To reduce the verbosity, we have another method called flatMap that does both of these operations in a single operation
const flatMap_totalSum = accts
    .flatMap(acct => acct.movements)
    .reduce((sum, value) => sum + value, 0);

console.log(flatMap_totalSum); // Prints: 6130

```
## Sorting Arrays
- Note that the `sort` method by default converts everything to strings implicitly. Hence using the `sort` method to sort arrays of number swill lead to wrong results. Hence be sure to pass in a custom comparator when sorting numbers.
```js
// Sorting Strings
const owners = ['Jonas', 'Zach', 'Adam', 'Martha'];
console.log(owners.sort()); // Prints: ["Adam", "Jonas", "Martha", "Zach"]
// The sort() operation mutates the original array as well
console.log(owners); // Prints: ["Adam", "Jonas", "Martha", "Zach"]

// Sorting Numbers
values = [200, -200, 340, -300, -20, 50, 400, -460];
console.log(values.sort()); // Prints: [-20, -200, -300, -460, 200, 340, 400, 50]
// WHAT HAPPENED?

// Well the sort() function implicitly converts everything to string.

// So how do we sort numbers?
// We pass in a custom comparator

// Sorting in ascending order
values = [200, -200, 340, -300, -20, 50, 400, -460];
values.sort((a, b) => {
    if (a > b) {
        return 1;
    } else if (a < b) {
        return -1;
    } else {
        return 0;
    }
});

// And now the numbers are sorted in a way that makes sense
console.log(values); // Prints: [-460, -300, -200, -20, 50, 200, 340, 400]

// Sorting in descending order
values = [200, -200, 340, -300, -20, 50, 400, -460];
values.sort((a, b) => {
    if (a > b) {
        return -1;
    } else if (a < b) {
        return 1;
    } else {
        return 0;
    }
});
console.log(values); // Prints: [400, 340, 200, 50, -20, -200, -300, -460]

// If we are working with numbers, we can simplify the above operation to just this:
values = [200, -200, 340, -300, -20, 50, 400, -460];

// Ascending
values.sort((a, b) => a - b);
console.log(values); // Prints: [-460, -300, -200, -20, 50, 200, 340, 400]

// Descending
values.sort((a, b) => b - a);
console.log(values); // Prints: [400, 340, 200, 50, -20, -200, -300, -460]
```

## More ways of creating and filling arrays
- Here you go:
```js
// This is how we have been constructing arrays so far
const arr4 = [1, 2, 3, 4, 5, 6, 7];

// Note how we are using the Array() constructor to create array
console.log(new Array(1, 2, 3, 4, 5, 6, 7));

// But now note what happens when you do this:
let x = new Array(7);
// It creates an empty array of size 7 and NOT a array with a single element - 7
console.log(x); // Prints: [empty × 7]

// So the point is that when we pass in a single args to the Array() method, it creates an empty array of the specified length
// instead of creating an array of that element

// But we CAN do something useful with x
// We can use the fill() method to fill the array with elements
x.fill(5);
console.log(x); // Prints: [5, 5, 5, 5, 5, 5, 5]

// We can also specify a begin parameter in the fill() method. Now the array will be filled with 1 starting from the index 3.
x = new Array(7);
x.fill(1, 3);
console.log(x); // Prints: [empty × 3, 1, 1, 1, 1]

// We can also specify a range
x = new Array(7);
x.fill(1, 3, 5);
console.log(x); // Prints: [empty × 3, 1, 1, empty × 2]

// The starting array need not always be empty.
// Also note how we are changing the content of an array declared with const
const y = [1, 2, 3, 4, 5, 6, 7];
y.fill(5, 2, 4);
console.log(y); // Prints: [1, 2, 5, 5, 5, 6, 7]


// Array.from()


// The first args is an object that specifies the length of the array
// The second args is the callback fn that is used to create the array
const arr5 = Array.from({length: 7}, () => 5);
console.log(arr5); // [5, 5, 5, 5, 5, 5, 5]

// In the callback fn we get access to the current element and the current index
// The Array.from() method accepts 2 parameters usually:
// 1) arrayLike – An array-like object to convert to an array.
// 2) mapfn – A mapping function to call on every element of the array
const arr6 = Array.from({length: 7}, (currElmnt, idx) => idx + 1);
console.log(arr6); // Prints: [1, 2, 3, 4, 5, 6, 7]

// There are multiple things that are going on in this example
// 1) using Array.from() for creating an array from the result of querySelectorAll
// 2) document.querySelectorAll returns an 'arrayLike' structure that is first args (as shown above)
// 3) Then we are also passing in a mapping function that is oterating through each item in this arrayLike structure
//    and returning the individual numbers as an array
labelBalance.addEventListener('click', function () {
    const movementsUI = Array.from(
        document.querySelectorAll('.movements__value'),el => Number(el.textContent.replace('€', ''))
    );
    console.log(movementsUI);
    
    // This also creates an array from the document.querySelectorAll(). But then we would have to map() each element separately
    // Hence we prefer the Arrays.from() method
    const movementsUI2 = [...document.querySelectorAll('.movements__value')];
});
```
## Summary: Which Array method to use?
![WhichArrayMethodToUse.png](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/WhichArrayMethodToUse.png)


## Array Methods Practice
```js
///////////////////////////////////////
// Array Methods Practice

// Note the behavior of the ++ operator
let a = 10;
console.log(a++); // Prints: 10
console.log(a); // Prints: 11

a = 10;
console.log(++a); // Prints: 11
console.log(a); // Prints: 11


// Problem Statement: Given an array, calculate separately the sum of +ve and -ve numbers
values = [200, -200, 340, -300, -20, 50, 400, -460];
let {deposit, withdrawal} = values.reduce((sumStore, currElmnt) => {
    if (currElmnt > 0) {
        sumStore.deposit += currElmnt;
        return sumStore;
    } else {
        sumStore.withdrawal += currElmnt;
        return sumStore;
    }
}, {deposit: 0, withdrawal: 0});

console.log(deposit, withdrawal); // Print: 990 -980

// We can rewrite the above fn as follows though:
// We are giving aliases to the names because we have already used these names above
let {deposit : dep, withdrawal : withd} = values.reduce((sumStore, currElmnt) => {
    // Now we are dynamically generating the property name
    sumStore[currElmnt > 0 ? 'deposit' : 'withdrawal'] += currElmnt;
    console.log('Deposit = ', sumStore.deposit);
    console.log('Withdrawal = ', sumStore.withdrawal);
    return sumStore;
}, {deposit: 0, withdrawal: 0});
console.log(dep, withd); // Print: 990 -980

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Lecture 164: Arrays method practice
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

const dogs = [
    { weight: 22, curFood: 250, owners: ['Alice', 'Bob'] },
    { weight: 8, curFood: 200, owners: ['Matilda'] },
    { weight: 13, curFood: 275, owners: ['Sarah', 'John'] },
    { weight: 32, curFood: 340, owners: ['Michael'] }
];

// 1)
dogs.forEach(dog => dog.recommendedFood = dog.weight * 0.75 * 28);
console.log(dogs);

// 2)

const checkFoodConsumptionLevel = function (dog) {
    if (dog?.curFood > (1.1 * dog.recommendedFood)) {
        return `Overeat`;
    } else if (dog?.curFood < (0.9 * dog.recommendedFood)) {
        return `Undereat`;
    } else {
        return(`Recommended Amt of food is being consumed`);
    }
}
console.log(checkFoodConsumptionLevel(dogs.find(dog => dog.owners.includes('Sarah'))));
console.log(`----------`);

// 3)
// Create an array containing all owners of dogs who eat too much ('ownersEatTooMuch')
// and an array with all owners of dogs who eat too little ('ownersEatTooLittle').
// Eating too much means the dog's current food portion is larger than the recommended portion,
// and eating too little is the opposite.
//     Eating an okay amount means the dog's current food portion is
// within a range 10% above and 10% below the recommended portion (see hint).
const {ownersEatTooMuch, ownersEatTooLittle} = dogs.reduce((result, dog) => {
    const level = checkFoodConsumptionLevel(dog);
    if (level === 'Overeat') {
        result.ownersEatTooMuch.push(dog.owners);
        console.log('Overeat');
        return result;
    } else if (level === 'Undereat') {
        result.ownersEatTooLittle.push(dog.owners);
        console.log('Undereat');
        return result;
    } else {
        // NOTE: We have to return a result for EVERY scenario!!
        // Hence this return stmnt should also be there
        return result;
    }
}, {ownersEatTooMuch: [], ownersEatTooLittle: []});

console.log(ownersEatTooMuch); // [["Matilda"]]
console.log(ownersEatTooLittle); // [["Alice", "Bob"], ["Michael"]]

```

## Coding Challenge #4
Julia and Kate are still studying dogs, and this time they are studying if dogs are eating too much or too little. Eating too much means the dog's current food portion is larger than the recommended portion, and eating too little is the opposite. Eating an okay amount means the dog's current food portion is within a range 10% above and 10% below the recommended portion (see hint).
* Loop over the array containing dog objects, and for each dog, calculate the recommended food portion and add it to the object as a new property. Do NOT create a new array, simply loop over the array. Forumla: `recommendedFood = weight ** 0.75 * 28`. (The result is in grams of food, and the weight needs to be in kg)
* Find Sarah's dog and log to the console whether it's eating too much or too little. HINT: Some dogs have multiple owners, so you first need to find Sarah in the owners array, and so this one is a bit tricky (on purpose) 🤓
* Create an array containing all owners of dogs who eat too much ('ownersEatTooMuch') and an array with all owners of dogs who eat too little ('ownersEatTooLittle').
* Log a string to the console for each array created in 3., like this: "Matilda and Alice and Bob's dogs eat too much!" and "Sarah and John and Michael's dogs eat too little!"
* Log to the console whether there is any dog eating EXACTLY the amount of food that is recommended (just true or false)
Log to the console whether there is any dog eating an OKAY amount of food (just true or false)
* Create an array containing the dogs that are eating an OKAY amount of food (try to reuse the condition used in 6.)
* Create a shallow copy of the dogs array and sort it by recommended food portion in an ascending order (keep in mind that the portions are inside the array's objects)
HINT 1: Use many different tools to solve these challenges, you can use the summary lecture to choose between them 😉 HINT 2: Being within a range 10% above and below the recommended portion means: `current > (recommended * 0.90) && current < (recommended * 1.10)`. Basically, the current portion should be between 90% and 110% of the recommended portion.
TEST DATA:
```js
const dogs = [
  { weight: 22, curFood: 250, owners: ['Alice', 'Bob'] },
  { weight: 8, curFood: 200, owners: ['Matilda'] },
  { weight: 13, curFood: 275, owners: ['Sarah', 'John'] },
  { weight: 32, curFood: 340, owners: ['Michael'] }
];
```
```js
const dogs = [
  { weight: 22, curFood: 250, owners: ['Alice', 'Bob'] },
  { weight: 8, curFood: 200, owners: ['Matilda'] },
  { weight: 13, curFood: 275, owners: ['Sarah', 'John'] },
  { weight: 32, curFood: 340, owners: ['Michael'] },
];

// 1.
dogs.forEach(dog => (dog.recFood = Math.trunc(dog.weight ** 0.75 * 28)));

// 2.
const dogSarah = dogs.find(dog => dog.owners.includes('Sarah'));
console.log(dogSarah);
console.log(
  `Sarah's dog is eating too ${
    dogSarah.curFood > dogSarah.recFood ? 'much' : 'little'
  } `
);

// 3.
const ownersEatTooMuch = dogs
  .filter(dog => dog.curFood > dog.recFood)
  .flatMap(dog => dog.owners);
// .flat();
console.log(ownersEatTooMuch);

const ownersEatTooLittle = dogs
  .filter(dog => dog.curFood < dog.recFood)
  .flatMap(dog => dog.owners);
console.log(ownersEatTooLittle);

// 4.
// "Matilda and Alice and Bob's dogs eat too much!"
//  "Sarah and John and Michael's dogs eat too little!"
console.log(`${ownersEatTooMuch.join(' and ')}'s dogs eat too much!`);
console.log(`${ownersEatTooLittle.join(' and ')}'s dogs eat too little!`);

// 5.
console.log(dogs.some(dog => dog.curFood === dog.recFood));

// 6.
// current > (recommended * 0.90) && current < (recommended * 1.10)
const checkEatingOkay = dog =>
  dog.curFood > dog.recFood * 0.9 && dog.curFood < dog.recFood * 1.1;

console.log(dogs.some(checkEatingOkay));

// 7.
console.log(dogs.filter(checkEatingOkay));

// 8.
// sort it by recommended food portion in an ascending order [1,2,3]
const dogsSorted = dogs.slice().sort((a, b) => a.recFood - b.recFood);
console.log(dogsSorted);
```


## The Bankist App
### Project Code
**HTML**
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link rel="shortcut icon" type="image/png" href="/icon.png" />

    <link
      href="https://fonts.googleapis.com/css?family=Poppins:400,500,600&display=swap"
      rel="stylesheet"
    />

    <link rel="stylesheet" href="style.css" />
    <title>Bankist</title>
  </head>
  <body>
    <!-- TOP NAVIGATION -->
    <nav>
      <p class="welcome">Log in to get started</p>
      <img src="logo.png" alt="Logo" class="logo" />
      <form class="login">
        <input
          type="text"
          placeholder="user"
          class="login__input login__input--user"
        />
        <!-- In practice, use type="password" -->
        <input
          type="text"
          placeholder="PIN"
          maxlength="4"
          class="login__input login__input--pin"
        />
        <button class="login__btn">&rarr;</button>
      </form>
    </nav>

    <main class="app">
      <!-- BALANCE -->
      <div class="balance">
        <div>
          <p class="balance__label">Current balance</p>
          <p class="balance__date">
            As of <span class="date">05/03/2037</span>
          </p>
        </div>
        <p class="balance__value">0000€</p>
      </div>

      <!-- MOVEMENTS -->
      <div class="movements">
        <div class="movements__row">
          <div class="movements__type movements__type--deposit">2 deposit</div>
          <div class="movements__date">3 days ago</div>
          <div class="movements__value">4 000€</div>
        </div>
        <div class="movements__row">
          <div class="movements__type movements__type--withdrawal">
            1 withdrawal
          </div>
          <div class="movements__date">24/01/2037</div>
          <div class="movements__value">-378€</div>
        </div>
      </div>

      <!-- SUMMARY -->
      <div class="summary">
        <p class="summary__label">In</p>
        <p class="summary__value summary__value--in">0000€</p>
        <p class="summary__label">Out</p>
        <p class="summary__value summary__value--out">0000€</p>
        <p class="summary__label">Interest</p>
        <p class="summary__value summary__value--interest">0000€</p>
        <button class="btn--sort">&downarrow; SORT</button>
      </div>

      <!-- OPERATION: TRANSFERS -->
      <div class="operation operation--transfer">
        <h2>Transfer money</h2>
        <form class="form form--transfer">
          <input type="text" class="form__input form__input--to" />
          <input type="number" class="form__input form__input--amount" />
          <button class="form__btn form__btn--transfer">&rarr;</button>
          <label class="form__label">Transfer to</label>
          <label class="form__label">Amount</label>
        </form>
      </div>

      <!-- OPERATION: LOAN -->
      <div class="operation operation--loan">
        <h2>Request loan</h2>
        <form class="form form--loan">
          <input type="number" class="form__input form__input--loan-amount" />
          <button class="form__btn form__btn--loan">&rarr;</button>
          <label class="form__label form__label--loan">Amount</label>
        </form>
      </div>

      <!-- OPERATION: CLOSE -->
      <div class="operation operation--close">
        <h2>Close account</h2>
        <form class="form form--close">
          <input type="text" class="form__input form__input--user" />
          <input
            type="password"
            maxlength="6"
            class="form__input form__input--pin"
          />
          <button class="form__btn form__btn--close">&rarr;</button>
          <label class="form__label">Confirm user</label>
          <label class="form__label">Confirm PIN</label>
        </form>
      </div>

      <!-- LOGOUT TIMER -->
      <p class="logout-timer">
        You will be logged out in <span class="timer">05:00</span>
      </p>
    </main>

    <!-- <footer>
      &copy; by Jonas Schmedtmann. Don't claim as your own :)
    </footer> -->

    <script src="script.js"></script>
  </body>
</html>

```
**CSS**

```css
/*
 * Use this CSS to learn some intersting techniques,
 * in case you're wondering how I built the UI.
 * Have fun! 😁
 */

* {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

html {
  font-size: 62.5%;
  box-sizing: border-box;
}

body {
  font-family: 'Poppins', sans-serif;
  color: #444;
  background-color: #f3f3f3;
  height: 100vh;
  padding: 2rem;
}

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
}

.welcome {
  font-size: 1.9rem;
  font-weight: 500;
}

.logo {
  height: 5.25rem;
}

.login {
  display: flex;
}

.login__input {
  border: none;
  padding: 0.5rem 2rem;
  font-size: 1.6rem;
  font-family: inherit;
  text-align: center;
  width: 12rem;
  border-radius: 10rem;
  margin-right: 1rem;
  color: inherit;
  border: 1px solid #fff;
  transition: all 0.3s;
}

.login__input:focus {
  outline: none;
  border: 1px solid #ccc;
}

.login__input::placeholder {
  color: #bbb;
}

.login__btn {
  border: none;
  background: none;
  font-size: 2.2rem;
  color: inherit;
  cursor: pointer;
  transition: all 0.3s;
}

.login__btn:hover,
.login__btn:focus,
.btn--sort:hover,
.btn--sort:focus {
  outline: none;
  color: #777;
}

/* MAIN */
.app {
  position: relative;
  max-width: 100rem;
  margin: 4rem auto;
  display: grid;
  grid-template-columns: 4fr 3fr;
  grid-template-rows: auto repeat(3, 15rem) auto;
  gap: 2rem;

  /* NOTE This creates the fade in/out anumation */
  opacity: 0;
  transition: all 1s;
}

.balance {
  grid-column: 1 / span 2;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  margin-bottom: 2rem;
}

.balance__label {
  font-size: 2.2rem;
  font-weight: 500;
  margin-bottom: -0.2rem;
}

.balance__date {
  font-size: 1.4rem;
  color: #888;
}

.balance__value {
  font-size: 4.5rem;
  font-weight: 400;
}

/* MOVEMENTS */
.movements {
  grid-row: 2 / span 3;
  background-color: #fff;
  border-radius: 1rem;
  overflow: scroll;
}

.movements__row {
  padding: 2.25rem 4rem;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #eee;
}

.movements__type {
  font-size: 1.1rem;
  text-transform: uppercase;
  font-weight: 500;
  color: #fff;
  padding: 0.1rem 1rem;
  border-radius: 10rem;
  margin-right: 2rem;
}

.movements__date {
  font-size: 1.1rem;
  text-transform: uppercase;
  font-weight: 500;
  color: #666;
}

.movements__type--deposit {
  background-image: linear-gradient(to top left, #39b385, #9be15d);
}

.movements__type--withdrawal {
  background-image: linear-gradient(to top left, #e52a5a, #ff585f);
}

.movements__value {
  font-size: 1.7rem;
  margin-left: auto;
}

/* SUMMARY */
.summary {
  grid-row: 5 / 6;
  display: flex;
  align-items: baseline;
  padding: 0 0.3rem;
  margin-top: 1rem;
}

.summary__label {
  font-size: 1.2rem;
  font-weight: 500;
  text-transform: uppercase;
  margin-right: 0.8rem;
}

.summary__value {
  font-size: 2.2rem;
  margin-right: 2.5rem;
}

.summary__value--in,
.summary__value--interest {
  color: #66c873;
}

.summary__value--out {
  color: #f5465d;
}

.btn--sort {
  margin-left: auto;
  border: none;
  background: none;
  font-size: 1.3rem;
  font-weight: 500;
  cursor: pointer;
}

/* OPERATIONS */
.operation {
  border-radius: 1rem;
  padding: 3rem 4rem;
  color: #333;
}

.operation--transfer {
  background-image: linear-gradient(to top left, #ffb003, #ffcb03);
}

.operation--loan {
  background-image: linear-gradient(to top left, #39b385, #9be15d);
}

.operation--close {
  background-image: linear-gradient(to top left, #e52a5a, #ff585f);
}

h2 {
  margin-bottom: 1.5rem;
  font-size: 1.7rem;
  font-weight: 600;
  color: #333;
}

.form {
  display: grid;
  grid-template-columns: 2.5fr 2.5fr 1fr;
  grid-template-rows: auto auto;
  gap: 0.4rem 1rem;
}

/* Exceptions for interst */
.form.form--loan {
  grid-template-columns: 2.5fr 1fr 2.5fr;
}
.form__label--loan {
  grid-row: 2;
}
/* End exceptions */

.form__input {
  width: 100%;
  border: none;
  background-color: rgba(255, 255, 255, 0.4);
  font-family: inherit;
  font-size: 1.5rem;
  text-align: center;
  color: #333;
  padding: 0.3rem 1rem;
  border-radius: 0.7rem;
  transition: all 0.3s;
}

.form__input:focus {
  outline: none;
  background-color: rgba(255, 255, 255, 0.6);
}

.form__label {
  font-size: 1.3rem;
  text-align: center;
}

.form__btn {
  border: none;
  border-radius: 0.7rem;
  font-size: 1.8rem;
  background-color: #fff;
  cursor: pointer;
  transition: all 0.3s;
}

.form__btn:focus {
  outline: none;
  background-color: rgba(255, 255, 255, 0.8);
}

.logout-timer {
  padding: 0 0.3rem;
  margin-top: 1.9rem;
  text-align: right;
  font-size: 1.25rem;
}

.timer {
  font-weight: 600;
}

```
**JavaScript**
```js
'use strict';

/////////////////////////////////////////////////
/////////////////////////////////////////////////
// BANKIST APP

/////////////////////////////////////////////////
// Data
const account1 = {
  owner: 'Jonas Schmedtmann',
  movements: [200, 450, -400, 3000, -650, -130, 70, 1300],
  interestRate: 1.2, // %
  pin: 1111,
};

const account2 = {
  owner: 'Jessica Davis',
  movements: [5000, 3400, -150, -790, -3210, -1000, 8500, -30],
  interestRate: 1.5,
  pin: 2222,
};

const account3 = {
  owner: 'Steven Thomas Williams',
  movements: [200, -200, 340, -300, -20, 50, 400, -460],
  interestRate: 0.7,
  pin: 3333,
};

const account4 = {
  owner: 'Sarah Smith',
  movements: [430, 1000, 700, 50, 90],
  interestRate: 1,
  pin: 4444,
};

const accounts = [account1, account2, account3, account4];

/////////////////////////////////////////////////
// Elements
const labelWelcome = document.querySelector('.welcome');
const labelDate = document.querySelector('.date');
const labelBalance = document.querySelector('.balance__value');
const labelSumIn = document.querySelector('.summary__value--in');
const labelSumOut = document.querySelector('.summary__value--out');
const labelSumInterest = document.querySelector('.summary__value--interest');
const labelTimer = document.querySelector('.timer');

const containerApp = document.querySelector('.app');
const containerMovements = document.querySelector('.movements');

const btnLogin = document.querySelector('.login__btn');
const btnTransfer = document.querySelector('.form__btn--transfer');
const btnLoan = document.querySelector('.form__btn--loan');
const btnClose = document.querySelector('.form__btn--close');
const btnSort = document.querySelector('.btn--sort');

const inputLoginUsername = document.querySelector('.login__input--user');
const inputLoginPin = document.querySelector('.login__input--pin');
const inputTransferTo = document.querySelector('.form__input--to');
const inputTransferAmount = document.querySelector('.form__input--amount');
const inputLoanAmount = document.querySelector('.form__input--loan-amount');
const inputCloseUsername = document.querySelector('.form__input--user');
const inputClosePin = document.querySelector('.form__input--pin');

/////////////////////////////////////////////////
// Functions

const displayMovements = function (movements, sort = false) {
  containerMovements.innerHTML = '';

  const movs = sort ? movements.slice().sort((a, b) => a - b) : movements;

  movs.forEach(function (mov, i) {
    const type = mov > 0 ? 'deposit' : 'withdrawal';

    const html = `
      <div class="movements__row">
        <div class="movements__type movements__type--${type}">${
      i + 1
    } ${type}</div>
        <div class="movements__value">${mov}€</div>
      </div>
    `;

    containerMovements.insertAdjacentHTML('afterbegin', html);
  });
};

const calcDisplayBalance = function (acc) {
  acc.balance = acc.movements.reduce((acc, mov) => acc + mov, 0);
  labelBalance.textContent = `${acc.balance}€`;
};

const calcDisplaySummary = function (acc) {
  const incomes = acc.movements
    .filter(mov => mov > 0)
    .reduce((acc, mov) => acc + mov, 0);
  labelSumIn.textContent = `${incomes}€`;

  const out = acc.movements
    .filter(mov => mov < 0)
    .reduce((acc, mov) => acc + mov, 0);
  labelSumOut.textContent = `${Math.abs(out)}€`;

  const interest = acc.movements
    .filter(mov => mov > 0)
    .map(deposit => (deposit * acc.interestRate) / 100)
    .filter((int, i, arr) => {
      // console.log(arr);
      return int >= 1;
    })
    .reduce((acc, int) => acc + int, 0);
  labelSumInterest.textContent = `${interest}€`;
};

const createUsernames = function (accs) {
  accs.forEach(function (acc) {
    acc.username = acc.owner
      .toLowerCase()
      .split(' ')
      .map(name => name[0])
      .join('');
  });
};
createUsernames(accounts);

const updateUI = function (acc) {
  // Display movements
  displayMovements(acc.movements);

  // Display balance
  calcDisplayBalance(acc);

  // Display summary
  calcDisplaySummary(acc);
};

///////////////////////////////////////
// Event handlers
let currentAccount;

btnLogin.addEventListener('click', function (e) {
  // Prevent form from submitting
  e.preventDefault();

  currentAccount = accounts.find(
    acc => acc.username === inputLoginUsername.value
  );
  console.log(currentAccount);

  if (currentAccount?.pin === Number(inputLoginPin.value)) {
    // Display UI and message
    labelWelcome.textContent = `Welcome back, ${
      currentAccount.owner.split(' ')[0]
    }`;
    containerApp.style.opacity = 100;

    // Clear input fields
    inputLoginUsername.value = inputLoginPin.value = '';
    inputLoginPin.blur();

    // Update UI
    updateUI(currentAccount);
  }
});

btnTransfer.addEventListener('click', function (e) {
  e.preventDefault();
  const amount = Number(inputTransferAmount.value);
  const receiverAcc = accounts.find(
    acc => acc.username === inputTransferTo.value
  );
  inputTransferAmount.value = inputTransferTo.value = '';

  if (
    amount > 0 &&
    receiverAcc &&
    currentAccount.balance >= amount &&
    receiverAcc?.username !== currentAccount.username
  ) {
    // Doing the transfer
    currentAccount.movements.push(-amount);
    receiverAcc.movements.push(amount);

    // Update UI
    updateUI(currentAccount);
  }
});

btnLoan.addEventListener('click', function (e) {
  e.preventDefault();

  const amount = Number(inputLoanAmount.value);

  if (amount > 0 && currentAccount.movements.some(mov => mov >= amount * 0.1)) {
    // Add movement
    currentAccount.movements.push(amount);

    // Update UI
    updateUI(currentAccount);
  }
  inputLoanAmount.value = '';
});

btnClose.addEventListener('click', function (e) {
  e.preventDefault();

  if (
    inputCloseUsername.value === currentAccount.username &&
    Number(inputClosePin.value) === currentAccount.pin
  ) {
    const index = accounts.findIndex(
      acc => acc.username === currentAccount.username
    );
    console.log(index);
    // .indexOf(23)

    // Delete account
    accounts.splice(index, 1);

    // Hide UI
    containerApp.style.opacity = 0;
  }

  inputCloseUsername.value = inputClosePin.value = '';
});

let sorted = false;
btnSort.addEventListener('click', function (e) {
  e.preventDefault();
  displayMovements(currentAccount.movements, !sorted);
  sorted = !sorted;
});
```
[BACK ⬅️](https://github.com/subhadeeppaul/JavaScript-Notes)
