# Sliding Sudoku

## Game Introduction

### 1. What Is the Game?

**Sliding Sudoku** is a puzzle game that combines traditional Sudoku with **adjacent sliding mechanics**. Instead of directly entering numbers, the player must move the existing digits around the board by swapping neighboring cells until the board matches a valid Sudoku solution. The game features three difficulty levels: **Easy (6×6), Medium (9×9), and Hard (18×18)**.

### **2. How to Play**

Choose a difficulty:

- **Easy:** 6×6 grid, digits 1–6, 3×2 blocks.
- **Medium:** 9×9 grid, digits 1–9, 3×3 blocks.
- **Hard:** 18×18 grid, digits 1–18, 3×6 blocks.

Then:

1. Click or tap a cell to select it.
2. Use the **Arrow Keys or WASD** to swap the selected digit with an adjacent cell.
3. Only **up, down, left, and right** moves are allowed.
4. Continue rearranging the digits until every cell matches the generated solution.
5. The game tracks both **moves and time**.
6. Solve the entire board to win.

### 3. Important Mechanics

#### Sudoku-Based Objective

The goal is not simply to create a visually correct board. Every **row, column, and block** must contain each digit exactly once. The game generates a complete valid Sudoku solution first and then scrambles it.

#### Sliding / Swapping

The central mechanic is swapping two neighboring cells. Each successful swap increases the move counter, moves the selected position to the destination cell, and checks whether the puzzle has been solved.

#### Guaranteed Reachable Puzzle

The starting board is created by performing many **random adjacent swaps** on the solved board. Therefore, the puzzle remains a reachable permutation of the solution rather than being an unrelated random arrangement.

#### Move and Time Tracking

The move counter records every swap. The timer does not begin immediately when the puzzle appears; it starts with the player's **first move** and increases once per second.

#### Correct-Cell Highlighting

Cells that currently contain the correct digit are highlighted in **light navy blue**, while the selected cell is highlighted in **light orange**. This provides visual feedback about progress.

#### Winning Animation

When every cell matches the solution, the timer stops and a **diagonal wave/cascade animation** passes across the board. After three seconds, the game displays the final number of moves and completion time.

#### Difficulty Scaling

The difficulty affects the board size and Sudoku structure rather than simply changing a numerical parameter. The Hard mode contains **324 cells**, making it substantially larger than the 36-cell Easy board.
