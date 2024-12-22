# Snack and Ladder

## Understand Requirements

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


## Identify Classes and Objects

### Board
- It is a n * n board.
- It has n * n cells.
- Each cell has a position.
- Each cell has a snake or ladder.

```
class Board {
    int n;

    constructor(n) {
        this.n = n;
    }
}
```

### Jumper
- It has a id.
- It has a start position.
- It has a end position.
- start position is greater than end position.

```
class Jumper {
    int id;
    int startPosition;
    int endPosition;
}
``` 

### snake
- it has a id.
- It has a start position.
- It has a end position.
- start position is greater than end position.
- it takes the player to the end position.

```
class Snake extends Jumper {
    constructor(id, startPosition, endPosition) {
        super(id, startPosition, endPosition);
    }
}
```

### ladder
- It has a id.
- It has a start position.
- It has a end position.
- start position is less than end position.
- it takes the player to the end position.

```
class Ladder extends Jumper {
    constructor(id, startPosition, endPosition) {
        super(id, startPosition, endPosition);
    }
}
```

### Player
- It has a id.
- It has a name.
- It has a current position.
- It has a rank when the game is over.

```
class Player {
    int id;
    String name;
    int currentPosition;
    int rank;

    constructor(id, name) {
        this.id = id;
        this.name = name;
        this.currentPosition = 1;
        this.rank = 0;
    }
}
```

### Dice
- It has a k side.
- It has a result when rolled.

```
class Dice {
    int k;
    int result;

    constructor(k) {
        this.k = k;
    }
}
```

## Define Relationships & Methods


### Board

- Board has list of snakes and ladders.

```
class Board {
    int n;
    List<Snake> snakes;
    List<Ladder> ladders;
    Map<Integer, Snake> snakeMap;
    Map<Integer, Ladder> ladderMap;

    constructor(n) {
        this.n = n;
        this.snakes = new ArrayList<>();
        this.ladders = new ArrayList<>();
        this.snakeMap = new HashMap<>();
        this.ladderMap = new HashMap<>();
    }

    addSnake(Snake snake) {
        this.snakes.add(snake);
        this.snakeMap.put(snake.startPosition, snake);
    }

    addLadder(Ladder ladder) {
        this.ladders.add(ladder);
        this.ladderMap.put(ladder.startPosition, ladder);
    }

    getSnake(int position) {
        return this.snakeMap.get(position);
    }

    getLadder(int position) {
        return this.ladderMap.get(position);
    }

    hasSnake(int position) {
        return this.snakeMap.containsKey(position);
    }

    hasLadder(int position) {
        return this.ladderMap.containsKey(position);
    }
}



```
### Dice

- Dice has a result when rolled by the current player.

```
class Dice {
    int k;
    int result;

    constructor(k) {
        this.k = k;
    }

    int roll() {
        return random.nextInt(k) + 1;
    }
}
```

### Game
- It has a board and board has list of snakes and ladders.
- It has a dice.
- It has a list of players.
- It has a current player.
- current player is the player who is currently playing who rolls the dice.
- It has a list of players who has finished the game with certain rank.

```
class Game {
    Board board;
    Dice dice;
    List<Player> players;
    Player currentPlayer;
    List<Player> finishedPlayers;

    constructor(board, dice, players) {
        this.board = board;
        this.dice = dice;
        this.players = players;
        this.currentPlayer = players.get(0);
        this.finishedPlayers = new ArrayList<>();
    }

    changeCurrentPlayer() {
        this.currentPlayer = this.players.get(this.players.indexOf(this.currentPlayer) + 1 % this.players.size());
    }

    rollDiceOfCurrentPlayer() {
        int diceResult = this.dice.roll();
        int nextPosition = this.board.getNextPosition(this.currentPlayer.currentPosition, diceResult);
        
        if (nextPosition > this.board.n) {
            nextPosition = this.currentPlayer.currentPosition;
        }
        
        if (this.board.hasSnake(nextPosition)) {
            nextPosition = this.board.getSnake(nextPosition).endPosition;
        }
        
        if (this.board.hasLadder(nextPosition)) {
            nextPosition = this.board.getLadder(nextPosition).endPosition;
        }

        this.currentPlayer.currentPosition = nextPosition;

        if (nextPosition == this.board.n) {
            this.addRankedPlayer(this.currentPlayer);
        }

        this.changeCurrentPlayer();

        return diceResult;
    }

    addSnake(Snake snake) {
        if (snake.startPosition > snake.endPosition) {
            this.board.addSnake(snake);
        }
    }

    addLadder(Ladder ladder) {
        if (ladder.startPosition < ladder.endPosition) {
            this.board.addLadder(ladder);
        }
    }

    addPlayer(Player player) {
        this.players.add(player);
    }

    removePlayer(Player player) {
        this.players.remove(player);
    }

    addRankedPlayer(Player player) {
        player.rank = this.finishedPlayers.size() + 1;
        this.finishedPlayers.add(player);
        this.players.remove(player);
    }
}
```

## Data Structures

Using list and hashmap data structure for storing snakes, ladders, players and finished players. and finding snakes and ladders in O(1) time.

- List of snakes and ladders.

```
List<Snake> snakes;
List<Ladder> ladders;
```

- List of players.

```
List<Player> players;
```

- List of finished players. 

```
List<Player> finishedPlayers;
```

## State Diagrams And Sequence Diagrams


## Error Handling

Throwing error when the player is not found in the list of players or the snake or ladder is not found in the board.


## Design Patterns

### Factory Design Pattern

Using factory design pattern for creating snakes and ladders.

### Singleton Design Pattern

Using singleton design pattern for creating board, dice and game.



