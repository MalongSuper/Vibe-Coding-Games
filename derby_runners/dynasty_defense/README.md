# Dynasty Defense - Overview

### 1. What Is the Game?

**Dynasty Defense: The Four Paths** is a browser-based **tower-defense strategy game** in which the player protects a central Emperor’s Palace from enemy forces approaching along **four converging paths**. The battlefield is centered around the palace, with enemy spawn points positioned to the west, east, north, and south.

The player begins each battle with **500 gold and 30 Palace Lives**, then constructs defensive units on available tower plots. The objective is to survive every wave while preventing too many enemies from reaching the palace.

The game combines several tower-defense concepts: strategic tower placement, different attack types, resource management, tower upgrading, hero selection, increasingly difficult waves, and boss encounters.

Importantly, this game **does not use a learning AI system**. Enemy movement and combat are deterministic, scripted behaviors governed by predefined statistics and wave-generation rules. The challenge comes from the increasing number, speed, durability, and classification of enemies rather than from opponents learning from the player.

### 2. How to Play

Before entering battle, the player chooses a difficulty:

- **Easy — 15 waves**
- **Medium — 20 waves**
- **Hard — 30 waves**

The player must also select **exactly six heroes** during the War Council phase before the battle can begin.

Once the battlefield begins, the basic procedure is:

1. Start with **500 gold and 30 Palace Lives**.
2. Choose a standard soldier or one of the six selected heroes.
3. Select an available tower plot around the central battlefield.
4. Spend gold to deploy the unit.
5. Allow the unit to attack approaching enemies automatically.
6. Upgrade standard units by placing the **same unit type** on an existing standard unit.
7. Use demolish mode to remove units and reclaim their plots.
8. Defend against increasingly difficult waves.
9. Survive boss waves and the final ultimate boss.
10. Win by completing the final wave before the Palace loses all of its Lives.

The game itself describes the main strategic loop as deploying units when enough gold is available and upgrading matching standard units up to **Level 5**. Heroes are treated differently and cannot be upgraded.

### 3. Important Game Mechanics

#### Four Converging Paths

The most distinctive feature is the **four-direction battlefield**. Enemies can enter from: **West; East; North; South.** All four paths converge on the central palace. The game represents these spawn points explicitly in `PathEngine.spawnPoints`.

This means the player must think about **coverage across the entire map**, rather than concentrating all towers along one traditional horizontal lane.

#### Tower Placement

The battlefield contains a large collection of circular tower plots arranged around the center. A plot can contain one unit at a time.

When a unit is selected, the player clicks an available plot to deploy it. The game checks whether the player has enough gold and whether the plot is already occupied before creating the unit. This makes **positioning and attack range** extremely important.

#### Gold Economy

Gold is the primary resource. The standard unit costs are:

| Unit | Cost |
| --- | --- |
| Melee | 20 G |
| Blade | 30 G |
| Archer | 40 G |
| Mace | 50 G |
| Spear | 60 G |
| Magic | 100 G |

Heroes cost **150 G** each. The player therefore needs to decide between deploying more units, using expensive but powerful units, purchasing heroes, and upgrading existing towers.

#### Standard Unit Roles

The game provides six standard unit types with different statistics:

| Unit | Range | Damage | Attack Interval | Role |
| --- | --- | --- | --- | --- |
| **Melee** | 70 | 12 | 0.6 s | Cheap close-range defense |
| **Blade** | 85 | 14 | 0.5 s | Fast melee attacker |
| **Archer** | 190 | 9 | 0.7 s | Long-range attacker |
| **Mace** | 75 | 45 | 1.8 s | Heavy slow damage |
| **Spear** | 125 | 18 | 0.8 s | Balanced melee/ranged coverage |
| **Magic** | 130 | 28 | 1.4 s | Strong ranged damage |

These characteristics create different tactical roles rather than making every tower interchangeable.

#### Automatic Targeting and Attacking

Once deployed, units automatically search for enemies inside their range.

The core entity-update system searches for the nearest enemy within the unit's range. When an enemy is found, the unit waits for its attack cooldown and then either launches a projectile or applies direct damage, depending on its attack type.

This means the player does not manually control individual attacks. The main strategic decisions are **where to place units, what type to place, and when to upgrade them**.

### 4. Leveling and Upgrading

One of the most important mechanics is the **unit upgrade system**.

A standard unit begins at **Level 1**. To upgrade it, the player selects the same unit type and places it on the already occupied plot.

**Each upgrade increases the unit's level, multiplies its damage by 1.5, increases its range by 10%, and costs the normal purchase price of that unit.**

Standard units can be upgraded up to **Level 5**. For example, upgrading an Archer repeatedly produces a tower with substantially greater damage and attack coverage without requiring another plot.

Heroes are explicitly excluded from this system. They **cannot be leveled up**, and the game also prevents using a hero to upgrade a standard unit.

This creates an important strategic decision between: 

- **Wide deployment** — spreading more units over more plots.
- **Vertical investment** — concentrating resources into a smaller number of highly upgraded towers.

### 5. Heroes

Before the battle begins, the player drafts **exactly six heroes** from a roster of 36 fixed characters. Each hero has a name, class type, gender, and visual characteristics.

Examples include:

- Lin Wei — Magic
- Mei Ling — Spear
- Zhao Yun — Blade
- Sun Shang — Archer
- Zhang Fei — Mace
- Diao Chan — Magic
- Guan Yu — Blade
- Lu Bu — Mace
- Zhu Ge — Magic
- Zhou Yu — Archer
- Lu Meng — Spear
- Huang Gai — Mace.

Heroes cost **150 G** to deploy. They receive substantial statistical bonuses compared with the corresponding standard unit:

- **35% greater range**
- **150% greater damage**
- **25% faster firing**, because their fire interval is multiplied by 0.75.

However, only one copy of each drafted hero can be deployed at a time.

Thus, heroes function as **elite versions of existing unit classes**, rather than as completely separate upgrade trees.

### 6. Enemy and Wave System

There is **no machine-learning AI** in this game. Instead, enemies are created by the `WaveManager`, which determines how many enemies appear, which types are used, which paths they enter from, when they spawn, whether the wave contains a boss, and whether the wave is the final encounter.

The game's enemies are therefore best described as **scripted/algorithmic opponents**.

#### Normal Enemies

For ordinary enemies, the system starts with a base HP of **25**, damage of **5**, and speed of **45**, then applies wave and difficulty multipliers.

The available normal enemy archetypes correspond to the player's standard classes: Melee; Blade; Archer; Magic; Mace; Spear

Early waves primarily feature one type, while later waves mix different unit classes. From Wave 5 onward, the game combines a close/mid-range type with Archer or Magic units.

#### Difficulty Scaling

Enemy durability increases as the wave number increases. The HP multiplier is: `1 + (current wave × 0.25)` . Hard mode receives an additional **0.5** multiplier. 

Enemy speed is also adjusted according to difficulty: Easy: `0.5` ;  Medium: `0.8` ;  Hard: `1.0`relative to the base speed calculation. This means later waves become harder through both **greater enemy endurance and faster pressure**, rather than merely spawning more enemies.

### 7. Bosses and the Final Boss

Bosses are introduced on **every fifth wave**. 

A boss wave selects one lane and inserts a stronger boss-type enemy into the normal spawn queue.  The boss archetype is randomly selected from Melee, Blade, Archer, or Magic.

Boss enemies receive substantially greater statistics: **600 × wave/difficulty multiplier + 300 HP; 25 damage; 35 × difficulty speed multiplier.** They are therefore considerably tougher than ordinary troops.

#### Final Boss

The final wave is different. A single random path receives the **ultimate boss**. The boss depends on difficulty:

- **Easy:** Knight
- **Medium:** Gladiator
- **Hard:** Priestess.

The ultimate boss has: **3500 × wave/difficulty multiplier HP; 100 damage; 20 × difficulty speed multiplier.** It is deliberately slower than ordinary enemies but has an extremely large health pool and catastrophic life damage if it reaches the palace.

An ultimate boss removes **7 Palace Lives** when it reaches the center, compared with 3 Lives for a regular boss-class enemy and 1 Life for a standard enemy.

The visual size also emphasizes the hierarchy: ultimate bosses are rendered at **2.6× scale**, while regular boss-class enemies are rendered at 1.4× scale.

A notable implementation detail is that the final boss names are mostly a **presentation/classification layer**: the core spawning code primarily gives them the ultimate-boss statistics and the corresponding Knight/Gladiator/Priestess appearance.

### 8. Palace Lives and Losing

The Palace begins with **30 Lives**.

When an enemy reaches the central target, the game reduces the player's Lives according to the enemy category:

- Normal enemy → **−1 Life**
- Boss/hero enemy → **−3 Lives**
- Ultimate boss → **−7 Lives**

If Lives reach zero, the game immediately ends in defeat.

This gives the player a limited margin for error, while allowing weaker enemies to leak occasionally without immediately ending the game.

### 9. Strategy

The strongest strategy is to think about **coverage, specialization, and upgrades** rather than simply filling every plot.

#### Cover All Four Paths

Because enemies approach from four directions, concentrating towers in a single area can leave another path undefended. Long-range units such as **Archers** are particularly useful for extending coverage across a path, while shorter-range high-damage units can protect areas close to the palace.

#### Combine Attack Roles

A balanced defense can combine:

- **Blade/Melee** for rapid close-range damage.
- **Mace** for large individual attacks.
- **Spear** for balanced coverage.
- **Archer** for long-range coverage.
- **Magic** for strong ranged damage.

The difference between range, damage, and attack interval means that a mixture of towers is more flexible than relying exclusively on one class.

#### Upgrade Efficiently

Because each standard-unit upgrade multiplies damage by 1.5 and increases range by 10%, upgrading an existing strategic tower can be more effective than continuously building low-level replacements.

However, concentrating upgrades too heavily can leave another path without coverage. The player must balance **vertical strength** against **map-wide coverage**.

#### Use Heroes as Elite Anchors

Heroes cost considerably more than basic units, but their range, damage, and firing speed bonuses make them powerful focal points for the defense.

Because only the six drafted heroes are available and each can only be deployed once, they should be positioned carefully rather than treated as disposable units.

#### Prepare for Boss Waves

Every fifth wave introduces a boss, so the player should avoid entering these waves with a weak economy or poorly upgraded defenses. The final wave is especially important because it contains the ultimate boss in addition to the normal wave force.

#### Prioritize the Most Dangerous Path

The game explicitly identifies the path associated with boss spawning in its wave warning system. This gives the player advance information about where major threats will enter, allowing the player to prepare that direction before the wave begins.
