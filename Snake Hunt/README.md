# Snake Hunt

## Game Introduction

#### 1. What Is the Game?

**Snake Hunt** is a modern arcade-style version of the classic Snake game. The player controls a continuously moving snake, collects different types of apples to gain points and special effects, and tries to survive as long as possible. Unlike traditional Snake, the game introduces **multiple collectible types, hazards, temporary power-ups, increasing movement speed, timers, and mobile controls**.

#### 2. How to Play

Choose the **color of your snake**.

1. Press **PLAY** to begin.
2. Control the snake using **Arrow Keys or WASD**; mobile players can swipe.
3. Move toward apples to collect them and increase your score.
4. Avoid hitting the **walls, your own body, and bombs**.
5. Use beneficial apples strategically to gain shields, speed boosts, or additional points.
6. Survive as long as possible and achieve the highest score.
7. After game over, choose **Play Again** or return to the menu.

### 3. Important Mechanics

#### Apple System

Apples are the main source of points and special effects. They spawn in groups every **2.5 seconds**, with a maximum of six normal apples on the board, and each apple normally disappears after **5 seconds**.

| Apple | Effect |
| --- | --- |
| **Red** | +1 point |
| **Blue** | +2 points |
| **Green** | +3 points |
| **Purple** | +5 points |
| **Gold** | +10 points + 6-second shield |
| **Orange** | +10 points + 6-second speed boost |
| **White** | Resets the snake |
| **Rainbow** | Fills the board with beneficial apples temporarily |
| **Poison** | −2 points |
| **Rotten** | −5 points |
| **Bomb** | Causes game over |

The game's apple directory explicitly documents these effects.

#### Growth and Scoring

Normal scoring apples cause the snake to grow. Higher-value apples therefore increase both **score and physical length**, making the snake progressively harder to control. The code determines whether the eaten apple should cause growth before updating the snake.

#### Increasing Speed

The snake becomes gradually faster as it grows. Its base speed is **5 segments per second**, with an additional **0.2 segments per second for every extra segment**. The orange apple temporarily doubles the movement speed.

#### Shield

The Gold Apple grants **10 points and six seconds of invincibility**. While shielded, hitting a wall causes the snake to wrap around to the opposite side instead of crashing. The shield can also protect the snake from certain hazards.

#### Collision and Game Over

Without a shield, hitting the boundary or the snake's own body causes a crash. Eating a Bomb immediately triggers a separate explosion sequence and ends the game.

#### Rainbow Apple

The Rainbow Apple temporarily clears the existing apples and creates **20–25 beneficial apples**. Normal spawning resumes after six seconds, creating a short period where the player can rapidly collect valuable items.
