# 2048
**by Wenda Wu, Copyright 2020. All rights reserved.**

### Key skills learned
This was my first project using the pygame library, and coding in an Object Oriented way in python.
By working on this, I learned:
* How to import external .png and .ttf files using pygame
* How to display different graphics in pygame
* How to create different classes in python

### How does it work?
The game is very simple (he says)

The game consists of a 4 x 4 grid of squares. The player can choose to go up, down, left, or right, and move all the squares in that direction (until they hit a wall or another square)

When two squares of the same value collide, they instead form a square with the sum of their values (essentially doubling the value of one of them)

Most scoring systems add the value of the new square to the score when one is created

After every move, one random empty square is turned into a square of value either 2, 4, or rarely 8

The game ends when all the squares are filled and there are no two squares of the same value that are adjacent to each other

The objective is to score as high as possible before a game over

### That's neat, but how was it implemented?
Because the game is so simple, the code is actually quite simple as well (He also says)

The approach taken is a square centric approach, rather than a tile centric one.
