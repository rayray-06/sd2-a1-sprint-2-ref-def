# sd2-a1-sprint-2-ref-def
sprint 2, working on the game i made in sprint 1 for software dev2 
# Platform Quest - 2D Platformer Game


## Table of Contents
- [1.0 Project Overview](#10-project-overview)
- [2.0 Project Aim and Objectives](#20-project-aim-and-objectives)
- [3.0 Game Concept & Target Audience](#30-game-concept--target-audience)
- [4.0 Overall Specification & Minimum Viable Product (MVP)](#40-overall-specification--minimum-viable-product-mvp)
- [5.0 User and System Requirements](#50-user-and-system-requirements)
- [6.0 Scrum-Style User Stories](#60-scrum-style-user-stories)
- [7.0 Scrum Product Backlog](#70-scrum-product-backlog)
- [8.0 Game Narrative, Characters, and Visual Design](#80-game-narrative-characters-and-visual-design)
- [9.0 Environment, Gameplay, and Player Motivation Loops](#90-environment-gameplay-and-player-motivation-loops)
- [10.0 Game Rules & Logic System](#100-game-rules--logic-system)
- [11.0 State Management Architecture](#110-state-management-architecture)
- [12.0 Engine, Platform, and Input Maps](#120-engine-platform-and-input-maps)
- [13.0 Core Algorithmic Pseudocode (GDScript Structure)](#130-core-algorithmic-pseudocode-gdscript-structure)
- [14.0 Project Management & Development Records](#140-project-management--development-records)
- [15.0 review](#150-review)

## 1.0 Project Overview
**Platform Quest** is a 2D side-scrolling platform game designed and developed using the **Godot Engine (v4.x)** and programmed in **GDScript**. Created as part of the reassessment for the Software Development 2 module, the project demonstrates how to plan, build, and test a simple interactive system.

The game requires the player to explore an underground map, run across platform layouts, jump over open gaps, gather ancient relics, avoid obstacles, and locate the final exit portal safely.

## 2.0 Project Aim and Objectives

### 2.1 Aim
To build, evaluate, and document a stable 2D platformer prototype in Godot that satisfies core software engineering principles—specifically low class coupling, modular scenes, and solid input validation.

### 2.2 Objectives
* **Requirements & Sprints:** Organize assignment constraints into real Scrum User Stories and a manageable Product Backlog.
* **Scene Architecture:** Use Godot's node nesting tree to separate player logic, level design, UI, and collectible items.
* **Physics & Interactions:** Code responsive movement profiles by adapting Godot’s built-in vector functions.
* **State Operations:** Set up a clean layout linking the Main Menu, active level loops, Game Over screens, and Victory screens.
* **Tests:** Run systematic playtests to prove the code matches our original assignment requirements.

## 3.0 Game Concept & Target Audience

### 3.1 Game Concept
Platform Quest balances classic 2D retro design with modern game feel. The level layout provides a natural difficulty progression. 

### 3.2 Target Audience 

#### Casual Gamers
* **Characteristics:** Want immediate visual feedback, straightforward layouts, and easy-to-learn control schemes.
* **Design Match:** Configured intuitive directional keyboard layouts along with clear score displays.

#### Nostalgic Platform Game Fans
* **Characteristics:** Players who love 2D pixel styles, strict jump weight, and a fair mechanical challenge.
* **Design Match:** Applied crisp *Nearest Neighbor* filters to pixel art sheets and tuned gravity curves to match retro gameplay.

#### Students & Young Adults (Aged 18–25)
* **Characteristics:** Highly sensitive to sticky collisions, poor hitboxes, or loose floaty movement.
* **Design Match:** Fine-tuned collision boxes and grounded checks so player movement inputs respond instantly.

## 4.0 Overall Specification & Minimum Viable Product (MVP)

### 4.1 Core Features (The MVP)
To keep the project scope realistic while ensuring all grading parameters are achieved, the core features include:
* **Bidirectional Movement:** Horizontal tracking connected directly to player arrow or `A`/`D` keys.
* **Grounded Jump Vectors:** Vertical physics checked against the floor to prevent infinite mid-air jumps.
* **Static Layer Colliders:** Setting up terrain layer layers so the player interacts properly with walls and solid paths.
* **Relic Tracking:** Intercepting overlapping boundaries to update point counts before safely freeing the item instance.
* **Basic Hazards:** Dedicated contact triggers that immediately load failure states.
* **UI Screen Overlays:** Clean canvas layers for the Main Menu, Game Over screen, and a final Level Clear prompt.

### 4.2 Optional/Extended Scope Features
* **Dynamic Camera Bounds:** Adding a `Camera2D` smoothing offset to trace player positions comfortably.
* **Audio Feedback Streams:** Connecting node streams to trigger unique sound effects whenever a player jumps or collects items.

### 4.3 Explicit Acceptance Criteria
The prototype is considered complete and operational only when:
1. The character moves left or right instantly on input and cuts speed immediately when keys are released.
2. The vertical jump only triggers when the player node's floor check is verified as true.
3. Overlapping a danger tile immediately halts inputs and switches the scene to the Game Over template.
4. Touching the exit gate stops physics updates and opens the Level Win overlay menu.

## 5.0 User and System Requirements

### 5.1 User Requirements
* **.1:** The player must control movement smoothly using responsive keyboard actions.
* **.2:** The player must be able to tell platforms, collectible items, and danger zones apart visually.
* **.3:** The player must see their point score update immediately on the screen interface.
* **.4:** The player must be able to restart the game loop from the failure screen without the software crashing.

### 5.2 System Requirements
* **.1:** The engine must read hardware inputs (`A`, `D`, `Space`, `W`) in real time.
* **.2:** The system must apply an acceleration downward when the character is not resting on floor geometry.
* **.3:** The application must utilize Godot's 2D collision layer masks to handle entity overlaps.
* **.4:** The script pipeline must update active point variables on relic collections and push changes to the string UI node.
* **.5:** The engine must handle scene reloads or menu swaps cleanly without leaking active assets in memory.

### 5.3 Non-Functional Requirements
* **.1 Performance:** The game loop must maintain a smooth framerate target on typical computer setups.
* **.2 Maintainability:** Code must be split into distinct scripts (e.g., `player.gd`, `relic.gd`) to keep code modular and clean.
* **.3 Robustness:** Collision checks must run reliably to keep characters from clipping through floor tiles or getting stuck in wall boundaries.

## 6.0 Scrum-Style User Stories

| ID | Priority | User Story Description | Purpose / Technical Justification |
| :--- | :--- | :--- | :--- |
| **US.1** | High | As a player, I want responsive movement controls so that I can explore the environment effectively. | Formulates the fundamental baseline for level traversal and mechanical validation. |
| **US.2** | High | As a player, I want to jump onto platforms so that I can access different parts of the level. | Grants vertical access across uneven spatial geometry, satisfying core platformer assumptions. |
| **US.3** | High | As a player, I want to collect relics so that I can work towards completing the objective. | Sets clear progression drivers and establishes score tracking. |
| **US.4** | High | As a player, I want hazards to create consequences for mistakes so that the game feels challenging. | Instantiates risk, introducing explicit win/lose tension metrics. |
| **US.5** | High | As a player, I want a clear level objective so that I know how to complete the game. | Establishes the terminal phase of the gameplay loop, enabling successful state migration. |
| **US.6** | Medium | As a player, I want visual feedback when collecting relics so that I know my progress is tracked. | Drives player engagement by reflecting real-time inventory adjustments on screen. |
| **US.7** | Medium | As a player, I want a main menu so that I can start or restart the game easily. | Provides clean application entry and exit setups, aligning with usability standards. |
| **US.8** | Medium | As a player, I want a game over screen so that I understand when I have failed. | Confirms a terminal loss state clearly and resets player variables cleanly. |
| **US.9** | Medium | As a player, I want a win screen so that I receive confirmation of completing the level. | Validates skill performance and closes out the active gameplay loops successfully. |
| **US.10**| Low | As a player, I want additional levels so that the game offers more content in future versions. | Evaluates structural scalability across the scene management architecture. |

## 7.0 Scrum Product Backlog

| Backlog ID | Associated Feature | Priority | Technical Definition of Done (DoD) | Evaluation Metric & Verification Method |
| :--- | :--- | :--- | :--- | :--- |
| **B.1** | Player Movement | High | Velocity values change cleanly inside `_physics_process`. Character flips horizontally without shifting collision shapes. | Tap `A`/`D`. Monitor node properties to ensure position transformations align correctly. |
| **B.2** | Jump Engine | High | Upward velocities fire properly on input. Godot's physics fall calculations drop the character back down smoothly. | Hit `Space`. Verify jump only works from solid surfaces and blocks infinite air-jumping. |
| **B.3** | Map Tile Colliders | High | Tiles use a clean static collision configuration mapped to our primary Ground layer. | Guide actor over drops. Confirm they stay securely on platforms without sinking through tile seams. |
| **B.4** | Hazard Detection | High | Traps trigger area entry notifications, immediately running a reset or death sequence. | Move character into spikes. Ensure the player input loops cut out instantly. |
| **B.5** | AI Patrol Logic | High | Guard items pace predictably between path markers and switch directions at walls. | Observe automated movement. Confirm edge turns work and contact hits the player fail loop. |
| **B.6** | Relic Collection | Medium | Item areas register player overlap, increase point scores, and call `queue_free()` safely. | Walk over a relic. Verify the item leaves the scene tree and points count up on screen. |
| **B.7** | Core UI Canvas | Medium | Displays real-time score lines and brings up menu modules depending on the game state. | Check text readouts during play. Verify the string prints correct point adjustments. |
| **B.8** | Menu Lifecycles | Medium | The `GetTree().change_scene_to_file()` method handles file routing without loading hangs. | Swap screen modes. Confirm clean scene changes between active levels and menus. |
| **B.9** | Exit Triggers | High | Endzone layers track player entry, pause level updates, and render the final Win screen. | Step into the finish zone. Confirm active physics stop and the completion UI loads. |


## 9.0 Environment, Gameplay, and Player Motivation Loops

### 9.1 Environment Layout
Levels are constructed by placing modular tile layouts alongside specific hazard zones. The physical progression follows three key design zones:
1. **Intro Zone:** A flat, safe area used to test basic left/right running controls and single vertical jumps.
2. **Ascent Zone:** Vertical platform arrangements that require timed jumps over open gaps.
3. **Danger Corridor:** Narrow routes guarded by patrolling hazards, where players must time their movements carefully to reach the final exit.

### 9.2 The Gameplay Framework
<img width="457" height="212" alt="image" src="https://github.com/user-attachments/assets/e08cfdc3-10d2-4d78-9450-28a172c97f72" />


### 9.3 Player Motivation Loop
* **Current State:** The player enters a room with low scores and needs to find an exit path safely.
* **Core Need:** Navigating complex geometric gaps while safely avoiding incoming threats.
* **The Challenge:** Missing jumps results in instant death, requiring players to build muscle memory and master the controls.
* **The Reward:** Picking up shining relics increments the UI score counters, while reaching the exit awards a clear victory screen.

## 10.0 Game Rules & Logic System
* **Spawn Coordinates:** The player initializes at set positions $(X_0, Y_0)$ whenever a level scene loads.
* **Movement Boundaries:** Horizontal running is restricted by solid walls, while vertical jumping requires `is_on_floor()` to return true.
* **Relic Rules:** Overlapping an item asset flags it as picked up, adds +1 to points, and removes the instance. Collected objects remain gone for the rest of that run.
* **Failure Actions:** Striking an enemy hitbox or landing on spikes calls the scene reset tool and opens the Game Over menu overlay.
* **Victory States:** Passing through the end portal trigger stops active play logic, clears the level, and shows the Win screen canvas.

## 11.0 State Management Architecture
<img width="374" height="319" alt="image" src="https://github.com/user-attachments/assets/bce3edea-7471-41d5-afa3-48e71db18362" />


## 12.0 Engine, Platform, and Input Maps

### 12.1 Engine Environment & Scripting
* **Engine Environment:** **Godot Engine (v4.x)** (Chosen for its lightweight footprint, dedicated 2D node workflows, and clean scene instancing toolset).
* **Script Framework:** **GDScript** (High-level, indentation-based language designed specifically to interact cleanly with Godot's internal engine loops).

### 12.2 Target Build Environment
* **Platform Target:** Desktop PC machines running regular keyboard hardware setups.
* **Project Input Map Assignments:**
  * `move_left`: Mapped to `A` and `Left Arrow` keys.
  * `move_right`: Mapped to `D` and `Right Arrow` keys.
  * `jump`: Mapped to `Spacebar` and `W` keys.

## 13.0 Core Algorithmic Pseudocode (GDScript Structure)
<img width="575" height="270" alt="image" src="https://github.com/user-attachments/assets/a0f006ca-d9d7-4f0b-9cb3-e8f6491f009d" />
<img width="328" height="140" alt="image" src="https://github.com/user-attachments/assets/edcfbc19-02ec-4d76-ad81-6c12e696b71c" />
<img width="262" height="72" alt="image" src="https://github.com/user-attachments/assets/0a62bfb0-6e76-4c4c-965f-2ee1681bffa3" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/d3ab2079-19ce-412f-8631-8397ab5c784c" />
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/b0139327-48b9-41b7-9234-ea496ac62fe7" />


## 14.0 Project Management & Development Records
###14.1 Iterative Development Log
Day 1: Set up Godot 4 project directories. Established subfolders for assets, scenes, and scripts while configuring the repository.

Day 2: Imported 2D graphics sheets and set up our player scene using an AnimatedSprite2D node with idle and run animations.

Day 3: Programmed directional movement code within _physics_process. Built real-time key capture handling.

Day 4: Configured custom Project Input Maps. Fixed air-jumping issues by using Godot's built-in is_on_floor() validation check.

Day 5: Created world terrain layouts using TileMapLayer. Connected physics shapes to tiles and built item tracking masks using an Area2D setup.

Day 6: Tied relic collection scripts directly to control canvas texts. Ran end-to-end scene navigation checks and finalized text documentation.

## 15.0 review
While the core mechanics are operational, the prototype currently exhibits three distinct structural limitations due to development scope constraints:

Unbounded Character Scale: The player character's structural node scale is currently oversized relative to the overall game window and platform tiles. While this does not break collision accuracy, it restricts the camera's viewable play area and will require downscaling to match standard platformer proportions in future builds.

Single-Level Constraint: The project features only one fully realized level layout. There is no multi-stage scene management or level-to-level progression implemented at this stage.

Absence of Terminal Game Loops (No Endgame State): The game does not currently feature a working win or lose condition. While the player can navigate the architecture and jump off ledges, stepping into hazard zones or reaching the end of the level layout does not stop physics or trigger UI menu screens. The game currently runs as an infinite testing sandbox.
| Feature | Implementation Status | Functional Description / Current State |
| :--- | :--- | :--- |
| **Bidirectional Movement** | :white_check_mark: **Fully Operational** | Captured via keyboard axis mapping (`left`, `right`). The character moves smoothly, though the sprite is currently too large for the environment. |
| **Vertical Jumps** | :white_check_mark: **Fully Operational** | Ground-checked physics calculation loop using `is_on_floor()`. Successfully triggers an upward velocity vector (`JUMP_VELOCITY = -850.0`). |
| **Ledges & Platforms** | :white_check_mark: **Fully Operational** | Solid physics colliders applied to the level geometry. The character interacts properly with floors and can jump onto or off elevated ledges. |
| **Level Textures** | :white_check_mark: **Fully Operational** | Godot TileMap structures have visual textures properly applied to clearly define the playable terrain from the background. |
| **Multi-Stage Progression** | :x: *Not Implemented* | The game does not change scenes or progress. It is strictly limited to a single-level testing sandbox. |
| **Terminal Game Loops** | :x: *Not Implemented* | There is no working endgame state. Reaching the end of the level or falling into gaps does not trigger a Win or Game Over screen. |

## refrences 
https://www.youtube.com/watch?v=oED12Mo2018&list=PLjcN1EyupaQl0W9bQZR5i-ky7ukJZmL0Z

## 12.0 Sprint 2 Work and Backlog Changes

### 12.1 Sprint 2 Goals
For Sprint 2, the main goals are fixing the bugs from Sprint 1 and making sure the game runs smoothly. Since time is short, we are focus on fixing what we have instead of adding too many hard new systems.

**What we are fixing in Sprint 2:**
1. **Fixing the Player Size:** Changing the character scale down in the inspector so they look normal next to the platforms.
2. **Fixing the Code Error:** Fixing the script error on line 13 where assigning a text string broke the animation.
3. **Cleaning up the Backlog:** Reviewing the list of features, removing the hard stuff we won't have time for, and keeping only what i can actually deliver.

### 12.2 Product Backlog Review & Scope Changes

We changed the plan to keep things realistic for this submission. We completely removed the enemy AI and the Main Menu screens from the project scope to keep our code and scene setup simple. We also put off the traps, collectibles, and level endings so we could focus 100% on making sure the running, jumping, and textured platforms work perfectly.

| Backlog ID | Feature | Priority | Status | Notes / What We Did |
| :--- | :--- | :--- | :--- | :--- |
| **B.1** | Player Movement | High | **COMPLETED** | Running left and right works perfectly. |
| **B.2** | Jumping | High | **COMPLETED** | Normal jumping works on the floor. No double jumping. |
| **B.3** | Level Ledges and Art | High | **COMPLETED** | Platforms have textures and solid collisions so you don't fall through. |
| **B.4** | Traps / Hazards | High | **POSTPONED** | spikes have not been added yet, currently focusing on the main functionality of the game. |
| **B.5** | Enemy AI Patrol | High | **REMOVED** | **Dropped from project scope.** Deleted to keep the code simple. |
| **B.6** | Relic Collection | Medium | **POSTPONED** | Picking up items was put off due to time limits. |
| **B.7** | Game Score UI | Medium | **POSTPONED** | The on-screen point counter text was put off. |
| **B.8** | Main Menu Screens | Medium | **REMOVED** | **Dropped from project scope.** Cancelled to let the player load straight into the level. |
| **B.9** | Level Ending / Exit Door | High | **POSTPONED** | The door does not load a new level yet. |


### 12.3 Sprint 2 Progression & Visual Evidence

#### Phase 1: Sprite Scaling & Collision Adjustment
* **The Problem:** The imported player character sprite was massive—over 3x the size of the environment platforms—making the game unplayable as a platformer.
