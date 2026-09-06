# Attack The Tide

## 1. What Is the Game?

**Attack The Tide** is a browser-based **lane-based tower-defense strategy game** in which the player must defend a farm-like battlefield from progressively stronger waves of enemies. The game combines unit placement, resource management, automated combat, defensive structures, special abilities, and global super powers.

The battlefield is organized into **five lanes and twelve columns**. Enemies enter from the far side of the battlefield and continuously advance toward the player's defensive line. The player's heroes are placed in columns 2–12, while **Column 1 is reserved for Spike Rollers**, which provide a limited defensive buffer.

The game contains **seven eras**, ranging from the Tensei Era and Greek Era to the Medieval, Warfare, Robotic, Hybrid, and Nightmare Eras. Each era introduces a different visual theme and expands the pool of enemies available during waves.

The objective is simple but demanding: **survive every wave without allowing an enemy to breach the final defensive line**. The game supports Easy, Medium, and Hard difficulty levels. Depending on the era and difficulty, a stage can contain between **8 and 24 waves**.

---

## 2. How to Play

At the beginning of a stage, the player receives **100 buns**, while Sacred Flames start at zero. There is also a preparation period before the first wave, giving the player time to construct the initial defense.

The basic gameplay process is:

1. **Choose an era and difficulty.**
2. During the preparation phase, select a hero card.
3. **Click an empty battlefield cell** in columns 2–12 to place the selected hero.
4. Spend **buns** to deploy heroes.
5. Collect falling buns and Sacred Flames to increase available resources.
6. Allow the heroes to automatically attack approaching enemies.
7. Use the heroes' individual abilities and the global **Super Powers** at appropriate moments.
8. Survive each successive enemy wave.
9. Prevent enemies from reaching Column 1 after the Spike Rollers have been consumed.
10. Survive the final wave to achieve victory.

Heroes cannot be placed in an occupied cell, and the game prevents deployment when the player does not have enough buns or when that hero's cooldown has not finished.

---

## 3. Important Game Mechanics

### Lane-Based Defense

The battlefield consists of **five independent lanes**. Enemies normally remain within their assigned lane and move toward Column 1. This makes lane management important: a strong defense in one lane does not automatically protect the others.

Enemy placement during wave generation attempts to distribute enemies among lanes by repeatedly selecting the lane with the lowest current enemy count. This prevents the entire wave from being concentrated into a single lane.

### Resources

The game uses two main resources:

**Buns** are used to deploy heroes. Different heroes have different costs, ranging from inexpensive defensive units such as the Farmer and Shield Man to expensive attackers such as the Priestess.

Farmers generate buns at their location, while additional buns periodically fall from the sky. Players can click these drops to receive **25 buns**. 
**Sacred Flames** are used for global Super Powers. Flames periodically fall from the sky and provide **25 flames** when collected. 
This creates an economic layer in which the player must decide whether to spend buns immediately on more units or conserve resources for stronger defensive combinations and special abilities.

### Hero Deployment and Cooldowns

Every hero has:

- a **cost** in buns,
- a **cooldown** before another copy can be deployed,
- a health value,
- and a unique combat or defensive ability.

Examples include the Archer, Double Archer, Dagger, Shield Man, Buddhist, Mine, Spikeweed, TNT Barrel, Mage, Swordsman, and Priestess.

The placement system therefore encourages the player to build a **combination of roles** rather than repeatedly using a single unit.

### Combat

Heroes attack automatically according to their individual behavior. Basic ranged units can fire projectiles at enemies in their lane, while specialized units provide defensive or area effects. The game continuously updates units, enemies, projectiles, drops, and visual effects as part of the main simulation.

The game also includes special defensive units:

- **Shield Man** has very high health and acts as a blocker.
- **Mine** arms after ten seconds and destroys enemies on its tile.
- **Spikeweed** destroys enemies occupying its tile, with special handling for Very High toughness enemies.
- **TNT Barrel** explodes after one second and attacks a 3×3 area.
- **Buddhist** can jump to a nearby enemy tile and destroy enemies there.
- **Priestess** periodically fires a powerful lane-wide attack against enemies ahead of her. 
### Enemy Speed, Endurance, and Abilities

Unlike the previous racing game, **Attack The Tide does not contain a learning AI system**. The enemies are scripted entities with predefined statistics and behaviors.

Each enemy type is defined with characteristics such as:

- **HP**, representing endurance,
- **speed**, determining movement rate,
- **damage**, determining how strongly it attacks defenders,
- **toughness**, indicating its resilience category,
- and, for special enemies, unique abilities.

For example:

- **Bronze Soldier:** 8 HP, speed 18, low toughness.
- **Silver Soldier:** 16 HP, speed 20, medium toughness.
- **Gold Soldier:** 24 HP, speed 20, high toughness.
- **Bamboo Jumper:** speed 24 and can jump over defenders.
- **Ninja:** speed 32, making it one of the fastest enemies.
- **Samurai:** high damage at 105.
- **Sentinel:** 48 HP, speed 14, very high toughness, and an instant-kill laser.
- **Female Rider:** extremely fast at speed 60 and causes a 3×3 explosion when it crashes into a defender.
- **Dragon:** 48 HP, speed 14, and periodically breathes blue flame through its lane. 
This means the enemies are not simply differentiated by appearance. Their predefined **speed, endurance, damage, and special behaviors** directly affect how the player must defend each lane.

### Enemy Movement

Normal enemies move toward Column 1 at their assigned speed. Movement can be interrupted or modified by effects such as **Chains, Freeze, and Slow**. When slowed, an enemy's movement multiplier becomes 0.45 of its normal speed.

The enemy update system also implements specialized movement logic. For example, Bamboo Jumpers detect defenders in front of them and can jump over an occupied position rather than simply stopping at it.

### The Breach System

Column 1 is the final defensive boundary.

When an enemy reaches Column 1, the game first checks whether the Spike Roller for that lane is still available. If so, the Spike Roller activates, destroys the enemies in that lane, and is consumed. If the lane has already used its Spike Roller, the next enemy that reaches the boundary causes an immediate defeat.

This creates a critical strategic mechanic: **the Spike Roller is not a permanent defense**. It provides one emergency save for each lane, but it cannot be relied upon indefinitely.

---

## 4. How the Enemies Work

Because the enemies do not use machine learning, there is no AI training process comparable to reinforcement learning or adaptive AI.

Instead, enemy behavior is implemented through **predefined rules and state variables**. When an enemy is spawned, the game creates an enemy object containing its HP, maximum HP, speed, damage, lane, toughness, timers, and special-state variables such as freeze, slow, chain, invisibility, jumping, or special attack timers. 
The `updateEnemies(dt)` method then applies those programmed rules every frame. It:

- decreases status-effect timers,
- moves enemies according to their speed,
- handles blocking,
- performs enemy-specific abilities,
- attacks defending units,
- checks for lane breaches,
- and removes defeated enemies from active gameplay. 
Therefore, the game's "intelligence" comes from **carefully scripted behaviors**, not from an AI model learning from previous games.

---

## 5. Waves and Difficulty Progression

Enemies arrive in waves rather than continuously.

The number of waves depends on the selected era and difficulty. For most eras:

- **Easy:** 8 waves
- **Medium:** 12 waves
- **Hard:** 16 waves

The final Nightmare Era is longer:

- **Easy:** 12 waves
- **Medium:** 18 waves
- **Hard:** 24 waves.

Wave size also increases as the game progresses. The wave-generation function uses both the selected difficulty and the current wave number to increase enemy counts. Major waves receive additional enemies and may introduce Star Soldiers.

Later eras also introduce new enemy types while retaining some enemies from earlier eras. Consequently, difficulty increases not only through larger numbers but through a broader **combination of enemy behaviors and abilities**.

---

## 6. Super Powers

Super Powers provide battlefield-wide emergency abilities and consume Sacred Flames. Each has a cooldown and resource cost.

The main powers are:

| Power | Function |
|---|---|
| **Thunder** | Instantly destroys enemies across the battlefield. |
| **Fire** | Burns and destroys all enemies. |
| **Ice** | Deals 50% current-HP damage and slows enemies for 5 seconds. |
| **Tornado** | Destroys enemies and can also slow/push surviving enemies backward. |
| **Chains** | Locks enemies in place temporarily without dealing damage. |
| **Pushing Hand** | Pushes enemies backward across the battlefield. |

These effects are implemented directly in `usePower(powerId)`. For example, Ice applies a five-second slow and deals 50% damage, while Pushing Hand resets enemies to the far side of the battlefield. 
The important strategic point is that Super Powers have **costs and cooldowns**, so they should not be treated as unlimited attacks.

---

## 7. Strategy

The most important strategy is to build a **balanced defense rather than simply maximizing damage**.

### Build Defensive Layers

A strong defense should generally contain a combination of:

- **Damage dealers**, such as Archers, Double Archers, Mages, and Swordsmen.
- **Blockers**, especially the Shield Man.
- **Area or trap units**, such as Mines, Spikeweed, and TNT Barrels.
- **Specialized units**, such as Buddhist and Priestess.

Because each enemy enters through a specific lane, placing the right defensive unit in the correct lane is often more important than simply deploying the most expensive unit.

### Protect Vulnerable Lanes

Do not allow one lane to become significantly weaker than the others. Since a breach in an already-consumed Spike Roller lane can immediately end the game, monitoring the whole battlefield is essential.

### Save Powerful Abilities

Super Powers are especially valuable against major waves and large groups of high-endurance enemies. Using Thunder, Fire, Ice, or Tornado too early may leave the player without an emergency tool during a more dangerous wave.

### Use Enemy Properties Against Them

Enemy speed and toughness should influence placement decisions. Fast enemies such as Ninjas and Female Riders can overwhelm a weak lane before slow heavy enemies become a problem, while high-toughness enemies require sustained damage or specialized abilities.

### Manage the Economy

Buns are limited early in a stage, so spending everything immediately can make it difficult to respond to later threats. Farmers are especially valuable because they provide a recurring source of buns, while falling resources provide additional opportunities to recover economically. 
### Exploit Enemy Grouping

Area-of-effect defenses such as TNT Barrel and Spikeweed become particularly useful when several enemies occupy nearby cells. Similarly, global powers are strongest when many enemies are simultaneously present.
