# TETRIS

### 1. What Is the Game?

**Tetris** is a block-stacking puzzle game played on a **10×20 grid**. Seven standard tetrominoes fall from the top, and the player moves and rotates them to create complete horizontal lines. Completed lines disappear, awarding points and increasing the level and falling speed.

### 2. How to Play

- **← / A, → / D:** Move left/right
- **↑ / W:** Rotate
- **↓ / S:** Soft drop
- **Space:** Hard drop
- **P:** Pause
- Clear lines while preventing the blocks from reaching the top.

### 3. Important Mechanics

- Uses the seven **I, O, T, S, Z, J, and L** tetrominoes.
- Pieces are generated using a **7-piece bag system**, providing balanced randomization.
- Completing 1, 2, 3, or 4 lines gives **100, 300, 500, or 800 points × current level**.
- Every 10 cleared lines increases the level and makes pieces fall faster.
- Soft drop gives **1 point per row**, while hard drop gives **2 points per row**.
- A **ghost piece** shows where the current piece will land.
- The game includes pause, timer, next-piece preview, line-clear animations, and a session best score.

### 4. Key Methods and Functions

| Function | Purpose |
| --- | --- |
| `rotateMatrix()` | Rotates a tetromino. |
| `makeBag()` | Randomizes the seven-piece sequence. |
| `collides()` | Detects collisions with the board or boundaries. |
| `spawnPiece()` | Places a new piece at the top. |
| `lockPiece()` | Permanently places a falling piece on the board. |
| `clearLines()` | Removes completed rows. |
| `applyLineScore()` | Calculates score and increases the level. |
| `rotate()` | Rotates the active piece with wall-kick attempts. |
| `hardDrop()` | Instantly drops a piece and awards bonus points. |
| `endGame()` | Stops the game and displays the final result. |
| `loop()` | Runs the main animation, timer, falling, and rendering system. |

