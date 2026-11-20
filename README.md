# Pirate Token Sim

A barebones Fortnite Treasure Hunters chest simulator built to show how bad the actual odds are for the Pirate Shop Access Token.

People think grinding 50k chests means they're "due" for a drop. That's not how independent probability works. I built this so you can watch thousands of rolls burn past in real time without wasting 400 hours of your life in-game.

## How it works

Everything lives in a single `index.html` file running Vue 3 via CDN and Tailwind. No build step, no `node_modules`, no bloat.

* **Exact drop math:** Uses the real 1 in 137,500 base drop rate (`~0.000727%`), plus toggles for the Saturday Treasure Hour multipliers (`1.5x` and `2x`). Every chest is an independent `Math.random()` roll—there is no pity system.
* **Frame-accurate auto-grind:** Uses a `requestAnimationFrame` delta-time accumulator loop instead of sloppy `setInterval` timers. You can crank it from `10/s` up to `2,500/s` without freezing the browser thread.
* **Live telemetry:** Tracks total chests opened, cumulative odds of having seen at least one token by now, estimated real-world hours wasted (assuming ~240 chests/hr on an optimal route), and a full breakdown of every loot tier.
* **Procedural audio:** All click, rarity, and token reveal fanfare sounds are synthesized on the fly with the Web Audio API. Zero external `.mp3` assets to load or break.

## Controls & Usage

1. **Open chests:** Click the chest on screen or hit `Spacebar` for single pulls. Use the `10x` and `100x` buttons if you want quick bursts.
2. **Switch odds:** Toggle between `1x` (Normal), `1.5x` (Afternoon Treasure Hour), and `2x` (Evening Treasure Hour) at the top of the HUD.
3. **Auto-Grind:** Pick a speed (`10/s`, `100/s`, `500/s`, or `2,500/s`) and let it run. It automatically pauses if you hit a Pirate Token so you don't roll right past it.
4. **Preview the drop:** If your luck is realistically awful and you just want to see the multi-stage token reveal animation and synth fanfare, hit the **Test Token Drop** button in the header.
5. **Math & Why tab:** Explains the binomial probability formula (`1 - (1 - p)^n`) behind the cumulative odds counter and why 95,308 chests only gets you to a coin flip.

## Running it locally

Since there's no bundler, you have two ways to run it:

**Option 1: Just open it**
Download `index.html` and double-click it. It runs straight in Chrome, Firefox, Edge, or Brave.

**Option 2: Local server**
If your browser blocks Web Audio autoplay on `file://` URLs, serve it locally with Python:

```bash
python -m http.server 8000
