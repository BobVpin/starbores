# Star Warts: A New Hand

A parody space-opera trading card game for the browser. Collect cards, build a 20-card deck, and fight 1v1 duels to earn credz you can spend on stronger cards.

## What's in it

- **Matches:** heroes start on 25 health and gain one energy crystal per turn, up to 10. Units have Guard, Shield, Rush or Miss keywords, and many have battlecry effects.
- **31 cards** across four rarities, from Moisture Farmer to Darth Wader.
- **Credz economy:** everyone starts with 200 credz and a starter deck.
  - Duel rewards: 60 for a win, 15 for a loss.
  - Training droid rewards: 20 for a win, 5 for a loss.
  - Daily bonus: 50.
  - 12 achievements that each pay out once.
- **Shop:** buy single cards by rarity (40 / 120 / 300 / 800), or Bantha Booster and Kyber Crate packs with guaranteed Rare or Epic cards.
- **Deck builder:** up to 2 copies of a card and 1 of each Legendary, with an auto-build button.
- **Multiplayer:** open a duel, anyone in the lobby can accept, and moves sync live. There's also a rankings table by duel wins.

## Running it

It's one self-contained file: `index.html`.

- **Hosted as a Claude artifact:** the page uses the artifact runtime (`window.claude.use("db" | "room" | "user")`) for saved profiles, the duel lobby, live match state and rankings.
- **Opened anywhere else** (a local file or any static host): it falls back to offline mode. Progress saves to `localStorage` and the Training Droid is playable. Online duels need a backend.

## Taking it further

Right now each player's client keeps their own credz and runs the rules, which is fine among friends but not cheat-proof. For a public release, move the rules engine (`act()`, `newGame()`) and the currency onto a server. That means:

- a small Node service with WebSockets for matches
- a database for accounts, collections and credz
- the server as the only thing allowed to award credz or open packs

The engine is already a pure function that takes a state and an action, so it can run unchanged on the server.
