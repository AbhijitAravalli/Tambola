# Tambola Caller · Housie

A single-file, zero-dependency **Tambola / Housie** game and number caller that runs entirely in your browser. Generate valid 3×9 tickets, call numbers 1–90, and watch claims light up and get awarded automatically.

## Play it

No install, no build, no server. Just open the file:

1. Download or clone this repo.
2. Double-click **`tambola-housie.html`** (or open it in any modern browser).

Everything — ticket generation, the caller, claim detection — runs offline in the page. Nice fonts load from Google Fonts when online, with system-font fallbacks otherwise.

## How to use

### 1. Set up a game
- **Tickets** — how many tickets to generate (1–100).
- **Player names** — optional, one name per line. Unnamed tickets become "Player 1", "Player 2", …
- Click **Generate tickets & start**.

Every ticket is a valid housie ticket: 3 rows × 9 columns, 15 numbers total (5 per row), each column holding 1–3 numbers within its fixed range, sorted top-to-bottom. Tickets are guaranteed unique within a game.

### 2. Call numbers
- **Draw number** — draws the next random number (1–90). You can also press **Spacebar**.
- The current ball animates in; the **board** glows gold for called numbers and rings the latest one.
- **Recent calls** shows the last 12 numbers.
- **Undo last** — takes back the most recent draw (claims recompute correctly).

### 3. Options
- **Call numbers aloud** — speaks each number using the browser's speech synthesis.
- **Auto-draw every N s** — automatically draws on a timer (2–30 seconds).

### 4. Claims (auto-awarded)
The first ticket to complete each pattern wins it automatically:

| Claim | Condition |
|-------|-----------|
| **Early Five** | First 5 numbers marked on a ticket |
| **Top Line** | All numbers in row 1 |
| **Middle Line** | All numbers in row 2 |
| **Bottom Line** | All numbers in row 3 |
| **Four Corners** | First & last number of the top and bottom rows |
| **Full House** | All 15 numbers |

A banner announces each win, and the winning ticket shows a badge.

### 5. Other controls
- **New game · keep tickets** — clears called numbers/claims, keeps the same tickets.
- **New tickets** — discards everything and returns to setup.
- **Print tickets** — opens a clean, printer-friendly sheet of all tickets (2 per row).

## Persistence

Your current game (tickets + called numbers) is saved to the browser's `localStorage` and automatically resumes when you reopen the file. Saving is skipped silently if storage is unavailable (e.g. a sandboxed preview frame).

## Customizing claims

Claim patterns live in the `CLAIMS` array in the script. Add your own — for example an "Early Seven" or "Pyramid" — by adding an entry with an `id`, `name`, and a `test(grid, drawnSet)` function.

## Built-in self-test

On load, the game validates **1,000 generated tickets** and logs the result to the browser console — open DevTools to see:

```
✅ Tambola self-test passed — 1000/1000 valid tickets
```

## Tech

- Pure HTML + CSS + vanilla JavaScript, in one file.
- No frameworks, no dependencies, no network required to play.
- Works on desktop and mobile browsers.
