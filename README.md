# 2048
**by Wenda Wu, Copyright 2020. All rights reserved.**

# Key Skills Learned
This was my first project using the pygame library, and coding in an Object Oriented way in python.
By working on this, I learned:
* How to import external .png and .ttf files using pygame.
* How to display different graphics in pygame.
* How to create different classes in python.

# What is 2048?
2048 is a very simple game :D (he says).

The game consists of a 4 x 4 grid of squares.

Each square can be empty, or have a tile with a value (of a power of 2) on it.

The player can choose to go up, down, left, or right, and move all the "tiles" in that direction (until they hit a wall or another square).

When two squares of the same value collide, they instead form a square with the sum of their values (essentially doubling the value of one of them).

Most scoring systems add the value of the new square to the score when one is created.

After every move, one random empty square is turned into a square of value either 2, 4, or rarely 8.

The game ends when all the squares are filled and there are no two squares of the same value that are adjacent to each other.

The objective is to score as high as possible before a game over.

# Implementation
Because the game is so simple, the code is actually quite simple as well (He also says).

The approach taken is a board-centric approach, rather than a tile-centric[^1] one.

## Board-Centric? Tile-Centric?

Basically, what this means is that instead of tracking each little tile that shuffles around the board, the game tracks each square, and displays the value of the tile inside instead.

This is similar to chess programming, where developers usually have to choose between:
* a piece-centric[^1] approach (tracking each chess piece, and storing the information within the chess piece).

  or
  
* a board-centric approach (tracking the board as a whole, and storing the information of where each piece is in an array).

### Pros to Board-Centric
Well, I chose to programme in a board-centric way because:
* When the player makes a move (up down left or right), **Every** piece moves in that direction if it is possible for them to move.

  * Therefore, if we picked a tile-centric approach, for every tile we'd have to check the location of every other tile, and how the movement of this tile will affect the location and value of every other tile.
  * However, with a board-centric approach, we can cheat a bit. We already know which squares on the board have what values, and so, each square on the board just has to check all the squares in the direction of its movement.
  * This means that for a tile-centric approach, the time complexity would be $O(n^n)$[^2] for this process, as each tile would have to check the position and value of every other tile.
  * For a board-centric approach, the time complexity is $O(n\sqrt{n})$[^2]. This is because every square only needs to check the squares in the same line in the direction of travel.

* Tiles are created and destroyed all the time.

  * For a game of Checkers or Chess, there will only ever be a maximum number of pieces. You can't simply just place a pawn in the middle of the board.
  * Also for those games, for any given move a piece is either captured, or it isn't. You can't capture two pieces in a single move.
  * In 2048, neither of those rules are true. A huge aspect of the game is that a random tile spawns on the board after every move, and that you could theoretically remove up to 12 tiles (with perfect conditions) in a single move.
  * This is much easier to handle with a board-centric approach, as we don't have to worry about tile creation or destruction. There is always a fixed number of objects to refer to.
 
* It's much easier to program.

  *  Could you imagine trying to program a function that tracks every individual tile that is applicable in every single board configuration? I couldn't, and so I didn't.
  *  With a board-centric approach, we can split the board further into rows and columns[^3], and worry about programming code to deal with an individual row/column, and just iterating that for each row and column.

### Cons to Board-Centric
Well, there is one...

Animation.

Because we are not tracking the movement of each tile, it is damn near impossible to animate the movement of them.

Therefore, within the program, the values just... Teleport... Yeah. Teleport. They teleport to where they are meant to be.

Not a great solution, but the best one without a tile-centric approach.

## Implementing the game
So, we can split the program into two different sections:
* Defining the squares and the Board
* Playing the game

In my approach, I chose to store most of the information about the game in each board square. This information was:
* If the square was empty or not
* The value of the square
* The position of the square on the board and in the array in which it is stored
* If the square was touching any of the edges of the board.


[^1]:In 2048, the game "pieces" are called tiles, and so an approach that stores the information of each tile would be a tile centric approach.\
Basically, there are two different ways of representing game boards for board games. Tracking the information of a board as a whole, or allowing each piece to store their own information.
[^2]:In order to determine which is more efficient, we must remember that for the the tile-centric approach, n represents the number of tiles (squares that have a value), but for the board-centric approach, n represents the number of squares, empty or not.\
  Therefore, the break even point for computational time for a 4x4 board is 4 tiles, for a 5x5 board it is also 4 tiles, and for a 6x6 board it is also 4 tiles.\
  For a half-full board, worst case scenario a board-centric approach would do 64 comparisons. For a tile-centric approach, the worst case scenario is 16 million comparisons.
[^3]:In fact, you'll find that the code to handle the behaviour of squares in a column is identical to code that handles the behaviour of squares in a row, just with different constants.
