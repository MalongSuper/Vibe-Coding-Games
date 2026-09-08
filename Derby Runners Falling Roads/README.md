# Derby Runners: Falling Roads

## 1. What is the Game?

**Derby Runners: Falling Roads** is a fast-paced, 2D side-scrolling obstacle runner and racing game rendered entirely via HTML5 Canvas, Vanilla JavaScript, and Web Audio API. Inspired by anime horse-girl racing themes (reminiscent of *Uma Musume: Pretty Derby*), the game pits the player's chosen runner against 5 CPU-controlled AI opponents in fixed parallel track lanes. 

Players select from a expansive roster of over 20 unique chibi-styled runners—such as Special Week, Tokai Teio, Kitasan Black, Silence Suzuka, Symboli Rudolf, and Almond Eye—each featuring individual stat allocations (Speed, Stamina, Power, Skill, Gut, Wit) and procedural visual styling.

### Key Game Features:
- **Procedural Canvas Rendering**: Full vector-based rendering of chibi character sprites, animations, and status indicators without external sprite sheets.
- **Dynamic Track Lengths**: Selectable race distances ranging from 500 meters to 3000 meters.
- **Checkpoint System**: Integrated 4-segment checkpoint system with automatic respawn mechanics.
- **Weighted Item Mechanics**: Balanced item system featuring speed boosts, invulnerability shields, jetpacks, and targeted sabotage attacks.
- **Adaptive Day/Night Theme**: Global night mode toggle altering canvas lighting, star particle background dynamics, and UI themes.

---

## 2. How to Play

### Objectives
The objective of **Derby Runners: Falling Roads** is to navigate your runner down a fixed lane, jump over hazards (rocks, hurdles, fallen gaps), collect power-up orbs, and cross the finish line ahead of the 5 AI opponents.

### Controls & Workflow
1. **Main Menu**: Choose between starting a race, learning rules ("About the Game"), or toggling **Night Stage** mode.
2. **Roster Selection**: Browse the runner grid. Review character stat bars (**Speed**, **Stamina**, **Power**, **Skill**, **Gut**, **Wit**) and confirm your selection.
3. **Distance Selection**: Select the race length: **500m**, **1000m**, **2000m**, or **3000m**.
4. **In-Race Control**: 
   - **Auto-Acceleration**: Runners accelerate automatically along their designated lane.
   - **Jump (`[ J ]` Key)**: Press `[ J ]` to execute a vertical jump over obstacles and gaps.
   - **HUD Monitor**: Monitor real-time race progress percentage, current position rank, completed checkpoints, distance, active power-up timer, and live leaderboard updates.
5. **Post-Race**: View final placement standings on the Game Over modal.

---

## 3. Game Mechanics

### Movement & Physics Engine
Character motion is governed by a delta-time (`dt`) physics simulation:
- **Maximum Velocity**: Derived directly from the character's **Speed** stat:
  $$\text{maxSpeed} = \text{baseSpeed} + (\text{Speed} \times 1.4) \quad (\text{where } \text{baseSpeed} = 280)$$
- **Acceleration Rate**: Calculated using the **Power** stat:
  $$\text{accel} = 210 + (\text{Power} \times 2)$$
- **Gravity & Jump Impulse**: Gravity is fixed at $1300 \text{ px/s}^2$. Vertical jump impulse scales with **Power**:
  $$\text{jumpForce} = -520 - \text{Power}$$
- **Track Conversion**: World distance is scaled to canvas pixel space using a multiplier of $30 \text{ pixels/meter}$.

### Checkpoints & Respawn System
- Tracks are divided into **4 equal segments** by **3 intermediate checkpoints** placed at 25%, 50%, and 75% of total race length.
- When a runner collides with an obstacle without an active shield:
  1. The runner enters a `hit` state for 1.4 seconds with upward trajectory velocity ($ext{vy} = -280$).
  2. A visual particle explosion occurs in the character's accent color.
  3. The runner auto-respawns at `lastCheckpointX` with zero horizontal velocity ($	ext{vx} = 0$), resetting negative status ailments.

### Power-up & Sabotage System
Glowing item orbs are distributed along the course. Item types are determined via a **two-tier weighted probability system**:

| Category | Frequency | Item Type | Mechanics & Effect |
| :--- | :--- | :--- | :--- |
| **Boost** | 70% | **Speed** (35%) | Increases speed multiplier to $1.4\times$ for 5.0s. |
| | | **Shield** (35%) | Provides total immunity against obstacle collisions for 5.0s. |
| | | **Jetpack** (30%) | Elevates runner above obstacles ($y = -30\text{px}$) for 5.0s. |
| **Sabotage**| 30% | **Freeze** (40%) | Freezes target opponent in place for a specified duration. |
| | | **Butter** (40%) | Applies a slowing aura reducing target top speed. |
| | | **Arrow** (20%) | Forces target opponent into an immediate crash/hit state. |

---

## 4. How the AI Learns & Operates

Each CPU opponent is driven by an autonomous AI controller integrated into the update cycle (`updateAI(dt)`):

### Stat-Driven Autonomous Reaction
- **Perception & Obstacle Sensing**: AI runners scan ahead in their lane to detect upcoming obstacles and gaps.
- **Wit & Skill Modifiers**: The AI's decision to jump is influenced by its **Wit** and **Skill** stats. Higher **Wit** expands the AI's detection window, allowing it to initiate jumps with precision, while high **Skill** minimizes mistimed inputs.

### Adaptive Memory & Error Correction
- **Crash Tracking**: Each AI instance maintains state variables tracking performance:
  - `crashesSinceCheckpoint`: Keeps count of recent collisions in the current track segment.
  - `failedObstacleXs`: Maintains a memory array of exact X-coordinates where previous jump failures occurred.
- **Dynamic Learning Adjustment**: If an AI runner crashes into an obstacle, it records the coordinate. Upon respawning and re-approaching that position, the AI adjusts its jump timing (initiating jumps earlier or altering impulse duration) based on memory entries. As `crashesSinceCheckpoint` increases, the AI temporarily elevates its jump caution threshold to ensure safe clearance.

### Strategic Sabotage Targeting
When an AI runner collects a Sabotage power-up, it applies target selection logic based on race hierarchy:
- **Trailing AI**: Targets leading opponents ahead (prioritizing visible runners on screen).
- **Leader AI**: If the AI is currently in 1st place, it redirects sabotage attacks backward at the closest trailing pursuer.

---

## 5. Game Strategy

1. **Roster Selection & Stat Synergies**:
   - **High-Speed Runners** (e.g., *Kitasan Black*, *Sakura Bakushin O*): Ideal for longer tracks (2000m–3000m) where high top speeds can build dominant leads.
   - **High-Power Runners** (e.g., *Special Week*, *Tamamo Cross*, *Hishi Amazon*): Superior acceleration and higher jump heights make them resilient on obstacle-heavy tracks.
   - **High-Wit Runners** (e.g., *Agnes Tachyon*, *Mihono Bourbon*): Excel when played as AI or opponents due to lower collision error rates.

2. **Power-up Management**:
   - Save **Jetpack** and **Shield** status for dense obstacle clusters near track midpoints.
   - Use **Sabotage** items strategically: trigger attacks right as leading opponents approach major jump hazards to force high-penalty crashes.

3. **Checkpoint Risk Optimization**:
   - Take aggressive jump lines right after passing a checkpoint, as the penalty for crashing is minimal.
   - Play defensively when approaching a new checkpoint to avoid being sent back to the previous segment.
