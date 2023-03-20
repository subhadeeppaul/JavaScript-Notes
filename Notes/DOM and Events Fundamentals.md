
# JavaScript in the Browser - DOM and Events Fundamentals

## PROJECT ##1: Guess My Number!
```js
'use strict';

document.querySelector('.message');
console.log(document.querySelector('.message').textContent);
```
- (.) notation for classes
- (##) for selecting ids
- .textContent to select the text.

## What's the DOM and DOM Manipulation
DOM - Document Object Model: Structured Representation of Html Documents. Allows Javascript to Access Html Elements and Styles to Manipulate Them. Dom Changes text, HTML attributes, and even CSS styles.

## The DOM Tree Structure 
Link-Image

## DOM !== Javascript
Link-Image

## Selecting and Manipulating Elements

```js
console.log(document.querySelector('.message').textContent);
document.querySelector('.message').textContent = '🎉 Correct Number!';

document.querySelector('.number').textContent = 13;
document.querySelector('.score').textContent = 10;

document.querySelector('.guess').value = 23; // we use ".value" to read from the input field.
console.log(document.querySelector('.guess').value);
```

## Handling Click Events

- **Event Listener -** Now, an event is something that happens on the page. For example, a mouse click, or a mouse moving, or a key press,
- And if a function is just is value, then we can also pass it into another function as an argument.

```js
document.querySelector('.message');
console.log(document.querySelector('.message').textContent);

document.querySelector('.check').addEventListener('click', function () {
  const guess = console.log(document.querySelector('.guess').value);
  console.log(guess, typeof guess);

  if (!guess) {
    document.querySelector('.message').textContent = '🚫 No Number!';
  }
});
```

- whenever we get the user value it's in string format
- So we selected this button here using querySelector.
- And then we use the addEventListener method on that element to attach an event handler.
- And that event handler is this function here.


## Implementing the Game Logic

```js
const secretNumber = Math.trunc(Math.random() * 20) + 1;
let score = 20;

document.querySelector('.message');
console.log(document.querySelector('.message').textContent);

document.querySelector('.check').addEventListener('click', function () {
  const guess = Number(document.querySelector('.guess').value);
  console.log(guess, typeof guess);

// When there is no input
  if (!guess) {
    document.querySelector('.message').textContent = '🚫 No Number!';
  } else if (guess === secretNumber) { // When player wins
    document.querySelector('.message').textContent = '🎉 Correct Number!';
  } else if (guess > secretNumber) { // When guess is too high
    if (score > 1) {
      document.querySelector('.message').textContent = '📈 Too high!';
      score--;
      document.querySelector('.score').textContent = score;
    } else {
      document.querySelector('.message').textContent = '💥 You lost the game!';
      document.querySelector('.score').textContent = 0;
    }
    // When guess is too low
  } else if (guess < secretNumber) {
    if (score > 1) {
      document.querySelector('.message').textContent = '📉 Too low!';
      score--;
      document.querySelector('.score').textContent = score;
    } else {
      document.querySelector('.message').textContent = '💥 You lost the game!';
      document.querySelector('.score').textContent = 0;
    }
  }
});
```
- And so it's always good to keep a variable which actually holds the data in our code and not just rely on the DOM to hold our data. And the variable can also be called a state variable Because this score is part of the so-called application state which is basically all the data that is relevant to the application.

## Manipulating CSS Styles
link -something

## Coding Challenge ##1

```js
'use strict';

let secretNumber = Math.trunc(Math.random() * 20) + 1;
let score = 20;
let highScore = 0;
console.log(secretNumber);
document.querySelector('.message');
console.log(document.querySelector('.message').textContent);

document.querySelector('.check').addEventListener('click', function () {
  const guess = Number(document.querySelector('.guess').value);
  console.log(guess, typeof guess);

  // When there is no input
  if (!guess) {
    document.querySelector('.message').textContent = '🚫 No Number!';
  } else if (guess === secretNumber) {
    // When player wins
    document.querySelector('.message').textContent = '🎉 Correct Number!';
    document.querySelector('.number').textContent = secretNumber;
    document.querySelector('body').style.backgroundColor = '##60b347';
    document.querySelector('.number').style.width = '30rem';
    if (score > highScore) {
      highScore = score;
    }
  } else if (guess > secretNumber) {
    // When guess is too high
    if (score > 1) {
      document.querySelector('.message').textContent = '📈 Too high!';
      score--;
      document.querySelector('.score').textContent = score;
    } else {
      document.querySelector('.message').textContent = '💥 You lost the game!';
      document.querySelector('.score').textContent = 0;
    }
    // When guess is too low
  } else if (guess < secretNumber) {
    if (score > 1) {
      document.querySelector('.message').textContent = '📉 Too low!';
      score--;
      document.querySelector('.score').textContent = score;
    } else {
      document.querySelector('.message').textContent = '💥 You lost the game!';
      document.querySelector('.score').textContent = 0;
    }
  }
});

document.querySelector('.again').addEventListener('click', function () {
  document.querySelector('.message').textContent = 'Start Guessing';
  document.querySelector('body').style.backgroundColor = '##222';
  document.querySelector('.number').style.width = '15rem';
  secretNumber = Math.trunc(Math.random() * 20) + 1;
  score = 20;
  document.querySelector('.score').textContent = score;
  document.querySelector('.number').textContent = '?';
  document.querySelector('.guess').value = '';
  document.querySelector('.highscore').textContent = highScore;
});
```

## Implementing High scores
```js
if (score > highScore) {
      highScore = score;
    }
    
document.querySelector('.highscore').textContent = highScore;
```



## Refactoring Our Code: The DRY Principle

```js
'use strict';
let secretNumber = Math.trunc(Math.random() * 20) + 1;
let score = 20;
let highscore = 0;

const displayMessage = function (message) {
  document.querySelector('.message').textContent = message;
};

document.querySelector('.check').addEventListener('click', function () {
  const guess = Number(document.querySelector('.guess').value);
  console.log(guess, typeof guess);

  // When there is no input
  if (!guess) {
    // document.querySelector('.message').textContent = '⛔️ No number!';
    displayMessage('⛔️ No number!');

    // When player wins
  } else if (guess === secretNumber) {
    // document.querySelector('.message').textContent = '🎉 Correct Number!';
    displayMessage('🎉 Correct Number!');
    document.querySelector('.number').textContent = secretNumber;

    document.querySelector('body').style.backgroundColor = '##60b347';
    document.querySelector('.number').style.width = '30rem';

    if (score > highscore) {
      highscore = score;
      document.querySelector('.highscore').textContent = highscore;
    }

    // When guess is wrong
  } else if (guess !== secretNumber) {
    if (score > 1) {
      // document.querySelector('.message').textContent =
      // guess > secretNumber ? '📈 Too high!' : '📉 Too low!';
      displayMessage(guess > secretNumber ? '📈 Too high!' : '📉 Too low!');
      score--;
      document.querySelector('.score').textContent = score;
    } else {
      // document.querySelector('.message').textContent = '💥 You lost the game!';
      displayMessage('💥 You lost the game!');
      document.querySelector('.score').textContent = 0;
    }
  }
});

document.querySelector('.again').addEventListener('click', function () {
  score = 20;
  secretNumber = Math.trunc(Math.random() * 20) + 1;

  // document.querySelector('.message').textContent = 'Start guessing...';
  displayMessage('Start guessing...');
  document.querySelector('.score').textContent = score;
  document.querySelector('.number').textContent = '?';
  document.querySelector('.guess').value = '';

  document.querySelector('body').style.backgroundColor = '##222';
  document.querySelector('.number').style.width = '15rem';
});
```

### Guess the Number - HTML

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link rel="stylesheet" href="style.css" />
    <title>Guess My Number!</title>
  </head>
  <body>
    <header>
      <h1>Guess My Number!</h1>
      <p class="between">(Between 1 and 20)</p>
      <button class="btn again">Again!</button>
      <div class="number">?</div>
    </header>
    <main>
      <section class="left">
        <input type="number" class="guess" />
        <button class="btn check">Check!</button>
      </section>
      <section class="right">
        <p class="message">Start guessing...</p>
        <p class="label-score">💯 Score: <span class="score">20</span></p>
        <p class="label-highscore">
          🥇 Highscore: <span class="highscore">0</span>
        </p>
      </section>
    </main>
    <script src="script.js"></script>
  </body>
</html>
```

### Guess the Number - CSS
```css
@import url('https://fonts.googleapis.com/css?family=Press+Start+2P&display=swap');

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
  font-family: 'Press Start 2P', sans-serif;
  color: ##eee;
  background-color: ##222;
  /* background-color: ##60b347; */
}

/* LAYOUT */
header {
  position: relative;
  height: 35vh;
  border-bottom: 7px solid ##eee;
}

main {
  height: 65vh;
  color: ##eee;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.left {
  width: 52rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.right {
  width: 52rem;
  font-size: 2rem;
}

/* ELEMENTS STYLE */
h1 {
  font-size: 4rem;
  text-align: center;
  position: absolute;
  width: 100%;
  top: 52%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.number {
  background: ##eee;
  color: ##333;
  font-size: 6rem;
  width: 15rem;
  padding: 3rem 0rem;
  text-align: center;
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translate(-50%, 50%);
}

.between {
  font-size: 1.4rem;
  position: absolute;
  top: 2rem;
  right: 2rem;
}

.again {
  position: absolute;
  top: 2rem;
  left: 2rem;
}

.guess {
  background: none;
  border: 4px solid ##eee;
  font-family: inherit;
  color: inherit;
  font-size: 5rem;
  padding: 2.5rem;
  width: 25rem;
  text-align: center;
  display: block;
  margin-bottom: 3rem;
}

.btn {
  border: none;
  background-color: ##eee;
  color: ##222;
  font-size: 2rem;
  font-family: inherit;
  padding: 2rem 3rem;
  cursor: pointer;
}

.btn:hover {
  background-color: ##ccc;
}

.message {
  margin-bottom: 8rem;
  height: 3rem;
}

.label-score {
  margin-bottom: 2rem;
}
```

## PROJECT ##2: Modal Window

```js
'use strict';

const modal = document.querySelector('.modal');
const overlay = document.querySelector('.overlay');
const btnCloseModal = document.querySelector('.close-modal');
const btnsOpenModal = document.querySelectorAll('.show-modal');
```

## Working With Classes
```js
const openmodal = function () {
  console.log('Button clicked');
  modal.classList.remove('hidden');
  overlay.classList.remove('hidden');
};

for (let i = 0; i < btnsOpenModal.length; i++)
  btnsOpenModal[i].addEventListener('click', openmodal);

const CloseModal = function () {
  modal.classList.add('hidden');
  overlay.classList.add('hidden');
};

btnCloseModal.addEventListener('click', CloseModal);

overlay.addEventListener('click', CloseModal);
```
- in order to change the appearance of elements on our page.
- classes allow us to basically aggregate multiple CSS properties in just one, like a container.s o each class functions a bit like a container with a lot of properties in it.
- And then here, by adding and removing them, we basically can activate and deactivate certain styles, all at the same time.

## Handling an "Esc" Keypress Event
Now, keyboard events are so-called global events because they do not happen on one specific element. And for global events like keyboard events we usually list and on the whole document.
```js
document.addEventListener('keydown', function (e) {
  //   console.log(e);
  if (e.key === 'Escape' && !modal.classList.contains('hideen')) {
    CloseModal();
  }
});
```



 

## PROJECT ##3: Pig Game

```js
'use strict';

// Selecting elements
const score0El = document.querySelector('##score--0');
const score1El = document.getElementById('score--0');
const diceEl = document.querySelector('.dice');

score0El.textContent = 0;
score1El.textContent = 0;
diceEl.classList.add('hidden');
```

## Rolling the Dice
```js
'use strict';

// Selecting elements
const score0El = document.querySelector('##score--0');
const score1El = document.getElementById('score--1');

const current0El = document.getElementById('current--0');
const current1El = document.getElementById('current--1');

const diceEl = document.querySelector('.dice');
const btnNew = document.querySelector('.btn--new');
const btnRoll = document.querySelector('.btn--roll');
const btnHold = document.querySelector('.btn--hold');

// Starting Conditions
score0El.textContent = 0;
score1El.textContent = 0;
diceEl.classList.add('hidden');

const scores = [0, 0];
let currScore = 0;
let activePlayer = 0; // 0 - Player 1 & 1 -Player 1

btnRoll.addEventListener('click', function () {
  //1. Generate a random dice roll
  const dice = Math.trunc(Math.random() * 6) + 1;
  console.log(dice);
  //2. Diplay dice
  diceEl.classList.remove('hidden');
  diceEl.src = `dice-${dice}.png`;
  console.log(diceEl.src);

  //3.check for rolled 1
  if (dice !== 1) {
    currScore += dice;
    document.getElementById(`current--${activePlayer}`).textContent = currScore;
  } else {
    // switch to next player
     }
});
```

## Switching the Active Player
```js
const player0El = document.querySelector('.player--0');
const player1El = document.querySelector('.player--1');

btnRoll.addEventListener('click', function () {
  //1. Generate a random dice roll
  const dice = Math.trunc(Math.random() * 6) + 1;
  //2. Diplay dice
  diceEl.classList.remove('hidden');
  diceEl.src = `dice-${dice}.png`;

  //3.check for rolled 1
  if (dice !== 1) {
    currScore += dice;
    document.getElementById(`current--${activePlayer}`).textContent = currScore;
  } else {
    // switch to next player
    document.getElementById(`current--${activePlayer}`).textContent = 0;
    currScore = 0;
    activePlayer = activePlayer === 0 ? 1 : 0;
    player0El.classList.toggle('player--active'); // Toggle will act as on off switch
    player1El.classList.toggle('player--active');
  }
});
```

## Holding Current Score
```js
'use strict';

// Selecting elements

const player0El = document.querySelector('.player--0');
const player1El = document.querySelector('.player--1');

const score0El = document.querySelector('##score--0');
const score1El = document.getElementById('score--1');

const current0El = document.getElementById('current--0');
const current1El = document.getElementById('current--1');

const diceEl = document.querySelector('.dice');
const btnNew = document.querySelector('.btn--new');
const btnRoll = document.querySelector('.btn--roll');
const btnHold = document.querySelector('.btn--hold');

// Starting Conditions
score0El.textContent = 0;
score1El.textContent = 0;
diceEl.classList.add('hidden');

let scores = [0, 0];
let currScore = 0;
let activePlayer = 0; // 0 - Player 1 & 1 -Player 1
let playing = true;

const switchPlayer = function () {
  document.getElementById(`current--${activePlayer}`).textContent = 0;
  currScore = 0;
  activePlayer = activePlayer === 0 ? 1 : 0;
  player0El.classList.toggle('player--active');
  player1El.classList.toggle('player--active');
};

btnRoll.addEventListener('click', function () {
  if (playing) {
    //1. Generate a random dice roll
    const dice = Math.trunc(Math.random() * 6) + 1;
    //2. Diplay dice
    diceEl.classList.remove('hidden');
    diceEl.src = `dice-${dice}.png`;

    //3.check for rolled 1
    if (dice !== 1) {
      currScore += dice;
      document.getElementById(`current--${activePlayer}`).textContent =
        currScore;
    } else {
      // switch to next player
      switchPlayer();
    }
  }
});

btnHold.addEventListener('click', function () {
  if (playing) {
    scores[activePlayer] += currScore;
    document.getElementById(`score--${activePlayer}`).textContent =
      scores[activePlayer];
    // Switching Player
    if (scores[activePlayer] >= 10) {
      playing = false;
      diceEl.classList.add('hidden');
      document
        .querySelector(`.player--${activePlayer}`)
        .classList.add('player--winner');
      document
        .querySelector(`.player--${activePlayer}`)
        .classList.add('player--active');
    } else {
      switchPlayer();
    }
  }
});
```

## Resetting the Game
```js
const init = function () {
  scores = [0, 0];
  currentScore = 0;
  activePlayer = 0;
  playing = true;

  score0El.textContent = 0;
  score1El.textContent = 0;
  current0El.textContent = 0;
  current1El.textContent = 0;

  diceEl.classList.add('hidden');
  player0El.classList.remove('player--winner');
  player1El.classList.remove('player--winner');
  player0El.classList.add('player--active');
  player1El.classList.remove('player--active');
};

btnNew.addEventListener('click', init);
```

### Complete Code
***HTML***
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link rel="stylesheet" href="style.css" />
    <title>Pig Game</title>
  </head>
  <body>
    <main>
      <section class="player player--0 player--active">
        <h2 class="name" id="name--0">Player 1</h2>
        <p class="score" id="score--0">43</p>
        <div class="current">
          <p class="current-label">Current</p>
          <p class="current-score" id="current--0">0</p>
        </div>
      </section>
      <section class="player player--1">
        <h2 class="name" id="name--1">Player 2</h2>
        <p class="score" id="score--1">24</p>
        <div class="current">
          <p class="current-label">Current</p>
          <p class="current-score" id="current--1">0</p>
        </div>
      </section>

      <img src="dice-5.png" alt="Playing dice" class="dice" />
      <button class="btn btn--new">🔄 New game</button>
      <button class="btn btn--roll">🎲 Roll dice</button>
      <button class="btn btn--hold">📥 Hold</button>
    </main>
    <script src="script.js"></script>
  </body>
</html>
```

***CSS***
```CSS
@import url('https://fonts.googleapis.com/css2?family=Nunito&display=swap');

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
  font-family: 'Nunito', sans-serif;
  font-weight: 400;
  height: 100vh;
  color: ##333;
  background-image: linear-gradient(to top left, ##753682 0%, ##bf2e34 100%);
  display: flex;
  align-items: center;
  justify-content: center;
}

/* LAYOUT */
main {
  position: relative;
  width: 100rem;
  height: 60rem;
  background-color: rgba(255, 255, 255, 0.35);
  backdrop-filter: blur(200px);
  filter: blur();
  box-shadow: 0 3rem 5rem rgba(0, 0, 0, 0.25);
  border-radius: 9px;
  overflow: hidden;
  display: flex;
}

.player {
  flex: 50%;
  padding: 9rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: all 0.75s;
}

/* ELEMENTS */
.name {
  position: relative;
  font-size: 4rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  word-spacing: 2px;
  font-weight: 300;
  margin-bottom: 1rem;
}

.score {
  font-size: 8rem;
  font-weight: 300;
  color: ##c7365f;
  margin-bottom: auto;
}

.player--active {
  background-color: rgba(255, 255, 255, 0.4);
}
.player--active .name {
  font-weight: 700;
}
.player--active .score {
  font-weight: 400;
}

.player--active .current {
  opacity: 1;
}

.current {
  background-color: ##c7365f;
  opacity: 0.8;
  border-radius: 9px;
  color: ##fff;
  width: 65%;
  padding: 2rem;
  text-align: center;
  transition: all 0.75s;
}

.current-label {
  text-transform: uppercase;
  margin-bottom: 1rem;
  font-size: 1.7rem;
  color: ##ddd;
}

.current-score {
  font-size: 3.5rem;
}

/* ABSOLUTE POSITIONED ELEMENTS */
.btn {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  color: ##444;
  background: none;
  border: none;
  font-family: inherit;
  font-size: 1.8rem;
  text-transform: uppercase;
  cursor: pointer;
  font-weight: 400;
  transition: all 0.2s;

  background-color: white;
  background-color: rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(10px);

  padding: 0.7rem 2.5rem;
  border-radius: 50rem;
  box-shadow: 0 1.75rem 3.5rem rgba(0, 0, 0, 0.1);
}

.btn::first-letter {
  font-size: 2.4rem;
  display: inline-block;
  margin-right: 0.7rem;
}

.btn--new {
  top: 4rem;
}
.btn--roll {
  top: 39.3rem;
}
.btn--hold {
  top: 46.1rem;
}

.btn:active {
  transform: translate(-50%, 3px);
  box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.15);
}

.btn:focus {
  outline: none;
}

.dice {
  position: absolute;
  left: 50%;
  top: 16.5rem;
  transform: translateX(-50%);
  height: 10rem;
  box-shadow: 0 2rem 5rem rgba(0, 0, 0, 0.2);
}

.player--winner {
  background-color: ##2f2f2f;
}

.player--winner .name {
  font-weight: 700;
  color: ##c7365f;
}

.hidden {
  display: none;
}
```

***JavaScript***
```js
'use strict';

// Selecting elements
const player0El = document.querySelector('.player--0');
const player1El = document.querySelector('.player--1');
const score0El = document.querySelector('##score--0');
const score1El = document.getElementById('score--1');
const current0El = document.getElementById('current--0');
const current1El = document.getElementById('current--1');

const diceEl = document.querySelector('.dice');
const btnNew = document.querySelector('.btn--new');
const btnRoll = document.querySelector('.btn--roll');
const btnHold = document.querySelector('.btn--hold');

let scores, currentScore, activePlayer, playing;

// Starting conditions
const init = function () {
  scores = [0, 0];
  currentScore = 0;
  activePlayer = 0;
  playing = true;

  score0El.textContent = 0;
  score1El.textContent = 0;
  current0El.textContent = 0;
  current1El.textContent = 0;

  diceEl.classList.add('hidden');
  player0El.classList.remove('player--winner');
  player1El.classList.remove('player--winner');
  player0El.classList.add('player--active');
  player1El.classList.remove('player--active');
};
init();

const switchPlayer = function () {
  document.getElementById(`current--${activePlayer}`).textContent = 0;
  currentScore = 0;
  activePlayer = activePlayer === 0 ? 1 : 0;
  player0El.classList.toggle('player--active');
  player1El.classList.toggle('player--active');
};

// Rolling dice functionality
btnRoll.addEventListener('click', function () {
  if (playing) {
    // 1. Generating a random dice roll
    const dice = Math.trunc(Math.random() * 6) + 1;

    // 2. Display dice
    diceEl.classList.remove('hidden');
    diceEl.src = `dice-${dice}.png`;

    // 3. Check for rolled 1
    if (dice !== 1) {
      // Add dice to current score
      currentScore += dice;
      document.getElementById(`current--${activePlayer}`).textContent =
        currentScore;
    } else {
      // Switch to next player
      switchPlayer();
    }
  }
});

btnHold.addEventListener('click', function () {
  if (playing) {
    // 1. Add current score to active player's score
    scores[activePlayer] += currentScore;
    // scores[1] = scores[1] + currentScore

    document.getElementById(`score--${activePlayer}`).textContent =
      scores[activePlayer];

    // 2. Check if player's score is >= 100
    if (scores[activePlayer] >= 100) {
      // Finish the game
      playing = false;
      diceEl.classList.add('hidden');

      document
        .querySelector(`.player--${activePlayer}`)
        .classList.add('player--winner');
      document
        .querySelector(`.player--${activePlayer}`)
        .classList.remove('player--active');
    } else {
      // Switch to the next player
      switchPlayer();
    }
  }
});

btnNew.addEventListener('click', init);
```
