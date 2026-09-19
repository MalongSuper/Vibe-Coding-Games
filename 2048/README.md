## Classic 2048 Gane

**2048** is a tile-merging puzzle game played on a **4×4 grid**. The goal is to combine tiles until the target tile is reached. In **Classic mode**, matching tiles are merged to create larger values, with **2048** as the winning tile. The game also includes a **Fibonacci mode**, where tiles follow the Fibonacci sequence and the target is **377**.

## How to Play

Players move the tiles using the **arrow keys** or by **swiping on a touch screen**. When a direction is selected, all tiles slide as far as possible in that direction. In Classic mode, two tiles with the same value merge into one larger tile; for example, `2 + 2 = 4`. A new tile is normally added after every four moves, while another tile appears automatically every eight seconds, so players must continuously create space on the board.

The game is won when the target tile is created. It ends when the board becomes full and no valid merges remain.

## Mechanics

The game maintains a **4×4 grid** containing tile objects. Each tile stores its value and position, while the game keeps track of the current score, number of moves, highest tile, selected mode, and game state.

The central mechanic is the **movement and merging system**. For each move, the program processes every row or column in the selected direction, removes empty spaces, moves tiles toward the chosen edge, and merges compatible neighboring tiles. A tile can only participate in one merge during a single move.

Two different rule sets are implemented through the `MODES` object. Classic mode allows equal tiles to merge, while Fibonacci mode allows neighboring Fibonacci numbers to merge, such as `1 + 2 = 3`, `2 + 3 = 5`, and `3 + 5 = 8`.
