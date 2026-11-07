# Tested Free Games for Linux - run-tested on Ubuntu

Ten of the best free and open-source games for Linux, each one run by us on Ubuntu 22.04 LTS (tested 7 November 2026), plus 12 more that passed the same test. Every pick tells you why it's worth your time, gives one command to install and start, says what we verified, and names any catch. Screenshots and full test notes sit under each game further down.

What "verified" means here: we ran every game in an isolated test environment (no human player, virtual display, no sound), so "gameplay" can mean the game's own auto-played demo, and listed controls come from the game's own documentation unless marked exercised. Full method at the bottom. If a command says the package is not found, your Ubuntu variant may have the universe repository disabled - run `sudo add-apt-repository universe && sudo apt update`, then try again.


## The picks

### SuperTuxKart - the most complete free kart racer

```bash
sudo apt install supertuxkart && supertuxkart
```

Story mode, split-screen and online racing. Verified: launched to its first-run setup in our test. Catch: Ubuntu 22.04 carries 1.3; upstream is at 1.5. [Details and screenshots](#supertuxkart)

### 0 A.D. - full-scale ancient-warfare RTS

```bash
sudo apt install 0ad && 0ad
```

Real-time strategy with campaigns and multiplayer. Verified: launched and initialised in our no-GPU test env (launch-level only, modified env - see notes). Catch: Ubuntu 22.04's 0.0.25b is three releases behind upstream (Release 28). [Details](#0-ad)

### OpenTTD - transport empire building

```bash
sudo apt install openttd openttd-opengfx openttd-opensfx && openttd
```

The open Transport Tycoon successor, deep and actively developed. Verified: a new game map generated and ran in our test. Catch: the graphics/sound packs are separate packages (already in this command). [Details and screenshots](#openttd)

### Battle for Wesnoth - turn-based fantasy strategy

```bash
sudo apt install wesnoth && wesnoth
```

Sixteen official campaigns of hex-grid tactics, plus multiplayer. Verified: main menu rendered and responsive. Catch: 22.04 has 1.16; upstream stable is 1.18.x. [Details and screenshots](#battle-for-wesnoth)

### Minetest - open voxel sandbox

```bash
sudo apt install minetest && minetest
```

Minecraft-style building and survival with mods and multiplayer. Verified: we spawned into a generated world and walked in it. Catch: 22.04's 5.4.1 is old and upstream is now called Luanti (5.17) - check server version rules before playing online. [Details and screenshots](#minetest)

### Endless Sky - space trading and combat

```bash
sudo apt install endless-sky && endless-sky
```

Escape Velocity-style trading, fights and a long story. Verified: main menu rendered. Catch: 22.04 has 0.9.8; upstream is at 0.11.4. [Details and screenshots](#endless-sky)

### SuperTux - classic jump-and-run platforming

```bash
sudo apt install supertux && supertux2
```

A Mario-style platformer with a full story mode. Verified: menus navigated to the story world map in our test. Catch: the run command is `supertux2`, not `supertux`. [Details and screenshots](#supertux)

### Hedgewars - Worms-style artillery chaos

```bash
sudo apt install hedgewars && hedgewars
```

Turn-based hedgehog artillery with solo missions and multiplayer. Verified: first-run prompt and menu rendered. Catch: none significant; 1.0.0 is the current upstream release. [Details and screenshots](#hedgewars)

### Teeworlds - fast 2D multiplayer shooter

```bash
sudo apt install teeworlds && teeworlds
```

Grappling-hook arena shooting, multiplayer only. Verified: main menu rendered (0.7.5). Catch: 0.7.5 (2020) is the last official release; the community fork DDraceNetwork (DDNet) is where active development continues. [Details](#teeworlds)

### Freedoom Phase 2 - free Doom II campaign (FPS)

```bash
sudo apt install crispy-doom freedoom && crispy-doom -iwad /usr/share/games/doom/freedoom2.wad
```

Reached the actual in-level first-person view in our test.


## The games, with proof

### SuperTuxKart

Kart racing with a story mode, local split-screen and online play. The most polished free racer on Linux.

```bash
sudo apt install supertuxkart && supertuxkart
```

- **Licence:** GPL-3+ (code); data under free licences including CC-BY-SA and zlib (per the package copyright files).
- **Tested (7 Nov 2026):** supertuxkart 1.3+dfsg1-3. Launched and rendered its first-run flow: local/online account creation, then a consent prompt about connecting to the internet for add-ons and update notices. Software OpenGL (llvmpipe), no audio device.
- **Version note:** Ubuntu 22.04 carries 1.3; upstream's current release is 1.5 (per https://supertuxkart.net/Download, checked 7 Nov 2026). Single-player is unaffected; online racing may require matching versions.
- **Upstream:** https://supertuxkart.net

![SuperTuxKart first-run account setup](screenshots/supertuxkart-firstrun.png)

### 0 A.D.

Real-time strategy: build a civilization, raise armies, fight campaigns or multiplayer matches.

```bash
sudo apt install 0ad && 0ad
```

- **Licence:** GPL-2.0+ (code), CC-BY-SA-3.0 (data) per the package copyright file.
- **Tested (7 Nov 2026):** 0ad 0.0.25b-2. The game launched, opened its window and initialised its engine (confirmed in its log), and stayed running. The main menu had not finished drawing after ~95 seconds under software rendering, so this is launch-level evidence only. **Modified-environment result:** 0 A.D. refuses to start as root, and our isolation namespace maps the test user to root, so for this one game we presented a non-root user id via an `LD_PRELOAD` shim. On a normal desktop install none of that applies.
- **Version note:** Ubuntu 22.04 carries 0.0.25b ("Alpha 25b"); upstream's current release is Release 28 "Boiorix" (per https://play0ad.com/download/, checked 7 Nov 2026) - three releases ahead, so expect meaningful differences.
- **Upstream:** https://play0ad.com

### OpenTTD

The open-source successor to Transport Tycoon Deluxe: build rail, road, air and shipping networks.

```bash
sudo apt install openttd openttd-opengfx openttd-opensfx && openttd
```

- **Licence:** GPL-2.0 (per the package copyright file); the OpenGFX/OpenSFX content packs are free as well.
- **Tested (7 Nov 2026):** openttd 12.1-2build1 with openttd-opengfx 7.1-1 and openttd-opensfx 1.0.3-2. Starting a new game directly (`openttd -g`) generated a map and reached the in-game UI (toolbar, date, treasury). The game warned "no compatible GPU found, hardware acceleration disabled" - expected in our no-GPU test environment; it renders in software.
- **Catches:** the base `openttd` package ships no graphics or sound - install the two content packages as in the command above, or use the in-game online content downloader. Music playback additionally needs a General MIDI soundfont (the `timgm6mb-soundfont` package is pulled in by this install; on minimal systems music may stay silent).
- **Version note:** Ubuntu 22.04 carries 12.1; upstream's latest stable is 15.3 (per https://www.openttd.org, checked 7 Nov 2026). Savegames and multiplayer are version-sensitive.
- **Upstream:** https://www.openttd.org

![OpenTTD new game started](screenshots/openttd-game.png)

### Battle for Wesnoth

Turn-based strategy on hex maps: sixteen official campaigns, plus online multiplayer.

```bash
sudo apt install wesnoth && wesnoth
```

- **Licence:** GPL-2.0+ (per the package copyright file).
- **Tested (7 Nov 2026):** wesnoth 1:1.16.2-2. Main menu rendered (version 1.16.2 shown). On a real install the `wesnoth` command is an alternatives symlink to `wesnoth-1.16` created by the package's postinst; our extraction method skips maintainer scripts, so in the test we launched `wesnoth-1.16` directly.
- **Version note:** Ubuntu 22.04 carries 1.16.2; upstream's stable branch is 1.18.x (latest 1.18.8 per the official release announcements, checked 7 Nov 2026).
- **Upstream:** https://www.wesnoth.org

![Wesnoth main menu](screenshots/wesnoth-menu.png)

### Minetest

Open voxel sandbox: mining, building, survival, mods and multiplayer servers.

```bash
sudo apt install minetest && minetest
```

- **Licence:** LGPL-2.1+ (engine); bundled game content CC-BY-SA-3.0/MIT (per the package copyright files).
- **Tested (7 Nov 2026):** minetest 5.4.1+repack-2build1. Started a fresh world directly (`minetest --go`): spawned into a generated snowy landscape with the hearts/hotbar HUD and walked forward under simulated keyboard input. The main menu also rendered in a separate run.
- **Version note:** upstream renamed the project to **Luanti** and is at 5.17.0 (per https://www.luanti.org, checked 7 Nov 2026). Ubuntu 22.04's minetest 5.4.1 is far behind; some multiplayer servers require a newer client.
- **Upstream:** https://www.luanti.org

![Minetest in-game first-person view](screenshots/minetest-game.png)

### Endless Sky

Space trading, combat and exploration in the style of Escape Velocity, with a long story campaign.

```bash
sudo apt install endless-sky && endless-sky
```

- **Licence:** GPL-3+ (code); data CC-BY-SA-4.0 and other free licences (per the package copyright files).
- **Tested (7 Nov 2026):** endless-sky 0.9.8-1.2. Main menu rendered with version shown; pilot creation is one click past it.
- **Version note:** Ubuntu 22.04 carries 0.9.8; upstream's latest stable is v0.11.4 (per https://github.com/endless-sky/endless-sky/releases/latest, checked 7 Nov 2026).
- **Upstream:** https://endless-sky.github.io

![Endless Sky main menu](screenshots/endless-sky-menu.png)

### SuperTux

A Mario-style jump-and-run with a full story mode across two worlds.

```bash
sudo apt install supertux && supertux2
```

- **Licence:** GPL-3+ (code); data CC0/OFL and other free licences (per the package copyright files).
- **Tested (7 Nov 2026):** supertux 0.6.3-1. Intro cutscene and menus rendered and responded to simulated keys; we navigated Start Game > Story Mode to the world map.
- **Catch:** the run command is `supertux2`, not `supertux`.
- **Version note:** 0.6.3 is also the current upstream release (per https://supertux.org/download.html, checked 7 Nov 2026).
- **Upstream:** https://supertux.org

![SuperTux start menu](screenshots/supertux-menu.png)

### Hedgewars

Turn-based artillery battles with hedgehogs: solo missions, local and online multiplayer.

```bash
sudo apt install hedgewars && hedgewars
```

- **Licence:** GPL-2 (code); documentation GFDL-1.3; data CC-BY-SA-3.0 and other free licences (per the package copyright files).
- **Tested (7 Nov 2026):** hedgewars 1.0.0-16build1. Rendered its first-run dialog offering training missions, over the main menu.
- **Version note:** 1.0.0 is the current upstream release (per https://www.hedgewars.org/download.html, checked 7 Nov 2026; the source tarball carries 1.0.3 build fixes that don't change gameplay).
- **Upstream:** https://www.hedgewars.org

![Hedgewars first-run prompt](screenshots/hedgewars-welcome.png)

### Teeworlds

Fast 2D arena shooting with a grappling hook. Multiplayer only - there is no single-player mode.

```bash
sudo apt install teeworlds && teeworlds
```

- **Licence:** Zlib (code); data Zlib/CC0/BSD (per the package copyright files).
- **Tested (7 Nov 2026):** teeworlds 0.7.5-1. First-run language and player-name prompts, then the main menu rendered (0.7.5 shown). Finding a match needs an internet server.
- **Version note:** 0.7.5 (April 2020) is the latest official release (per https://www.teeworlds.com, checked 7 Nov 2026). The community fork DDraceNetwork (DDNet, https://ddnet.org) describes itself as actively maintained and is where most ongoing development happens.
- **Upstream:** https://www.teeworlds.com

### Freedoom Phase 2 / Crispy Doom

A complete free-content campaign for Doom II, played through the Crispy Doom engine.

```bash
sudo apt install crispy-doom freedoom
crispy-doom -iwad /usr/share/games/doom/freedoom2.wad   # or the `freedoom2` launcher
```

- **Licence:** game data under the Freedoom licence (BSD-style terms, per the package copyright file); engine GPL-2.0+.
- **Tested (7 Nov 2026):** freedoom 0.12.1-2 with crispy-doom 5.11.1-1. Launched, the menu responded to simulated keys, and the engine loaded MAP15 and entered the first-person level view with HUD. Sound initialised (dummy driver).
- **Controls:** standard Doom layout (arrows to move, Ctrl to fire, Space to use, Shift to run), configurable with `crispy-setup`. From the engine's documentation; only menu keys were exercised in our run.
- **Upstream:** https://freedoom.github.io/ and https://github.com/fabiangreffrath/crispy-doom (both reachable at test time)

![Freedoom title screen](screenshots/freedoom-menu.png)
![Freedoom in-level view](screenshots/freedoom-level.png)


## Also tested

These 12 smaller or older games passed the same test rig on the same day. They're solid, just not the headline picks above. Same deal: command, what we verified, catches, proof.

### Nebulus - rotating-tower platform action

```bash
sudo apt install toppler && toppler
```

Reached live gameplay (attract demo).

### Nebulus (Toppler)

Climb a rotating tower against the clock; a remake of the classic Nebulus/Tower Toppler.

```bash
sudo apt install toppler && toppler
```

- **Licence:** GPL-2.0+ (package copyright).
- **Tested:** 1.3-1. Menu rendered; after input the game entered its attract/demo mode showing the engine playing the tower itself. Player controls not exercised.
- **Controls (packaged man page, not exercised in our run):** cursor keys move; Space or Return selects, jumps, or throws a snowball.
- **Upstream:** https://gitlab.com/roever/toppler/ (reachable at test time)

![Nebulus menu](screenshots/toppler-menu.png)
![Nebulus demo gameplay](screenshots/toppler-demo.png)

### LTris - polished Tetris-style blocks

```bash
sudo apt install ltris && ltris
```

Reached live gameplay (auto-played demo; the New Game screen defaults to the "Demo" game type).

### LTris - polished Tetris-style blocks

```bash
sudo apt install ltris && ltris
```

Reached live gameplay (auto-played demo; the New Game screen defaults to the "Demo" game type). [Details and screenshots](#ltris)

### MadBomber - catch falling bombs, Kaboom!-style

```bash
sudo apt install madbomber && madbomber
```

Reached the live game screen.

### MadBomber - catch falling bombs, Kaboom!-style

```bash
sudo apt install madbomber && madbomber
```

Reached the live game screen. [Details and screenshots](#madbomber)

### Vodovod - pipe puzzle against the clock

```bash
sudo apt install vodovod && vodovod
```

Reached the Level 1 board. Catch: the original site is gone; the game is maintained via Debian/Ubuntu.

### Vodovod - pipe puzzle against the clock

```bash
sudo apt install vodovod && vodovod
```

Reached the Level 1 board. Catch: the original site is gone; the game is maintained via Debian/Ubuntu. [Details and screenshots](#vodovod)

### BlockOut II - Tetris in true 3D

```bash
sudo apt install blockout2 && blockout2
```

Reached a running game (score progressing).

### BlockOut II - Tetris in true 3D

```bash
sudo apt install blockout2 && blockout2
```

Reached a running game (score progressing). [Details and screenshots](#blockout-ii)

### Alex the Allegator 4 - Game Boy-styled platformer

```bash
sudo apt install alex4 && alex4
```

Intro verified (story screens respond to keys); gameplay not reached in our automated run.

### Alex the Allegator 4 - Game Boy-styled platformer

```bash
sudo apt install alex4 && alex4
```

Intro verified (story screens respond to keys); gameplay not reached in our automated run. [Details and screenshots](#alex-the-allegator-4)

### Ceferino - fast single-screen arcade

```bash
sudo apt install ceferino && ceferino
```

Intro verified. Catch: upstream site unresponsive at test time; the Ubuntu package is the reliable source.

### Ceferino - fast single-screen arcade

```bash
sudo apt install ceferino && ceferino
```

Intro verified. Catch: upstream site unresponsive at test time; the Ubuntu package is the reliable source. [Details and screenshots](#ceferino)

### Powermanga - vertical shoot 'em up

```bash
sudo apt install powermanga && powermanga
```

Launch verified (menu rendered). Catch: a starfield intro runs for several seconds before the menu appears; it's not hung.

### Powermanga - vertical shoot 'em up

```bash
sudo apt install powermanga && powermanga
```

Launch verified (menu rendered). Catch: a starfield intro runs for several seconds before the menu appears; it's not hung. [Details and screenshots](#powermanga)

### Trackballs - marble-rolling 3D levels

```bash
sudo apt install trackballs && trackballs
```

Launch verified (menu over animated 3D backdrop).

### Trackballs - marble-rolling 3D levels

```bash
sudo apt install trackballs && trackballs
```

Launch verified (menu over animated 3D backdrop). [Details and screenshots](#trackballs)

### Fillets-NG - Sokoban-like fish logic puzzles

```bash
sudo apt install fillets-ng && fillets
```

Launch verified (world-map level select). Catch: the binary is called `fillets`.

### Fillets-NG - Sokoban-like fish logic puzzles

```bash
sudo apt install fillets-ng && fillets
```

Launch verified (world-map level select). Catch: the binary is called `fillets`. [Details and screenshots](#fillets-ng)

### Pingus - Lemmings-style penguin puzzles

```bash
sudo apt install pingus && pingus
```

Launch verified (main menu). Catch: this is the older 0.7.x stable branch, still shipped in Debian/Ubuntu. 

---

### Pingus - Lemmings-style penguin puzzles

```bash
sudo apt install pingus && pingus
```

Launch verified (main menu). Catch: this is the older 0.7.x stable branch, still shipped in Debian/Ubuntu. [Details and screenshots](#pingus)

---

## The games, with proof

## How we test

For each game:

1. We resolve the full dependency closure with apt's own resolver (`apt-get install --download-only --print-uris`), so the packages tested are exactly the ones `sudo apt install` would fetch, in the same versions.
2. We extract the packages and run the game against them in an isolated filesystem namespace (overlayfs over the stock system) on Ubuntu 22.04.5 LTS, with a virtual display (Xvfb, 1280x800x24) and no audio device. This is not a literal `sudo apt install` on a desktop machine; it is a runtime test of apt's exact package set.
3. We capture screenshots from the live run and record whether the process stayed up, whether the screen responded to simulated keyboard/mouse input (xdotool), and anything that broke.
4. We read the maintainer scripts (preinst/postinst/prerm/postrm) of the game packages. They do routine housekeeping: menu entries/icons, font conffile cleanup, soundfont and command aliases via `update-alternatives` (crispy-doom, and `wesnoth` -> `wesnoth-1.16`), and high-score storage setup - powermanga installs its binary setgid `root:games` (mode 2755) with score files under `/var/games/powermanga`, and toppler and ltris create `root:games` score directories/files. Our extraction test does not run these scripts, so setgid bits, command aliases and score-file setup are not reproduced, and installed high-score saving was not exercised.
5. Licence statements come from each package's own `/usr/share/doc/<package>/copyright` file (including the `-data` package where a game splits one), not from assumption.

Honest limits:

- No physical GPU and no sound card in the test environment. 3D games rendered in software (llvmpipe); audio was disabled. Performance on real hardware will be better than anything you see here, and slow first draws in our runs are the test rig, not the game.
- Input is simulated (xdotool), not a human player. "Demo/attract mode" entries prove the game engine renders and runs a level by itself; they do not prove player controls. Where a control scheme is listed from the game's packaged documentation, it says so, and it means we did not exercise it in the automated run.
- One game (0 A.D.) additionally needed a test-only tweak: it refuses to run as root and our namespace maps the tester to root, so we presented a non-root user id via `LD_PRELOAD`. Its entry is labelled as a modified-environment result.
- Version notes compare Ubuntu 22.04's package with upstream's latest release, checked on 7 November 2026 from the linked upstream pages. "Latest" means "latest on that date"; check the upstream link for today.
- Nothing here is a guarantee about other Ubuntu versions, Wayland sessions, or your hardware. It's a dated record of what ran, where, and how.

## Evidence levels

| Level | Meaning |
|---|---|
| **Gameplay screen reached** | Menus passed and an actual level/game screen rendered (start of play or attract/demo mode - the entry says which). |
| **Menu interaction verified** | Menu or intro screens visibly changed in response to simulated input. |
| **Launch verified** | Game launched, rendered its real menu/graphics, and stayed running. Input not exercised. |

## Notes

- Every screenshot in `screenshots/` was captured from our own test run on 7 November 2026; nothing is copied from upstream marketing material. Screenshots depict the games and remain subject to each game's own licence; they are included as test evidence.
- Every game also has an Ubuntu package page: `https://packages.ubuntu.com/jammy/<package-name>`.
- Text in this repository is MIT-licensed (see LICENSE).
- Planned next: more games, exercising real gameplay controls for every entry, testing on the current Ubuntu LTS, a Windows edition, and re-dating entries as new Ubuntu releases land.
