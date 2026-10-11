# TACHYON — House Cup Ranking Explanation

## 1. Overview

TACHYON is an interactive 3D House Cup leaderboard that tracks points earned by four houses:

- **ALPHA**
- **INFERNO**
- **MATRIX**
- **LAYER**

The ranking system determines each house's position based on its accumulated points.

## 2. How the Ranking Is Calculated

The ranking calculation follows these steps:

1. Initialize every house with **0 points**.
2. Select a house and enter the points it has earned.
3. Validate the input: it must be a positive whole number, with a maximum of 100,000 points per award.
4. Add the awarded points to the selected house's existing total.
5. Sort all houses from the highest total score to the lowest.
6. Assign ranks according to sorted positions, giving equal scores the same rank.

## 3. Sample Ranking Table

The following table demonstrates an example of the ranking system using sample scores.

| Rank | House | Total Points |
|---:|---|---:|
| 1 | ALPHA | 100 |
| 1 | MATRIX | 100 |
| 3 | INFERNO | 75 |
| 4 | LAYER | 25 |

*Note: These are illustrative scores, not actual project data.*

## 4. Tie-Handling Logic

When two or more houses have equal scores, they receive the same rank.

For example, ALPHA and MATRIX both have 100 points, so they share **Rank 1**. INFERNO has 75 points and receives **Rank 3**, because two houses occupy the first position.

This is known as competition ranking: **1, 1, 3, 4**.

## 5. Ranking Algorithm

The following simplified JavaScript illustrates the ranking logic used by TACHYON:

```javascript
function rank() {
  const arr = HOUSES
    .map(h => ({ ...h, p: state.pts[h.n] }))
    .sort((a, b) => b.p - a.p);

  let r = 0;

  arr.forEach((h, i) => {
    if (i === 0 || h.p !== arr[i - 1].p) {
      r = i + 1;
    }
    h.r = r;
  });

  return arr;
}
```

### Algorithm explanation

- `map()` collects each house and its current points.
- `sort()` orders the houses by descending score.
- The loop compares each score with the previous score.
- If the score differs, the rank becomes the current position plus one.
- If the score is equal, the previous rank is retained.
- The sorted list is returned for displaying the leaderboard.

## 6. Additional Features

- **Live leaderboard:** Updates house rankings when points are awarded.
- **Cup leader:** Displays the leading house or a tie between leaders.
- **Undo:** Reverses the most recent award.
- **Reset:** Clears scores and the award history after confirmation.
- **Score timeline:** Visualizes how house scores change over time.
- **Browser storage:** Saves scores and award history using `localStorage`.

## 7. Technology Stack

- HTML5
- CSS3
- JavaScript
- Three.js for 3D graphics
- HTML Canvas for the score timeline
- Browser `localStorage` for persistence

## 8. Important Limitation

Scores are stored in the current browser's local storage. There is no shared backend database, so scores are not automatically synchronized across different users or devices.

---

**Project:** TACHYON — House Cup  
**Purpose:** Interactive house-point tracking, ranking, and visualization.
