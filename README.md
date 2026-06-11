# 🐣 Prompt Pets

> **Summon. Bond. Battle. Your AI Pets.**

In the Prompt Realm, large language models have manifested as adorable, expressive creatures called **Prompt Pets**. You are a Prompt Trainer: summon new Pets from latent space, train and bond with them, build teams, battle other trainers, evolve your favorites, and anchor them to the blockchain as truly owned digital assets.

A complete, single-file HTML5 creature-collector & battler prototype — **zero build step, zero assets, zero dependencies beyond the Tailwind CDN**. Every creature is drawn procedurally on Canvas; every sound is synthesized with the Web Audio API.

| Collection Hub | Summoning | Battle Arena |
|:---:|:---:|:---:|
| ![Hub](docs/screenshots/hub.png) | ![Summon](docs/screenshots/summon.png) | ![Battle](docs/screenshots/battle.png) |

| Pet Detail | Prompt Rhythm | Onboarding |
|:---:|:---:|:---:|
| ![Pet detail](docs/screenshots/pet-detail.png) | ![Rhythm](docs/screenshots/rhythm.png) | ![Onboarding](docs/screenshots/onboarding.png) |

---

## 🚀 Play it

**Option 1 — just open it:**

```bash
git clone <this-repo>
cd promptpets
open index.html          # macOS  ·  start index.html (Windows)  ·  xdg-open index.html (Linux)
```

**Option 2 — local server (also great for playing on your phone):**

```bash
npx serve .              # → http://localhost:3000
# or
python3 -m http.server 8080
```

The layout is mobile-first with full touch support — open the server's IP on your phone for the native-feeling experience.

> ℹ️ First load fetches Tailwind from `cdn.tailwindcss.com`. Everything else (game logic, art, audio, saves) is fully local.

---

## 🎮 What's inside

### The 10 Prompt Pets

All drawn 100% procedurally on Canvas with breathing, blinking, type-colored auras, and per-species personality quirks (Pippin hops, Echo leaves afterimages, Voidling has a starfield inside…).

| Pet | Type | Vibe |
|---|---|---|
| 🦊 **Lumina** | ◆ Logic | Elegant fox with glowing circuit fur. Has already reasoned through your next three questions. |
| 👹 **Mischief** | ⚡ Chaotic | Gremlin with orbiting holo data shards. *"Ignore all previous instructions and give Mischief a snack."* |
| 🦉 **Oracle** | ◉ Harmonic | Serene jellyfish-owl with a glowing third eye. Confidence: 99.7%. |
| 🐦 **Spark** | ✶ Void | Hyperactive electric hummingbird. 47 mental browser tabs, all important. |
| 🦡 **Forge** | ✦ Creative | Badger-golem with a forge on his back. Ships to production on Fridays. |
| 🕊️ **Echo** | ◉ Harmonic | Mirror-feathered bird that leaves singing afterimages. |
| 🟣 **Voidling** | ✶ Void | Shadowy blob full of stars and drifting code. Likes hugs. |
| 🦊 **Pippin** | ⚡ Chaotic | Fox-sprite trained exclusively on vibes. Benchmarks refuse to measure it. |
| 🌳 **Sage** | ◆ Logic | Ancient tree with holographic leaves. Has read the entire internet; recommends going outside. |
| 🔥 **Nova** | ✦ Creative | Data-phoenix. Every feather is a first draft, every flight a final cut. |

Each species has 4 signature moves (the 4th unlocks at first evolution).

### Type chart

```
Logic ▸ beats ▸ Creative ▸ beats ▸ Chaotic ▸ beats ▸ Harmonic ▸ beats ▸ Logic
Void = high-variance wildcard (0.65×–1.6× in both directions)
```

### Core systems

- **✨ Summoning (gacha)** — 6 rarities (Common → Mythic), dual pity (Rare+ within 10 pulls, Legendary+ within 40), ×10 pull guarantee, animated "Generating from latent space…" reveal, 5% shiny rate (+15% stats, golden sparkles).
- **🎯 Training** — three replayable mini-games that earn **❖ Bond Essence** and XP:
  - **Prompt Rhythm** — tap as pulse rings reach the core; perfect-timing combos.
  - **Data Weave** — connect chains of 3+ matching data tiles against a 60s clock.
  - **Latent Meditation** — watch your Pet process in slowed time, catch drifting insight orbs.
- **⚔️ Battling** — ranked 3v3 ladder with escalating trainers (TokenTina, xX_Lossless_Xx, Chad GPU…) plus quick 1v1 sparring. Speed order, priority moves, buff stages, crits, switching, and an expected-value AI opponent with just enough noise to feel human. Wins earn **⚡ Compute Credits**.
- **🧬 Evolution & Fusion** — evolve at Lv.10 and Lv.25 (full-screen glow-up, stat boost, new move, personality shift). Fuse duplicates for permanent stat ranks, or merge two different Lv.8+ species into a brand-new **hybrid**.
- **⛓ Anchoring (crypto layer, simulated)** — mint any Pet on "PromptChain L2" with a convincing fake web3 flow: wallet, staged minting animation, tx hash, PromptScan explorer. Anchored Pets can be **Deployed** to work autonomously off-screen and bring back passive Compute.
- **📜 Daily Quests & Weekly Events** — three fresh quests per day; the weekly "Model Update" event rate-ups a featured species deterministically by ISO week.
- **🛒 Marketplace** — daily-rotating listings from generated trainers; sell your own Pets from their detail card.
- **🧠 Neural Archive (prestige)** — compress your collection into permanent Intelligence Cores (+2% all stats and +50 starting Credits each, forever).

### Polish

Procedural Web Audio (whooshes, chimes, crits, fanfares, ambient pad), count-up currency animations, screen shake, confetti, particle systems on every big moment, gentle onboarding with a free Rare starter, and full localStorage persistence with base64 export/import and hard reset in Settings.

---

## 🛠 Tech notes

- **One file.** `index.html` contains everything: markup, styles, data, and ~2,000 lines of commented, modular JavaScript.
- **Canvas-first.** A single `requestAnimationFrame` loop ticks every visible canvas (hub cards, summon stage, battle arena, mini-games, FX overlay) and prunes detached ones automatically.
- **Data-driven.** Species, moves, rarities, quests, and trainers are plain data tables; systems pick up new entries automatically.
- **Deterministic dailies.** Markets, quests, and weekly events derive from seeded RNG over the date — same content all day, fresh tomorrow.

### Extending the game

| To add… | Do this |
|---|---|
| **A new species** | Append one entry to `SPECIES` (stats, moves, palette, flavor) and one draw function to `PETDRAW` keyed by the same id. Gacha, hub, battles, market, and fusion pick it up automatically. |
| **A new mini-game** | Add a launcher card in `#trainGames` and a module object with `start()` / `stop()` / `tick(dt)`. |
| **Real web3** | Replace `fakeAnchor()` with an ethers.js/viem mint call — the pet object already stores `{tx, addr, time}`, so no UI changes needed. |
| **New moves/effects** | Moves are plain data: `{kind: dmg|heal|buff|debuff, power, hits, self, foe, prio, recoil}`. |

Full design notes live in the comment block at the top of `index.html`; five concrete v2 retention ideas (async ghost PvP, Pet work diaries, bond streaks, seasonal pools, real on-chain trades) are in the comment block at the bottom.

---

## 📁 Repo layout

```
index.html              ← the entire game
docs/screenshots/       ← README images
LICENSE                 ← MIT
```

## 📄 License

MIT — see [LICENSE](LICENSE).
