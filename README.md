# 128bitcalculator — Math, but chunkier.

The 128bit family's pixel calculator app. Landing page + working mock live at https://hootywhooo86.github.io/128bitcalculator/

## What it is

A chunky, satisfying calculator for the 128bit family: big pixel buttons, a history tape that remembers every calculation, daily math quests that feed XP into 128bitlife, and a live widget for the bitlauncher home screen.

The mock on the landing page is a real working calculator: basic arithmetic, ±, %, a history tape, and a "Five a Day" quest bar (+25 XP at 5 solved calculations).

## Architecture

- One 128bit account + the shared family event feed (`supabase/family-feed.sql` — same `family_events` schema as the rest of the family). Calculator emits `calculation.solved` events so history syncs and quests can subscribe.
- Landing page is a static mock only; the real app build is Carlos's lane (see below).

## Open product questions (Daniel's call)

- **Modes:** standard only, or scientific (√, x², sin/cos, logs) and programmer (hex/binary) modes too? The mock is standard-only for now.
- **Conversions:** unit conversion (length, weight, temperature) and currency conversion in v1, or later?
- **History depth:** local-only tape, or cloud-synced across devices via the family feed?
- **Widget:** is the bitlauncher calculator widget a v1 must-have?
- **Quests:** how deep does the gamification go — daily streaks, difficulty tiers, kid mode for the family?
- **Platform:** iOS/Android/both, and is this a native build or a web app wrapped for stores?

## The app (`app/`)

A TI-83-style calculator that runs in any browser and installs to the home screen (PWA, works offline). Live at https://hootywhooo86.github.io/128bitcalculator/app/

- **CALC**: expression entry on a green LCD with a scrolling history (tap an answer to reuse it), `Ans`, 2ND functions (inverse trig, eˣ, 10ˣ, ³√, ⁿ√, nCr, nPr, abs, rand), x², ^, √, !, %, EE, DEG/RAD, implicit multiplication (`2π`, `3(4+1)`). Keyboard works too. Uses its own parser (no `eval`).
- **GRAPH**: Y1–Y4, pixel plotting, drag to TRACE, window settings, ZStandard/ZTrig/zoom, and a TABLE view.
- **CONVERT**: cooking volumes (US/metric/UK cups, tbsp, tsp, fl oz, pinch…), baking by weight (cups of flour/sugar/butter… ↔ grams, per-ingredient densities), distance, weight, temperature (incl. gas mark), speed & running pace, area, volume, time, fuel economy, data, energy, pressure, angle. Plus a **recipe scaler** that rescales a whole ingredient list and rounds to kitchen fractions (¼, ⅓, ½…).
- **STAT**: 1-Var Stats (mean, sum, n, median, Sx, σx, min/max, Q1/Q3, Σx², mode) and quick tip / split / percent-off math.
- Five a Day quest: +25 XP after 5 solved calculations a day.

Everything is saved on the device (localStorage).

## Android app

`android/` wraps the same web app with [Capacitor](https://capacitorjs.com) as an offline Android app (everything bundled, no internet needed). GitHub Actions builds the APK on every push (`.github/workflows/android.yml`); pushes to `main` publish it at https://github.com/Hootywhooo86/128bitcalculator/releases/tag/android-latest. Open that page on your phone, download `128bitcalculator.apk`, and allow installs from your browser. Later builds install over the old one and keep your data.

- Build it yourself: `npm ci && npx cap sync android && cd android && ./gradlew assembleDebug` (JDK 21 + Android SDK). `tools/make_icons.py` regenerates the pixel icons.
- The app keeps its own saved data, separate from the browser version, and the "use on every 128bit app" colour switch can't reach across separate Android apps.
- Signed with `android/app/sideload.keystore`, a key committed to the repo for sideloading. A Play Store release needs a private key kept out of the repo.

## Status

- Landing page: live, links to the app.
- App: v1 working (`app/index.html`). Formspree ID still needed in the landing waitlist form (`YOUR_FORM_ID`).
