# Whack-a-Mole Game

This project is a simple "Whack-a-Mole" game implemented using HTML, CSS, and JavaScript. The game involves clicking on moles that appear randomly in different holes to earn points within a set time limit.

## Table of Contents
- [Explanation of the Code](#explanation-of-the-code)
  - [HTML Structure](#html-structure)
  - [Each Hole](#each-hole)
  - [CSS Styling](#css-styling)
  - [JavaScript Functionality](#javascript-functionality)
    - [Variables](#variables)
    - [DOM References](#dom-references)
    - [Event Listeners](#event-listeners)
    - [`startGame()` Function](#startgame-function)
    - [`randomHole()` Function](#randomhole-function)
    - [`whack()` Function](#whack-function)
    - [`endGame()` Function](#endgame-function)
- [Additional Helpful Notes](#additional-helpful-notes)
  - [Game Duration Control](#game-duration-control)
  - [Timers and Intervals](#timers-and-intervals)
  - [Event Handling](#event-handling)
  - [Random Selection](#random-selection)
  - [Game State Management](#game-state-management)
  - [User Experience](#user-experience)
- [Tips for Understanding and Modifying the Code](#tips-for-understanding-and-modifying-the-code)
  - [Adjusting Game Difficulty](#adjusting-game-difficulty)
  - [Enhancing the Game](#enhancing-the-game)
  - [Debugging](#debugging)
  - [Understanding the Flow](#understanding-the-flow)
- [Clarifications on Specific Code Segments](#clarifications-on-specific-code-segments)
  - [Why Use `setTimeout(endGame, endGameTime * 1000);`](#why-use-settimeoutendgame-endgametime--1000)
  - [Why Not Call `endGame()` in the Countdown Timer](#why-not-call-endgame-in-the-countdown-timer)
  - [Why Remove Event Listeners with `mole.removeEventListener('click', whack);`](#why-remove-event-listeners-with-moleremoveeventlistenerclick-whack)
  - [Why Check `if (currentHole)` Before Hiding the Mole](#why-check-if-currenthole-before-hiding-the-mole)
  - [Why Set `moleVisible` to `false` After Whacking the Mole](#why-set-molevisible-to-false-after-whacking-the-mole)


## Explanation of the Code:
### HTML Structure:
- `<div id="scoreBoard">Score: 0</div>`: Displays the player's current score.
- `<div id="timer">Time Left: 0s</div>`: Shows the remaining time in seconds.
- `<button id="startButton">Start Game</button>`: Button to start the game.
- `<div class="grid">`: Container for the game grid, which holds the holes and moles.
###	Each Hole:
- `<div class="hole" id="hole1">`: Represents a hole where the mole can appear.
- `<div class="mole"></div>`: The mole element that can be shown or hidden.
### CSS Styling:
- **Grid Layout**: Uses CSS Grid to layout the holes in a 3-column grid.
- **Hole Styling**: Each hole is styled to look like a placeholder for the mole.
- **Mole Styling**: The mole is a brown circle that can be hidden or shown.
- **Hover Effect**: When the user hovers over the mole, the cursor changes, and the mole is highlighted.

### JavaScript Functionality:
  #### Variables:
- `score`: Tracks the player's score.
- `currentHole`: Keeps track of which hole currently has the mole.
- `gameTimer`: Controls the interval at which the mole appears.
- `moleVisible`: Boolean indicating if the mole is currently visible.
- `timeLeft`: Remaining time for the game.
- `endGameTime`: Total duration of the game (in seconds). Change this value to adjust the game length.
### DOM References:
- `startButton`: The start game button.
- `scoreBoard`: The score display element.
- `timerDisplay`: The timer display element.
- `holes`: A NodeList of all the hole elements.
### Event Listeners:
- `startButton.addEventListener('click', startGame);`: Starts the game when the button is clicked.
### `startGame()` Function:
- Resets Game Variables: Resets the score, time left, mole visibility, and current hole.
- Updates Displays: Resets the score and timer displays.
- Starts Mole Movement: Calls `randomHole()` every second to move the mole.
- Starts Countdown Timer: Decreases `timeLeft` every second and updates the timer display.
- Ends Game After Duration: Uses `setTimeout()` to call `endGame()` after the specified duration.
### `randomHole()` Function:
- Hides Previous Mole: If a mole is visible, it hides it before showing a new one.
- Selects Random Hole: Chooses a random hole from the list of holes.
- Shows Mole: Displays the mole in the new hole.
- Adds Click Listener: Adds a click event listener to the mole to handle whacking.
### `whack()` Function:
- Checks Mole Visibility: Ensures the mole is visible before processing the click.
- Increases Score: Increments the player's score.
- Updates Display: Updates the score display with the new score.
- Hides Mole: Hides the mole after it's been clicked.
- Updates Mole Status: Sets `moleVisible` to false.
### `endGame()` Function:
- Stops Mole Movement: Clears the interval that moves the mole.
- Displays Final Score: Shows an alert with the player's final score.
- Hides Mole: Hides any mole that might still be visible.
## Additional Helpful Notes:
### Game Duration Control:
- `endGameTime` Variable: Centralizes the game duration. By changing this value, you can easily adjust how long the game lasts without modifying multiple parts of the code.
- Synchronization: The `timeLeft` is set to `endGameTime` to ensure the countdown matches the actual game duration.
### Timers and Intervals:
- `setInterval()`: Used for two purposes:
- Mole Movement: Moves the mole to a new hole every second.
- Countdown Timer: Updates the remaining time every second.
- `setTimeout()`: Schedules the `endGame()` function to run after the game duration has elapsed.
### Event Handling:
- Clicking the Mole: The `whack()` function is called when the mole is clicked.
- Avoiding Multiple Listeners: Before adding a new click listener to the mole, the previous listener is removed to prevent multiple events from firing.
### Random Selection:
- `Math.random()` and `Math.floor()`: Used to select a random index corresponding to a hole in the grid.
### Game State Management:
- `moleVisible` Flag: Keeps track of whether the mole is currently visible to prevent issues like increasing the score when the mole is not actually displayed.
- `currentHole` Reference: Allows the program to hide the mole in the previous hole before showing it in a new one.
### User Experience:
- Immediate Feedback: The score updates instantly when the mole is clicked.
- Game Over Alert: An alert displays the final score, providing closure to the game session.
## Tips for Understanding and Modifying the Code:
### Adjusting Game Difficulty:
- Change Mole Appearance Interval: Modify the interval in `setInterval(randomHole, 1000);` to make the mole appear more or less frequently.
- Adjust Game Duration: Change the value of `endGameTime` to make the game longer or shorter.
### Enhancing the Game:
- Add Sound Effects: Play a sound when the mole appears or is whacked to make the game more engaging.
  - Not required but can be added more than one way. This example uses the `Audio` object and the `.play()` method.
- Implement High Score Tracking: Add functionality to keep track of the highest score achieved during the session.
### Debugging:
- Console Logging: Use `console.log()` statements to output variable values and track the flow of the program.
- Testing Individual Functions: Test each function separately to ensure it works before integrating it into the main game loop.
### Understanding the Flow:
- Event-Driven Programming: The game relies on events (clicks, time intervals) to trigger functions.
- Asynchronous Execution: Timers and intervals execute code asynchronously, meaning they run independently of the main execution flow.
## Clarifications on Specific Code Segments:
### Why Use `setTimeout(endGame, endGameTime * 1000);`?
- This ensures that the `endGame()` function is called exactly after the game duration specified by `endGameTime`. Multiplying by 1000 converts seconds to milliseconds, which is required by `setTimeout()`.
### Why Not Call `endGame()` in the Countdown Timer?
- Since we already have a `setTimeout()` scheduled to call `endGame()`, there's no need to call it again in the countdown timer. This prevents the possibility of `endGame()` being called multiple times.
### Why Remove Event Listeners with `mole.removeEventListener('click', whack);`?
- Each time the mole moves to a new hole, we add a new event listener. If we don't remove the previous listener, we might end up with multiple listeners attached to the mole, causing unintended behavior like the score increasing multiple times with a single click.
### Why Check `if (currentHole)` Before Hiding the Mole?
- When the game starts, `currentHole` might be `null` since no mole has been displayed yet. Checking if it exists prevents errors when trying to access properties of an `undefined` object.
### Why Set `moleVisible` to `false` After Whacking the Mole?
- This flag helps prevent the player from increasing the score by clicking on the area where the mole was previously displayed or clicking rapidly during transitions.


