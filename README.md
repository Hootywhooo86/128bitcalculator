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

## Status

- Landing page + mock: live (coming-soon).
- Real app build: not started. Formspree ID still needed in the waitlist form (`YOUR_FORM_ID` placeholder with a local-confirm fallback).
