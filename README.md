# STELLAR DANMAKU

**A love letter to Galaga and Touhou, crammed into a single HTML file.**

Stellar Danmaku is a browser-based bullet hell shooter that blends classic Galaga-style arcade combat with Touhou-inspired danmaku (bullet curtain) patterns. It runs entirely in the browser — no installs, no dependencies beyond Node for a simple static server — and plays on both desktop and mobile Safari.

---

## The Pitch

You pilot a lone fighter through waves of alien formations. Enemies don't just shoot at you — they paint the screen with spiraling, overlapping curtains of bullets that you have to weave through. It's part arcade shooter, part bullet ballet.

The game escalates in that classic Touhou way: early waves are manageable, almost meditative. Then a boss arrives and fills the screen with interlocking spiral patterns, and suddenly you're threading your ship through gaps that barely exist, grazing bullets for bonus points because the near-misses are half the fun.

---

## How It Plays

### The Basics

You move. You shoot (or on mobile, your ship auto-fires). Enemies fly in from the top in formations — diving swoops, slow heavy tanks, spinning bullet-sprayers, precise snipers. Kill them, dodge their bullets, collect the power-ups they drop.

Every 5th wave, a boss appears. Bosses have names (CRIMSON MOTH, VOID EMPRESS, STELLAR DRAGON), multi-phase attack patterns, and a health bar that stretches across the top of the screen. Their patterns shift as they take damage — what started as a manageable ring of bullets becomes a layered nightmare of spirals, fans, and aimed bursts.

### The Power System

You start weak — a single stream of shots. As you collect power items (red "P" drops from defeated enemies), your firepower grows through 4 levels:

1. **Single stream** — One laser, straight ahead
2. **Spread shot** — Side lasers fan out (or tighten up in focus mode)
3. **Wide barrage** — Five streams covering a wide arc
4. **Options** — Two floating gun pods orbit your ship and fire homing shots at the nearest enemy

Dying knocks you back a power level, which hurts. The tension between "stay safe at the bottom" and "push up to grab that power drop before it floats offscreen" is core to the moment-to-moment gameplay.

### Focus Mode

Hold SHIFT (or the FOCUS button on mobile) and your ship slows to a crawl — but your shot pattern tightens into a concentrated beam, your hitbox becomes visible (a tiny pink dot), and your item collection radius expands massively. Focus mode is how you survive dense bullet patterns: slow, deliberate micro-movements where you can see exactly what will and won't hit you.

This is directly inspired by Touhou's focus mechanic, and it's what elevates the game from "dodge stuff" to "dance through stuff."

### Grazing

Bullets that pass close to your hitbox without hitting it count as "grazes." Each graze adds to your score and your graze counter. This rewards aggressive, risky play — the best scores come from dancing on the edge of death, not hiding in corners.

### Bombs

You carry a limited supply of bombs (the green "B" drops). Using one clears all bullets on screen, damages all enemies, and gives you brief invincibility. Bombs are your panic button, but also a tactical tool — clearing a screen of bullets right before a boss phase transition, or using the invincibility frames to ram through an otherwise impossible pattern.

---

## The Enemies

### Regular Enemies (Waves 1-4, 6-9, etc.)

| Type | Behavior | Bullet Pattern |
|------|----------|----------------|
| **Grunt** | Flies straight down in formation | Single aimed shot at the player |
| **Swooper** | Sweeps in from the side in a sine wave | Ring of 8 bullets on a timer |
| **Spinner** | Drifts down while rotating | Constant stream of 3-bullet clusters, spinning |
| **Tank** | Slow, heavy, takes a beating | Fan of 5 aimed yellow bullets |
| **Sniper** | Parks mid-screen, barely moves | Fast double-shot, precisely aimed |

Waves combine these in formations — a tank escorted by grunts, a screen full of swooping enemies from both sides, a circle of grunts spiraling inward.

### Bosses (Every 5th Wave)

**CRIMSON MOTH** (Wave 5) — The introductory boss. Fires expanding rings of pink bullets and aimed cyan shots. In later phases, adds spiral patterns. Teaches you that bosses aren't just bullet sponges — their patterns change.

**VOID EMPRESS** (Wave 10) — Steps up the pressure with continuous rotating bullet arms (5-9 arms depending on phase), aimed fan bursts in rapid succession, and in her final phase, a massive alternating-color ring burst. She moves more aggressively and her patterns overlap in ways that demand focus mode.

**STELLAR DRAGON** (Wave 15) — The current endgame boss. Triple-layer rotating spirals (clockwise and counter-clockwise simultaneously), bullet rain from the top of the screen, and dense aimed laser bursts. The bullet count gets genuinely overwhelming. This is where bombs stop being optional.

Bosses scale with wave number — if you loop past wave 15, the bosses repeat but with more HP and denser patterns.

### Minibosses

Minibosses appear throughout campaign levels and Boss Fight mode. Each has a **signature mechanic** that demands a different player skill — not just different bullet patterns, but fundamentally different ways of fighting.

**DRIFT JELLYFISH** — *The Phase Shifter.* Drifts across the entire arena in graceful lissajous curves, trailing slow-falling bullet rain behind its path. Periodically phases out — becoming translucent and invulnerable — then reappears elsewhere with a burst of bullets. You need spatial awareness: track where it's been (the trail is dangerous), predict where it'll reappear, and pour damage during its solid windows. *(Tests: spatial awareness, pathfinding)*

**IRON SCARAB** — *The Berserker.* Telegraphs a charge aimed at the player, then launches in any direction — bouncing off walls like a billiard ball up to 3 times. Each impact slam creates a persistent crater that pulses bullet rings every 1.5 seconds. Wings fold during charges (smaller hitbox, 50% armor) and spread during hover (vulnerable, wider target). Multiple charges mean multiple craters — the arena gets progressively more dangerous. *(Tests: positioning, pressure management)*

**NEBULA SERPENT** — *The Moldorm.* A segmented snake boss with a trailing body that follows its head through a ring buffer of position history. Charges, rotates, and wall-bounces with an AI state machine. Every body segment is independently hittable along the entire undulating chain. The head leads while 7 body segments slither behind with tapered radii and connected tissue. *(Tests: tracking, spatial reading)*

**PLASMA SENTINEL** — *The Fortress.* Four orbiting shield orbs physically block your bullets — they absorb hits and must be destroyed or shot around. Each shield covers a 45° arc, and the rotation speed increases as shields are destroyed. Periodically opens a vulnerability window where shields stop rotating and the core glows bright — burst DPS during these windows is rewarded with extended openings. Destroying all shields triggers an exposed fury mode. *(Tests: timing, precision)*

**VOID HYDRA** — *The Regenerator.* Three independently-targetable heads, each with its own HP pool. Sever a head and the remaining heads enrage — firing faster with wider sweeps. But severed heads regenerate after 8 seconds, coming back 25% stronger each time. The intended strategy: damage all 3 heads evenly, then burst them down within a 5-second window to trigger the exposed state (3x damage to the body, bullet clear reward). *(Tests: target prioritization, burst timing)*

---

## The Visuals

The game uses a mix of hand-crafted sprite art and canvas-rendered effects:

- **Player ship** — Foozle Void Main Ship pixel art with animated engine exhaust and 4 damage states that visually degrade as you lose HP
- **Enemies** — Kenney Space Shooter Redux sprites, each enemy type mapped to a distinct silhouette so you can read the battlefield at a glance
- **Bullets** — Programmatic glowing circles and rice-grain shapes with per-bullet color coding (pink = grunt, cyan = spinner, yellow = tank, purple = sniper, orange = swooper). The glow is important — it makes bullet patterns readable even when dense
- **Background** — Tiled scrolling space texture with 3-layer parallax starfield and drifting meteors
- **Explosions** — Kenney fire sprites with additive blending, layered with particle bursts
- **Post-processing** — Full-screen bloom pass (blurred + brightened overlay with additive compositing) gives everything a soft neon glow

All assets are CC0 licensed (Kenney Space Shooter Redux, Foozle Void Collection).

---

## Mobile

The game was designed mobile-first for iPhone Safari. Touch controls use a **relative offset drag** system — touch anywhere on screen, then drag. Your ship moves 1:1 with your finger movement, no matter where you touched. This means your finger never has to be on top of your ship, so you can always see what you're dodging.

Auto-fire is always on. FOCUS and BOMB are dedicated buttons in the bottom-right corner.

---

## Technical Details

- **Single HTML file** — All game code lives in `index.html` (~5700 lines of JS)
- **Node server** — `server.js` is a minimal static file server (serves assets from `/assets/`)
- **Canvas** — 480x720 internal resolution, scaled to fit any screen
- **No frameworks** — Vanilla JS, requestAnimationFrame game loop
- **Asset loading** — Progress bar on startup, graceful fallback to programmatic rendering if sprites fail to load

### Running It

```
node server.js
# Open http://localhost:3003
```

---

## Where It Could Go

This is a working foundation. Here are some directions worth exploring:

**Recently Added**
- 3 selectable ships with different shot types and speeds
- Campaign mode with structured levels and star ratings
- Roguelike powerup system (20 powerups across 4 rarity tiers, offered between waves)
- 5 unique minibosses with signature mechanics (phase-shifting, wall-bouncing charges, shield blocking, multi-part HP, segmented body)
- AI-generated boss sprites with luminance keying for transparent backgrounds

**Gameplay — Next**
- Spell card system (named, scripted boss attacks with bonus rewards for no-hit clears)
- Difficulty selection that changes bullet density and speed
- Score multiplier that builds with continuous grazing
- More enemy types (shielded enemies, teleporters, enemies that split on death)

**Polish**
- Sound effects and music (the Kenney pack includes SFX files)
- Boss intro sequences (warning text, dramatic pause)
- Bullet canceling on enemy death (turning bullets into score items, like Touhou)
- Replay system / high score table

**Infrastructure**
- Online leaderboard
- Replay sharing
- Level editor for custom wave patterns

---

*All game art is CC0 licensed. Kenney Space Shooter Redux by kenney.nl. Foozle Void Main Ship by Foozle (foozlecc.itch.io).*
