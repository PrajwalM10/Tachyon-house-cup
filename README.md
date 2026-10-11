# TACHYON — House Cup

An interactive, cinematic 3D leaderboard for tracking points across four houses: **ALPHA**, **INFERNO**, **MATRIX**, and **LAYER**. The interface combines a Three.js arena with live standings, score history, sound effects, and animated visualisation modes.

## Features

- Interactive 3D arena powered by Three.js
- Four houses with distinct colours
- Add points using a custom amount or quick-add buttons (+10, +25, +50, +100)
- Live rankings and cup-leader display
- Score timeline and recent-award log
- Undo the most recent award, replay the score history, or reset the cup
- Four visualisation modes: Orbit, Pillars, Helix, and Crown
- Optional auto-morph, cinematic framing, sound effects, and free-orbit camera
- Saves scores and award history in the browser's local storage
- Responsive layout for desktop and mobile screens

## How to run

1. Download or clone this repository.
2. Open `index.html` in a modern browser such as Google Chrome or Microsoft Edge.
3. Select a house, enter a positive whole-number score, and click **ADD POINTS**.
4. Explore the visualisation modes and ranking panels.

The page loads Three.js and Google Fonts from external CDNs, so an internet connection is needed for those external assets. No package installation or backend server is required for normal use.

## How ranking is calculated

Each house has a total score, initially `0`. When points are awarded, the amount is added to that house's total. The ranking function sorts all houses by total score in descending order:

1. The house with the highest total receives rank **#1**.
2. Houses with equal totals share the same rank.
3. Ranking uses competition-style positions: if two houses tie at #1, the next house is ranked #3.
4. A champion is displayed only when the highest score is greater than zero. If multiple houses share the highest positive score, the app displays a tie.

**Example:** ALPHA = 100, MATRIX = 100, INFERNO = 75, LAYER = 20 results in ALPHA #1, MATRIX #1, INFERNO #3, and LAYER #4.

The score is the sum of all valid awards for each house. The app accepts whole numbers greater than 0 and limits a single award to 100,000 points. Undo removes the most recent award from both the log and the corresponding total.

## Data storage

The app stores its current points and award log in the browser's `localStorage` under the key `tachyon-orbit-v2`. Data stays in that browser on that device; it is **not** synchronised between users or devices, and clearing browser storage can remove it.

## Technologies used

- HTML5
- CSS3 (responsive layout, animations, visual effects)
- JavaScript
- [Three.js](https://threejs.org/) for the 3D scene
- Canvas 2D API for the score timeline
- Browser Web Audio API and Speech Synthesis API for optional sound and voice
- Browser `localStorage` for persistence

## Sample output / screenshots

Add screenshots of the running app to the `screenshots/` folder, then embed them here. Suggested screenshots:

- `screenshots/arena.png` — the 3D arena and its four house orbs
- `screenshots/leaderboard.png` — rankings, cup leader, and score timeline after awarding points

Once those images exist, you can display them in this README with:

```md
![TACHYON 3D arena](screenshots/arena.png)
![TACHYON leaderboard and timeline](screenshots/leaderboard.png)
```

## Notes

- This is a frontend-only demo; there is no shared database, authentication, or server-side score validation.
- Scores are stored locally in the browser, so different visitors will have separate scoreboards.
- Three.js and Google Fonts are loaded from third-party CDNs.

## License

No license has been specified yet. Add a license file if you want to define how others may reuse the code.
