# Snack and Ladder

## Problem Statement

- Here we create board of size 10 * 10 and dice of side 6.
- Each player puts their counter on the board at starting position at 1 and takes turns to roll the dice.
- Move your counter forward the number of spaces shown on the dice.
- If your counter lands at the bottom of a ladder, you can move up to the top of the ladder.
- If your counter lands on the head of a snake, you must slide down to the bottom of the snake.
- Each player will get a fair chance to roll the dice.
- On the dice result of 6, the user gets one more chance to roll the dice again. However, the same user can throw the dice a maximum of 3 times.
- Note: if the result of the dice is 6,6,6 the user can not throw the dice again as the maximum attempts are over and the next user will get to throw the dice.
- When the user rolls dice and it leads to an invalid move, the player should remain in the same position.
  - Ex: when the user is in position 99 and rolling of dice yields any number more than one the user remains in the same position.
- Print the ranks of users who finished first, second, and so on…


## Solution

