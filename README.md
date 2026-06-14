# ⏱️ Stopwatch with Lap Tracker

A clean, fully functional stopwatch web application built with plain **HTML**, **CSS**, and **JavaScript** — no libraries, no frameworks, no setup needed.

---

## 📋 Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Code Breakdown](#code-breakdown)
- [How to Run](#how-to-run)
- [How to Use](#how-to-use)
- [Technologies Used](#technologies-used)

---

## ✨ Features

- ▶️ **Start / Pause / Resume** the stopwatch with one button
- ⚑ **Record lap times** while the timer is running
- ↺ **Reset** the timer and clear all laps
- 📊 **Live stats** — total laps, fastest lap, and average lap time
- 🟢 **Fastest lap** highlighted in green
- 🔴 **Slowest lap** highlighted in red
- ⏱️ **Centisecond precision** — MM:SS.cs display
- 📱 Works in any modern browser, no installation required

---

## 📁 Project Structure

```
stopwatch/
└── index.html      ← entire app in one file (HTML + CSS + JavaScript)
```

Everything lives in a single `index.html` file:

| Layer | Location |
|-------|----------|
| **Structure** | `<body>` — HTML elements and layout |
| **Styling** | `<style>` block inside `<head>` |
| **Logic** | `<script>` block before `</body>` |

---

## 🔍 Code Breakdown

### HTML Structure

```
.container
├── .main-title              ← "STOPWATCH" heading
└── .sw-wrap                 ← white card
    ├── .sw-display          ← timer area
    │   ├── #display         ← MM:SS digits
    │   ├── #msDisplay       ← .cs centiseconds
    │   └── #statusLabel     ← Ready / Running / Paused
    │
    ├── .sw-controls         ← action buttons
    │   ├── #startBtn        ← Start / Pause / Resume
    │   ├── #lapBtn          ← Record a lap
    │   └── #resetBtn        ← Reset everything
    │
    ├── .sw-stats            ← three summary cards
    │   ├── #lapCount        ← total laps
    │   ├── #fastLap         ← fastest lap time
    │   └── #avgLap          ← average lap time
    │
    └── .sw-laps             ← lap table
        ├── .sw-laps-header  ← column labels (Lap / Split / Time)
        └── #lapList         ← dynamically rendered lap rows
```

---

### CSS Highlights

| Class | What it styles |
|-------|---------------|
| `.main-title` | Large blue "STOPWATCH" heading at the top |
| `.sw-wrap` | White rounded card with drop shadow |
| `.sw-time` | 70px bold timer digits |
| `.sw-ms` | 35px centisecond decimal |
| `.sw-controls` | Flexbox row for the three buttons |
| `.primary` | Blue background for Start/Resume button |
| `.danger` | Red background for Reset button |
| `.sw-stats` | 3-column CSS Grid for the stat cards |
| `.sw-laps-header` | Blue table header row |
| `.fastest` | Green highlight for the best lap row |
| `.slowest` | Red highlight for the worst lap row |

---

### JavaScript Functions

#### State Variables

| Variable | Purpose |
|----------|---------|
| `running` | Whether the timer is currently ticking |
| `startTime` | Timestamp when the timer last started (`Date.now()`) |
| `elapsed` | Total elapsed time in milliseconds |
| `rafId` | `requestAnimationFrame` handle used to cancel the loop |
| `laps` | Array of recorded lap objects `{ num, total, split }` |
| `lapStart` | Timestamp when the current lap started |

---

#### `fmt(ms)` — Format main display
Converts milliseconds to `MM:SS` string.
```js
fmt(75000)  →  "01:15"
```

#### `fmtMs(ms)` — Format centiseconds
Returns the `.cs` decimal part.
```js
fmtMs(1340)  →  ".34"
```

#### `fmtLap(ms)` — Format lap time
Full lap format: `MM:SS.cs`
```js
fmtLap(75340)  →  "01:15.34"
```

#### `tick()` — Animation loop
Called every animation frame via `requestAnimationFrame`. Calculates elapsed time from `Date.now() - startTime` and updates the live display.

#### `toggleStart()` — Start / Pause / Resume
Handles all three states in one function:
- **Start** → begins timer, enables Lap and Reset buttons
- **Pause** → cancels the animation frame, freezes display
- **Resume** → restarts from the paused position

#### `recordLap()` — Record a lap
Captures the split time (time since the last lap) and total elapsed time, adds a new entry to the `laps` array, then calls `renderLaps()`.

#### `resetTimer()` — Reset everything
Stops the timer, clears all state variables and the DOM — restoring the app to its initial "Ready" state.

#### `renderLaps()` — Render the lap table
Sorts laps by split time to find fastest and slowest, calculates the average, updates the stat cards, and rebuilds the lap table HTML with `.fastest` / `.slowest` CSS classes applied where appropriate.

---

## 🚀 How to Run

No server or install needed. It's a single HTML file.

1. Save the code as `index.html`
2. Open it in your browser:
   - **Double-click** the file, or
   - Drag it into a browser window, or
   - Right-click → *Open with* → your browser

> ✅ Works in Chrome, Firefox, Edge, and Safari.

---

## 🎮 How to Use

| Button | Action |
|--------|--------|
| **Start** | Starts the stopwatch |
| **Pause** | Freezes the timer (shown while running) |
| **Resume** | Continues from where it paused |
| **Lap** | Records a lap (only active while running) |
| **Reset** | Clears the timer and all recorded laps |

**Reading the lap table:**

| Column | Meaning |
|--------|---------|
| **Lap** | Lap number in the order it was recorded |
| **Split** | Time taken for that individual lap |
| **Time** | Total elapsed time when the lap was recorded |

> 🟢 **Green row** = fastest lap  
> 🔴 **Red row** = slowest lap  
> *(Highlights appear only when 2 or more laps are recorded)*

---

## 🛠️ Technologies Used

| Technology | Usage |
|------------|-------|
| **HTML5** | Page structure and UI elements |
| **CSS3** | Styling, Flexbox, Grid, transitions |
| **JavaScript ES6+** | Timer logic, DOM manipulation, event handling |
| `requestAnimationFrame` | Smooth high-performance timer rendering |
| `Date.now()` | Accurate millisecond timestamps |

---

## 👨‍💻 Author

Built as an internship project demonstrating core front-end web development skills.

---

## 📃 License

Open source — free to use for learning and educational purposes.
