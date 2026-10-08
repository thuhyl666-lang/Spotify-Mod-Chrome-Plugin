# Dust Strike — CS:GO-inspired browser FPS

A single-file (`index.html`) 5v5 tactical shooter built with Three.js r128. Everything is generated at runtime: textures, map, weapons, skins and sound. No asset files.

**Run it:** open `index.html` in a desktop browser, or serve the folder (`npx serve csgo-fps`). Three.js, `BufferGeometryUtils` and `PointerLockControls` load from cdnjs and jsDelivr, so you need an internet connection.

## Features
- **Map:** a dust2/Mirage-style layout with Long A (with doors), Short A catwalk and a balcony over Long, Mid with mid doors, Upper and Lower tunnels, and bomb sites A and B with raised platforms, stairs, arches, crates, barrels and cars.
- **Rendering:** about 30–40 draw calls. Static geometry is merged per material with `BufferGeometryUtils.mergeBufferGeometries`, ambient occlusion is baked into vertex colors, and bots are drawn as `InstancedMesh` parts. A single 1024² sun shadow map follows the player, and adaptive resolution keeps the frame rate near 60 FPS.
- **Weapons:** knife, Glock-18, USP-S, Desert Eagle, AK-47, M4A4 (with a silencer toggle) and AWP (two zoom levels with a scope overlay). Rifles have CS-style spray patterns, every weapon has movement, jump and crouch spread, a dynamic crosshair and inspect, reload and draw animations. Wood can be shot through.
- **Damage:** head ×3, torso ×1, legs ×0.75. Kevlar and the helmet reduce damage by each weapon's armor-penetration value. Headshot kills show a HEADSHOT banner.
- **Economy:** you start with $800, earn $300 per kill ($1000 for knife kills), $3250 for a round win, and a growing loss bonus. Press **B** to buy during the buy phase while in spawn.
- **Bomb:** Terrorists plant (3.2 s); Counter-Terrorists defuse (5 s, or 2.5 s with a kit).
- **Bot AI:** a state machine (Patrol → Alerted → Engage / Cover → Reload, plus Plant and Defuse) on top of an A* navigation grid, with raycast line-of-sight, hearing, team callouts, CT rotations, varying accuracy and Easy, Normal and Hard difficulty.
- **Effects:** pooled particles, bullet-hole and blood decals, tracers, muzzle flashes and shell casings.
- **Audio:** every sound is synthesized with the Web Audio API and played through a pooled set of positional voice chains.
- **Cases:** a roulette case opener with five rarity tiers (50 / 30 / 15 / 4 / 1 %), wear values and StatTrak. Equipped skins repaint the 3D weapon models immediately, and the inventory is saved in `localStorage`.

## Controls
| Key | Action |
| --- | --- |
| WASD / Mouse | Move / aim (LMB fire, RMB scope, silencer or heavy stab) |
| Space · C · Shift | Jump · crouch · walk |
| 1 2 3 · Q · wheel | Weapon slots · last weapon · cycle |
| R · F | Reload · inspect |
| B · E · Tab · Esc | Buy · plant/defuse · scoreboard · pause |
