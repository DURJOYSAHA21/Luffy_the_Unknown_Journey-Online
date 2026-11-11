# Luffy: The Unknown Journey

*One morning a boy named Luffy wakes up, sits down at his game console, presses
START, and gets pulled into the World of Chaos. A collapsing fortress, a dark
labyrinth, a sea storm, an island of monsters and a burning volcano stand
between him and home, and on top of the volcano waits the Chaos King. When he
finally wins, he's back on his beanbag. Was it all a dream?*

A 2D story adventure written in **C++ with OpenGL and freeglut** for our Computer
Graphics course (8th semester): a title screen, an animated opening in Luffy's
bedroom, five levels with five different kinds of gameplay, a chapter card
before each one, one set of lives for the whole journey, a final boss, sound
effects, and an ending back home. The full story is in [STORY.md](STORY.md).

Everything on screen is drawn with OpenGL shapes and every sound is generated in
code: no images, sprites, sound files or game engine.

**▶ [Play in your browser](https://durjoysaha21.github.io/Luffy_the_Unknown_Journey-Online/play/)**
(no install needed; works in Chrome, Edge and Firefox)

> Fan project: the hero is a tribute to Luffy from *One Piece* (Eiichiro Oda).
> Not affiliated with or endorsed by the creators of One Piece.

![Title screen](docs/screenshots/00-title.png)

## The journey

| | Scene | What happens | Made by |
|---|---|---|---|
| | **Title screen** | LUFFY: THE UNKNOWN JOURNEY, press SPACE to start | **Durjoy Saha** |
| 0 | **Prologue** (cutscene) | Luffy wakes up, presses START on his console and is pulled through a portal | **Durjoy Saha** |
| 1 | **The Dungeon** | Open 5 locked doors, each a different puzzle. Taking the key sets off an **earthquake**: dodge the falling rocks to the exit | **Durjoy Saha** |
| 2 | **The Star Labyrinth** | A **dark maze lit only by Luffy's torch**. Collect stars, avoid the guardians, open the treasure box, then **escape before the labyrinth collapses** | Rifat |
| 3 | **Breaking the Blockade** | Steer past enemy ships to the island while a **storm** rolls in and the ships fire **cannonballs** | Fahim |
| 4 | **The River of Monsters** | The monsters **patrol**; jump on them to defeat them, collect coins | Soriya |
| 5 | **The Volcano Showdown** | Defeat the Chaos Crew among **erupting lava bombs**, then the **Chaos King** rises from the lava | Keya |
| 6 | **Epilogue** (cutscene) | Back in the bedroom: GAME OVER… or is it? A golden star lies on the floor. THE END + credits | **Durjoy Saha** |

The levels were made by the team. The story mode, the upgrades and the boss are
in `story.h` (see [CHANGES.md](CHANGES.md)).

| Morning in the bedroom | Pulled into the game |
|---|---|
| ![Bedroom](docs/screenshots/0a-bedroom.png) | ![Portal](docs/screenshots/0b-portal.png) |
| **Chapter card** | **Dungeon: the earthquake** |
| ![Chapter card](docs/screenshots/0d-chapter-3-card.png) | ![Earthquake](docs/screenshots/1b-earthquake.png) |
| **Labyrinth: torch light, collapsing** | **Blockade: the storm** |
| ![Maze](docs/screenshots/2-maze.png) | ![Sea](docs/screenshots/3-sea.png) |
| **River: stomping a monster** | **The volcano** |
| ![River](docs/screenshots/4-river.png) | ![Volcano](docs/screenshots/5-volcano.png) |
| **The Chaos King** | **Back home** |
| ![Chaos King](docs/screenshots/5b-chaos-king.png) | ![Ending](docs/screenshots/6-ending-star.png) |

## Lives

One counter for the whole journey: **5 hearts**, shown at the top of every
level. The screen flashes red and shakes when a heart is lost:

| Level | Costs a heart |
|---|---|
| Dungeon | a spike ball, a falling rock |
| Labyrinth | a guardian (back to the start), or the collapse timer running out |
| Blockade | crashing into a ship, a cannonball |
| River | monsters, once the health bar is empty |
| Volcano | HP reaching 0 (fire, lava, falling, lava bombs, fireballs, the boss) |

At 0 hearts it's **Game Over**: press **R** to try the same chapter again with 5
hearts, or ESC to quit.

| Game Over | Victory |
|---|---|
| ![Game over](docs/screenshots/game-over.png) | ![Victory](docs/screenshots/victory.png) |

## Level 1: The Dungeon (Durjoy Saha)

A side-scrolling level, 4000 units wide, with a camera that follows the
player. It has a day/night cycle (moving sun, moon and clouds), rain, torches
and spinning gears. Five doors block the way:

| Door | Puzzle |
|---|---|
| 1 | Carry the two crates (**E** to pick up / put down) onto the two red pressure plates |
| 2 | A panel shows 4 random symbols like `( ) % !`. Each one is a Shift+number key (`!` = 1 … `)` = 0), so type the 4 digits and press **Enter**. The code is different every game |
| 3 | Pull the lever to ride the lift up and over the wall |
| 4 | Four levers must be pulled in the right order; a hint is painted on the wall |
| 5 | Use the launch pad (**H**) to reach the key, dodge two swinging spike balls, and unlock the last door |

Taking the key sets off an earthquake: rocks fall from the ceiling, and a
growing shadow on the floor shows where each one will land.

![Level 1: the dungeon](docs/screenshots/1-dungeon.png)

## Controls

| Where | Keys |
|---|---|
| Anywhere | **M** sound on/off |
| Title screen | **Space** start · **ESC** quit |
| Prologue, chapter cards | **Space** or **Enter** to continue (or skip the cutscene) |
| 1 Dungeon | **W/A/S/D** move · **Space** jump · **E** crates and levers · number keys + **Enter** for the code · **H** launch pad |
| 2 Labyrinth | **Arrow keys** move · **B** open the treasure box (then type the password, **Enter**) |
| 3 Blockade | **Arrow keys** steer · **R** try again after a crash |
| 4 River | **A/D** move · **W** or **Space** jump (land on monsters to defeat them) |
| 5 Volcano | **hold A/D** run · **W** jump · **J** sword (left) · **K** knife (right) · after winning: **Space** go home |
| Epilogue | **Space** skip to THE END · **ESC** quit |
| Game Over (any level) | **R** try this chapter again · **ESC** quit |

## Computer graphics techniques used

- **Primitives:** points, lines, triangles, quads, polygons, triangle fans and strips
- **Circles, arcs and stars** from trigonometry: clouds, sun, moon, gears, coins, hearts, the golden star
- **2D transformations:** `glTranslatef` / `glRotatef` / `glScalef` / `glPushMatrix`, including reusing one hero model at any size and angle and **mirroring** it (a negative y scale) for the maze's upside-down coordinates
- **Hierarchical modelling:** the Chaos King's arms swing around his shoulders inside his own transform
- **Radial light mask:** the labyrinth's darkness is two triangle strips with per-vertex alpha, leaving a flickering circle of torch light around Luffy
- **Alpha blending:** fog, glows, fades in and out of white, the red hurt flash, smoke and rain
- **Colour interpolation:** gradient skies from per-vertex colours (title screen, volcano)
- **Particle systems:** sparks, dust, explosions and rising embers, each with velocity, gravity and fading
- **Screen shake** by moving the viewport a few pixels per frame
- **Projectile physics:** cannonballs, lava bombs on arcs, fireballs aimed at the player
- **DDA line drawing** and **Cohen–Sutherland line clipping**, implemented by hand in the labyrinth
- **Scrolling camera** over a 4000-unit world in level 1
- **Stroke and bitmap fonts**, centred by their real pixel width so they fit every window size
- **Sound synthesis:** square, sine and triangle waves and noise written into WAV buffers in memory and played with `PlaySound`
- **Animation** driven by a 60 fps `glutTimerFunc` loop; time-based cutscene timelines

## Build and run

**Code::Blocks (what the course used):** open `TRY-improved.cbp` and press
**Build and run** (F9). It needs freeglut set up in Code::Blocks' MinGW.
`story.h` is included by `main.cpp`, so there's nothing extra to set up.

**Command line (MinGW g++ with freeglut):**

```bash
g++ main.cpp -o game.exe -lfreeglut -lopengl32 -lglu32 -lwinmm -lgdi32
./game.exe
```

If Windows says `freeglut.dll` is missing, copy it next to `game.exe`.

## Browser version

The same C++ code also compiles to **WebAssembly** with
[Emscripten](https://emscripten.org), so the game runs in any modern browser.
The built files are in `docs/play/` (`index.html`, `index.js`, `index.wasm`,
about 350 KB together).

**Put it online with GitHub Pages:** push the repo (including `docs/play/`),
then on GitHub open **Settings → Pages → Build and deployment**, choose
**Deploy from a branch**, branch **main**, folder **/docs**, and **Save**.
After a minute the game is at <https://durjoysaha21.github.io/Luffy_the_Unknown_Journey-Online/play/>.

**Rebuild it** after changing the code: install Emscripten once
(`emsdk install latest` and `emsdk activate latest`), then run
`web\build_web.bat` (it calls `em++` and then `web\fix_glemu.py`).

What the browser build needs, all switched on only for Emscripten (the
Code::Blocks build is unchanged):

| File | Why |
|---|---|
| `web/webcompat.h` | The browser's GLUT has no fonts and no `glRasterPos`, so text is drawn with a small pixel font (generated from Consolas). `GL_POLYGON` becomes a triangle fan. Colours are sent with every vertex, because the browser's emulation only colours the next vertex |
| `story.h` | Sounds play through the browser's Web Audio instead of `PlaySound` |
| `web/fix_glemu.py` | Emscripten 7.0.0 emits one line of its legacy-GL setup too early; this moves it (run automatically after each build) |
| `web/shell.html` | The web page around the game: title, scaling, controls; Space and the arrows don't scroll the page |

## What changed from the course version

This folder is a copy of the original course project (`../TRY`, untouched).
Every change is marked in `main.cpp`: `// [FIX n]` for bug fixes, `// [STORY]`
for the story mode and the upgrades. Details and test results are in
[CHANGES.md](CHANGES.md).

**Bug fixes**

1. **Level 1:** lives went negative with no Game Over (now handled by the journey's lives)
2. **Volcano:** defeating every enemy did nothing, so the game could never be won
3. **Volcano:** two enemies were invisible but still hurt you (wrong draw function after merging)
4. **Blockade:** after a crash the boat could still sail to the island and skip the level
5. **Labyrinth:** the wrong-password message gave the answer away
6. The window could open partly off-screen
7. **Labyrinth:** the maze showed the *boat* level's score (always 0) instead of its own
8. **Volcano:** birds flew through the control text
9. **Level 1:** the door-2 code wrote one byte past the end of its array
10. **River:** the checks used level 1's player position, so monsters, coins and the middle platform never reacted

**Story mode and upgrades** (`story.h`): title screen, opening cutscene, chapter
cards, one lives counter, ending cutscene with credits, sound effects,
particles and screen shake, the dark collapsing labyrinth, the sea storm and
cannonballs, patrolling river monsters, the dungeon earthquake, and a rebuilt
volcano with smooth controls, new art, lava bombs and the Chaos King.

## Team

| Member | Part |
|---|---|
| **Durjoy Saha** | Level 1 (dungeon), story, story mode and upgrades |
| Rifat | Level 2 (labyrinth) |
| Fahim | Level 3 (blockade) |
| Soriya | Level 4 (river) |
| Keya | Level 5 (volcano) |


© 2026 Durjoy Saha and team. All rights reserved. See [LICENSE](LICENSE).
