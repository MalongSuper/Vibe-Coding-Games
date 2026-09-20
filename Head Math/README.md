# Head Math

#### 1. What Is the Game?

**Head Math Pro** is a fast-paced browser-based mental arithmetic game designed to train calculation speed and accuracy. Players solve randomly generated **addition or subtraction problems** and try to achieve the highest possible score without making a mistake. The game combines mathematics with a timer, power-ups, visual effects, and a rank system to make repeated practice more engaging.

### 2. How to Play

Choose **Addition** or **Subtraction**.

1. For Addition, choose whether each problem contains **2, 3, or 4 numbers**.
2. Solve the displayed equation and enter the answer.
3. Press **Submit** or the **Enter** key.
4. A correct answer increases the score and generates a new question.
5. **One incorrect answer ends the game.**
6. Use power-ups when a problem is difficult.
7. Continue until you make a mistake, then check your final score, time, and rank.

### 3. Important Mechanics

#### Question Generation

Addition problems can contain 2–4 randomly generated numbers. The number generator is weighted toward smaller values, while subtraction generates two positive numbers and automatically places the larger number first to avoid negative answers.

#### Scoring

Every normal correct answer gives **1 point**. The game also tracks the number of correct answers and total playing time.

#### Power-Ups

There are three important power-ups:

- **Solve:** immediately provides the current answer.
- **Drop Digit:** removes a digit from a number, reducing the difficulty.
- **5x Score:** makes the next correct answer worth **5 points**.

Only **one power-up can be used per question**. Power-ups can also be restored after every five correct answers, with the restored type selected randomly.

#### Timer and Game Over

The game records total play time and monitors the time spent on each question. After **15 seconds** on a question, a hint encourages the player to use a power-up. A wrong answer triggers feedback and then ends the game.

#### Ranking System

The final score determines the player's rank:

| Score | Rank |
| --- | --- |
| 0–4 | Broken Math |
| 5–9 | Know Math |
| 10–19 | Basic Math |
| 20–49 | Abstract Math |
| 50–99 | Mega Math |
| 100–149 | Super Math |
| 150+ | Eternal Math |

These ranks provide long-term goals beyond simply completing individual questions.

### 4. Key Methods and Functions in the Code

| Function | Purpose |
| --- | --- |
| `weightedNumber()` | Generates numbers with a higher probability of producing smaller values. |
| `selectMode()` | Selects Addition or Subtraction and controls the appropriate menu flow. |
| `chooseTerms()` | Sets the number of terms for Addition problems. |
| `startGame()` | Resets game variables, activates the game interface, and creates the first equation. |
| `generateEquation()` | Creates a new mathematical problem and calculates its correct answer. |
| `startQuestionTimer()` | Tracks total game time and detects when the player has struggled for 15 seconds. |
| `submitAnswer()` | Validates the player's input, checks correctness, updates the score, or triggers game over. |
| `checkPowerRestoration()` | Awards a randomly selected power-up after every five correct answers. |
| `usePowerCalculator()` | Automatically solves the current question and awards a point. |
| `usePowerDigits()` | Removes a digit and recalculates the answer to make the problem easier. |
| `usePowerBoost()` | Activates the 5-point bonus for the next correct answer. |
| `getRank()` | Converts the final score into one of the seven ranks. |
| `endGame()` | Stops the timer and displays the final score, time, and rank. |
| `runEngine()` | Continuously renders the background matrix animation and particle effects. |

The core gameplay functions are concentrated in the JavaScript section of the HTML file, while the Canvas functions provide the game's animated visual effects and power-up graphics.
