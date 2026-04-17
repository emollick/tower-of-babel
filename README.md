# The Tower of Babel

> *"And the whole earth was of one language, and of one speech…*
> *Go to, let us build us a city and a tower, whose top may reach unto heaven."*
> — **Genesis 11:1,4**

An interactive 3D scene. A spiraling ziggurat rises from a desert plain, through a belt of clouds, and into a gathering storm. Workers climb its ramps. Altars burn. Banners wave. Click the tower, and the confusion of tongues rises in ancient scripts.

**Live:** https://tower-of-babel-1776392618.netlify.app

Built with Three.js. A single self-contained `index.html` — no build step, no bundler, no npm.

---

## What you'll see

A Mesopotamian ziggurat hand-composed from procedural geometry:

- **Nine stepped tiers** of decreasing radius, each with canvas-generated stone, masonry seams, and a normal map
- **A spiral ramp** that wraps the tower from foundation to summit, with 140 instanced workers walking up and down
- **Scaffolding and unfinished stonework** on the upper tiers — jagged stones, timber poles, diagonals
- **Arched windows** extruded from real curves, with stone frames and glowing panes that brighten at night
- **Grand doorways** at the base, firelit and inviting
- **Burning altars** on four tiers, each with a stepped plinth, bronze bowl, flickering point-light, additive-blended fire particles, and a dark smoke column that swirls and drifts
- **Banners** on the upper tiers — segmented flags that wave physically, their motion intensifying with the storm
- **A reflective water moat** ringing the base, framed in stone
- **Scattered quarry blocks, rubble, dust motes, and rising embers** around the construction site

And above and beyond:

- **Atmospheric sky** from the Three.js Sky shader, with a real sun that moves across the hours
- **5,000-star night sky** with twinkling shader, colored tints, and a Milky Way band
- **A procedurally textured moon** with maria and craters, orbiting opposite the sun, with a soft halo
- **A layered cloud belt** wrapping the upper tower, darkening into a storm cap at the peak
- **Lightning strikes** that branch from the clouds, with a flash point-light and secondary forks
- **Rain** — 2,500 shader-based streaks that fall when storms rise
- **Birds** circling the tower at various radii and heights
- **Thunder** — procedurally generated audio bursts that follow strikes with a delay
- **Filtered wind and a low drone** for ambient atmosphere

---

## How to interact

| Action | Effect |
|---|---|
| Drag | Orbit the camera around the tower |
| Scroll | Zoom |
| **Click the tower** | The confusion of tongues rises from that tier — cuneiform, hieroglyphs, Phoenician, Hebrew, Greek, runic, tifinagh, and more. A themed caption appears. |
| **Hour of Day** slider | Sweep a full day-night cycle. Dawn and dusk stain the stone; windows glow at night; the moon and stars appear. |
| **Storm** slider | Darken the clouds, raise the rain, unleash lightning |
| **Ascend to the Heavens** | Cinematic tween to the peak |
| **Descend to the Plain** | Cinematic tween to ground level |
| **Confound Their Tongues** | A column of divine light descends from heaven. The storm breaks. Lightning strikes repeatedly. Stones shear from the top and fall. A flight of 160 ancient glyphs scatters from the summit. |

Click anywhere once to unlock ambient audio (browsers require user interaction).

---

## Under the hood

Everything is generated at runtime. The tower, the stones, the moon, the Milky Way, the cloud sprites, the fire — all come from canvas and shader code in `index.html`. No textures, no models, no asset pipeline.

Some pieces worth a look:

- `makeStoneTexture` — layered sine + random noise with drawn masonry seams and weathering splotches, compiled into a `CanvasTexture`
- `buildTier` — each ziggurat tier: cylinder body, crenellations with missing-stone probability, decorative band, arched windows extruded from a `THREE.Shape`, and on the top tier, jagged incomplete stones
- `buildSpiralRamp` — 280 small angled box segments following the shrinking tier radii, with parapet walls
- **Starfield shader** — vertex-sized twinkling points with cross-flare fragments, biased toward a galactic band
- **Divine beam shader** — additive cylindrical column with UV-edge soft falloff and a time-driven pulse
- **Procedural moon** — radial gradient base, maria as darker radial gradients, crater dots with highlight rims
- **Rain** — shader-based streak points with vertically elongated UV falloff, opacity driven by the storm slider
- **Thunder** — `AudioContext` buffer of white noise with exponential envelope, lowpass filtered to around 180 Hz

Post-processing: `UnrealBloomPass` (strength scales with night), `FilmPass` for grain, `ACESFilmicToneMapping`, and a CSS vignette layer.

---

## Running locally

It's a single HTML file that loads Three.js over `importmap` from unpkg. To run:

```bash
# Easy way — just open it
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux

# If your browser blocks module imports from file://,
# serve it instead:
python -m http.server 8080
# then http://localhost:8080
```

No install step, no dependencies to fetch. The whole scene is ~2,700 lines of HTML/CSS/JS in one file.

---

## Stack

- **[Three.js](https://threejs.org/) r160** — rendering, Sky shader, OrbitControls, Reflector, EffectComposer
- **Canvas 2D** — every texture is drawn in JavaScript
- **Web Audio API** — wind, drone, thunder
- **GLSL** — custom shaders for stars, rain, and the divine beam
- A little patience, and the Book of Genesis

---

## Credits

Inspired by Pieter Bruegel the Elder's *Tower of Babel* (1563), the ziggurats of Ur and Etemenanki, and the brief, staggering eleventh chapter of Genesis.

Built by Claude (Opus 4.7) in collaboration with [@emollick](https://github.com/emollick).

---

> *"Therefore is the name of it called Babel;*
> *because the Lord did there confound the language of all the earth."*
