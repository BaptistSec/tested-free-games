# Tested Free Games for Ubuntu

Free and open-source games that we ran ourselves, with dated results, screenshots captured from the test runs, exact package versions, controls and known issues. Not another link list: every entry below was executed by us on the date shown.

Current scope: Ubuntu 22.04 LTS (Jammy), x86-64, packages from the official Ubuntu `universe` repository. First edition: 12 games, tested **7 November 2026**.

## How we test

For each game:

1. We resolve the full dependency closure with apt's own resolver (`apt-get install --download-only --print-uris`), so the packages tested are exactly the ones `sudo apt install` would fetch, in the same versions.
2. We extract the packages and run the game against them in an isolated filesystem namespace (overlayfs over the stock system) on Ubuntu 22.04.5 LTS, with a virtual display (Xvfb, 1280x800x24) and no audio device. This is not a literal `sudo apt install` on a desktop machine; it is a runtime test of apt's exact package set.
3. We capture screenshots from the live run and record whether the process stayed up, whether the screen responded to simulated keyboard/mouse input (xdotool), and anything that broke.
4. We audit the package's maintainer scripts (postinst etc.) for install-time actions. For all 12 games these only seed high-score files and register menu entries, so a real `sudo apt install` does the same thing plus those trivial steps.
5. Licence statements come from each package's own `/usr/share/doc/<package>/copyright` file, not from assumption.

Honest limits:

- No physical GPU and no sound card in the test environment. 3D games rendered in software; audio was disabled. Performance on real hardware will be better than anything you see here.
- Input is simulated (xdotool), not a human player. "Demo/attract mode" entries prove the game engine renders and runs a level by itself; they do not prove player controls. Where a control scheme is listed from the game's packaged documentation, it says so, and it means we did not exercise it in the automated run.
- Nothing here is a guarantee about other Ubuntu versions, Wayland sessions, or your hardware. It's a dated record of what ran, where, and how.

## Evidence levels

| Level | Meaning |
|---|---|
| **Gameplay screen reached** | Menus passed and an actual level/game screen rendered (start of play or attract/demo mode - the level column says which). |
| **Menu interaction verified** | Menu or intro screens visibly changed in response to simulated input. |
| **Launch verified** | Game launched, rendered its real menu/graphics, and stayed running. Input not exercised. |

## The games

| Game | Genre | Install command | Version tested | Evidence |
|---|---|---|---|---|
| [Freedoom Phase 2 (Crispy Doom)](#freedoom-phase-2--crispy-doom) | FPS | `sudo apt install crispy-doom freedoom` | 0.12.1 / engine 5.11.1 | **Gameplay screen reached** (level view) |
| [Nebulus (Toppler)](#nebulus-toppler) | Tower platform action | `sudo apt install toppler` | 1.3-1 | **Gameplay screen reached** (attract demo) |
| [LTris](#ltris) | Falling-block puzzle | `sudo apt install ltris` | 1.0.19-3build1 | **Gameplay screen reached** (demo mode) |
| [MadBomber](#madbomber) | Arcade catcher | `sudo apt install madbomber` | 0.2.5-8.1 | **Gameplay screen reached** |
| [Vodovod](#vodovod) | Pipe puzzle | `sudo apt install vodovod` | 1.10-5 | **Gameplay screen reached** |
| [BlockOut II](#blockout-ii) | 3D falling-block puzzle | `sudo apt install blockout2` | 2.5+dfsg1-1build1 | **Gameplay screen reached** |
| [Alex the Allegator 4](#alex-the-allegator-4) | Platform | `sudo apt install alex4` | 1.1-9 | **Menu interaction verified** (intro) |
| [Ceferino](#ceferino) | Arcade platform | `sudo apt install ceferino` | 0.97.8+svn37-2build1 | **Menu interaction verified** (intro/story) |
| [Powermanga](#powermanga) | Shoot 'em up | `sudo apt install powermanga` | 0.93.1-4 | **Launch verified** (menu rendered) |
| [Trackballs](#trackballs) | Marble-rolling 3D | `sudo apt install trackballs` | 1.3.3-1 | **Launch verified** |
| [Fillets-NG](#fillets-ng) | Logic puzzle | `sudo apt install fillets-ng` | 1.0.1-4build2 | **Launch verified** |
| [Pingus](#pingus) | Lemmings-style puzzle | `sudo apt install pingus` | 0.7.6-5.1 | **Launch verified** |

Every game also has an Ubuntu package page: `https://packages.ubuntu.com/jammy/<package-name>`.

---

### Freedoom Phase 2 / Crispy Doom

A complete free-content campaign for Doom II, played through the Crispy Doom engine.

- **Install:** `sudo apt install crispy-doom freedoom`, then run `crispy-doom -iwad /usr/share/games/doom/freedoom2.wad` (or the `freedoom2` launcher).
- **Licence:** game data under the Freedoom licence (BSD-style terms, per the package copyright file); engine GPL-2.0+.
- **Tested:** freedoom 0.12.1-2 with crispy-doom 5.11.1-1. Launched, the menu responded to simulated keys, and the engine loaded MAP15 and entered the first-person level view with HUD. Sound initialised (dummy driver).
- **Controls:** standard Doom layout (arrows to move, Ctrl to fire, Space to use, Shift to run), configurable with `crispy-setup`. From the engine's documentation; only menu keys were exercised in our run.
- **Upstream:** https://freedoom.github.io/ and https://github.com/fabiangreffrath/crispy-doom (both reachable at test time)

![Freedoom title screen](screenshots/freedoom-menu.png)
![Freedoom in-level view](screenshots/freedoom-level.png)

### Nebulus (Toppler)

Climb a rotating tower against the clock; a remake of the classic Nebulus/Tower Toppler.

- **Install:** `sudo apt install toppler`, run `toppler`.
- **Licence:** GPL-2.0+ (package copyright).
- **Tested:** 1.3-1. Menu rendered; after input the game entered its attract/demo mode showing the engine playing the tower itself. Player controls not exercised.
- **Controls (packaged man page, not exercised in our run):** cursor keys move; Space or Return selects, jumps, or throws a snowball.
- **Upstream:** https://gitlab.com/roever/toppler/ (reachable at test time)

![Nebulus menu](screenshots/toppler-menu.png)
![Nebulus demo gameplay](screenshots/toppler-demo.png)

### LTris

A polished Tetris-style falling-block game with a high-score chart and multiplayer options.

- **Install:** `sudo apt install ltris`, run `ltris`.
- **Licence:** GPL (package copyright; version text says GNU GPL, see `/usr/share/doc/ltris/copyright`).
- **Tested:** 1.0.19-3build1. Arrow keys navigated the menu into the New Game screen (verified by screenshot). Starting the default "Demo" game type launched the auto-played demo: the screenshots show the demo playing, score rising from 100 to 700 across a few seconds. Player controls not exercised.
- **Upstream:** http://lgames.sourceforge.net/index.php?project=LTris (reachable from our test network; one earlier check from elsewhere received a 403, likely bot filtering - the package page is the fallback)

![LTris menu](screenshots/ltris-menu.png)
![LTris demo gameplay](screenshots/ltris-gameplay.png)

### MadBomber

Kaboom!-style arcade catching: move the bucket, catch the bombs.

- **Install:** `sudo apt install madbomber`, run `madbomber`.
- **Licence:** GPL-2.0 (package copyright).
- **Tested:** 0.2.5-8.1. Menu rendered; selecting One Player with simulated keys reached the live game screen (bomber throwing bombs, buckets below).
- **Upstream:** http://www.newbreedsoftware.com/madbomber/ (reachable at test time)

![MadBomber menu](screenshots/madbomber-launch.png)
![MadBomber gameplay](screenshots/madbomber-gameplay.png)

### Vodovod

Connect pipes before the water starts flowing; a pipe-puzzle against the clock.

- **Install:** `sudo apt install vodovod`, run `vodovod`.
- **Licence:** GPL-2.0+ (package copyright).
- **Tested:** 1.10-5. Menu rendered; simulated keys started a new game and reached the Level 1 board with the pipe tray. Placing pipes (mouse work) not exercised.
- **Controls (in-game Help and packaged man page):** mouse places pipes; joystick configurable in Options. Not exercised beyond menu input.
- **Upstream:** the original project site is gone; the game is maintained in Debian/Ubuntu - https://tracker.debian.org/pkg/vodovod

![Vodovod menu](screenshots/vodovod-menu.png)
![Vodovod Level 1 board](screenshots/vodovod-gameplay.png)

### BlockOut II

Tetris in true 3D: rotate blocks in three axes and fill pits.

- **Install:** `sudo apt install blockout2`, run `blockout2`.
- **Licence:** GPL-2.0+ (package copyright).
- **Tested:** 2.5+dfsg1-1build1. Menu rendered; simulated keys started a "Flat Fun" game and the run progressed (score 34, 5 cubes played at capture). How much of that progress was our input versus automatic falling is unverified.
- **Controls (packaged man page, not verified in our run):** arrows and Space move the falling piece.
- **Upstream:** http://www.blockout.net/blockout2/ (reachable at test time)

![BlockOut II menu](screenshots/blockout2-menu.png)
![BlockOut II gameplay](screenshots/blockout2-gameplay.png)

### Alex the Allegator 4

A deliberately Game Boy-styled platformer: two-colour graphics, chiptune, short levels.

- **Install:** `sudo apt install alex4`, run `alex4`.
- **Licence:** GPL-2.0+ (package copyright).
- **Tested:** 1.1-9. Story intro rendered and advanced in response to key presses. Actual gameplay not reached in the automated run.
- **Controls (packaged man page, not exercised):** arrow keys move; jump and shoot (shooting unlocked once you find eggs); keyboard or joystick.
- **Upstream:** http://allegator.sourceforge.net/ (reachable at test time)

![Alex 4 intro](screenshots/alex4-intro.png)
![Alex 4 intro, later frame](screenshots/alex4-intro-2.png)

### Ceferino

Fast single-screen arcade platforming from the LosersJuegos team: aliens are stealing Don Ceferino's cows.

- **Install:** `sudo apt install ceferino`, run `ceferino`.
- **Licence:** GPL-2.0+ (package copyright).
- **Tested:** 0.97.8+svn37-2build1. Intro and comic story screens rendered and advanced after key presses. Actual gameplay not reached in the automated run.
- **Controls (packaged man page, not exercised):** menus with arrows + Return/Space; in game, Left/Right move, Up climbs stairs, Down crouches.
- **Upstream:** http://www.losersjuegos.com.ar/juegos/ceferino did not respond at test time (we don't know whether that's temporary); use the package page https://packages.ubuntu.com/jammy/ceferino

![Ceferino intro](screenshots/ceferino-menu.png)
![Ceferino story screen after input](screenshots/ceferino-after-input.png)

### Powermanga

Vertical-scrolling arcade shoot 'em up with power-ups and big sprites.

- **Install:** `sudo apt install powermanga`, run `powermanga`.
- **Licence:** GPL-3.0+ (package copyright).
- **Tested:** 0.93.1-4. Launched and rendered its animated menu (PLAY / ORDER / ABOUT / QUIT). Note: a starfield intro runs for several seconds before the menu appears; first launch is not hung, just slow. Menu input not exercised.
- **Controls (packaged docs, not exercised):** arrow keys move, Space fires, Ctrl confirms; Ctrl+Q quits.
- **Upstream:** http://linux.tlk.fr/games/Powermanga/ (reachable at test time)

![Powermanga menu](screenshots/powermanga-menu.png)

### Trackballs

Guide a marble through tilted 3D levels, in the spirit of Marble Madness.

- **Install:** `sudo apt install trackballs`, run `trackballs`.
- **Licence:** GPL-2.0+ (game; package copyright also lists the Ethymonics Free Music License for bundled music).
- **Tested:** 1.3.3-1. Launched and rendered its menu over an animated 3D backdrop. Input response unconfirmed; gameplay not reached in the automated run.
- **Controls (packaged man page, not exercised):** mouse steers the ball; sensitivity adjustable in Settings.
- **Upstream:** https://trackballs.github.io/ (reachable at test time)

![Trackballs menu](screenshots/trackballs-menu.png)

### Fillets-NG

Sokoban-like logic puzzles: push objects around to free two fish, with deadpan commentary.

- **Install:** `sudo apt install fillets-ng`, run `fillets`.
- **Licence:** GPL-2.0 (game and data); see `/usr/share/doc/fillets-ng/copyright` for full detail including packaging terms.
- **Tested:** 1.0.1-4build2. Launched and rendered its illustrated world-map level select. Input not exercised.
- **Controls (packaged man page, not exercised):** arrow keys move the current fish, Space switches fish, Backspace restarts the level, F5 toggles the move counter.
- **Upstream:** http://fillets.sourceforge.net/ (reachable at test time)

![Fillets-NG world map](screenshots/fillets-ng-menu.png)

### Pingus

A free Lemmings-style puzzle game with penguins: assign actions, guide the crowd to the exit.

- **Install:** `sudo apt install pingus`, run `pingus`.
- **Licence:** GPL-2.0+ (package copyright).
- **Tested:** 0.7.6-5.1. Launched and rendered its main menu (Story / Levelsets / Editor / Options). This is the older 0.7.x stable branch, still shipped in Debian/Ubuntu. Menu is mouse-driven; input not exercised in the automated run.
- **Upstream:** http://pingus.seul.org/ (reachable at test time)

![Pingus menu](screenshots/pingus-menu.png)

---

## Notes

- Every screenshot in `screenshots/` was captured from our own test run on 7 November 2026; nothing is copied from upstream marketing material. Screenshots depict the games and remain subject to each game's own licence; they are included as test evidence.
- All install commands use the Ubuntu `universe` repository, which must be enabled (it is by default on desktop Ubuntu).
- Text in this repository is MIT-licensed (see LICENSE).
- Planned next: more games, exercising real gameplay controls for every entry, a Windows edition, and re-dating entries as new Ubuntu releases land.
