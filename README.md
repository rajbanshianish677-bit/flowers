# 🌸 Programmer's Flowers

> Three luminous blossoms, grown line-by-line from pure SVG geometry.

A premium interactive generative flower gallery — **hand-coded entirely from SVG paths, gradients, and filters**. No images. No frameworks. No external requests. Everything you see is geometry, math, and light.

![Type](https://img.shields.io/badge/pure-SVG%20%2B%20CSS%20%2B%20JS-ff6b9c) ![Dependencies](https://img.shields.io/badge/dependencies-0-c9a7ff) ![Images](https://img.shields.io/badge/images-0-ffc94d)

---

## 🌹 The Collection

| Flower                   | Meaning             | Details                                                                           |
| ------------------------ | ------------------- | --------------------------------------------------------------------------------- |
| 🌹 **Rose** — _Passion_  | Deep crimson layers | 60 petals across 8 rings, phyllotaxis spiral heart, rim-light strokes, dew drops  |
| 🌸 **Lily** — _Elegance_ | Lavender whorls     | 22 petals in 3 whorls, dorsal stripes, freckles, stamens with drifting pollen     |
| 🌻 **Sunflower** — _Joy_ | Golden radial burst | 84 petals, 170 spiral seeds (golden angle 137.5°), glowing disc, sheen highlights |

Each flower grows on a **complete plant** — a self-drawing stem, alternating leaves that unfold as the stem grows, and a green calyx of sepals beneath the blossom.

---

## ✨ Features

- **Generative botany** — every petal, seed, and leaf is placed by code using golden-angle phyllotaxis and layered gradients
- **Blooming animations** — staggered per-petal delays with springy `cubic-bezier` easing; click any flower to re-bloom it
- **Particle system** — a single lightweight canvas renders ambient star-dust, click bursts, sunflower gold motes, and falling petals
- **Staged gallery** — one flower on stage at a time; navigate with ‹ › buttons, dots, or ← → arrow keys
- **Cinematic theme** — dark nebula backdrop, glass cards, breathing halos, film grain, and a vignette
- **Zero dependencies** — one HTML file, ~60 KB, works offline

## 🚀 Usage

Just open it:

```bash
# any static server works
python3 -m http.server 8737
# then visit http://localhost:8737
```

Or simply double-click `index.html` — no build step, no install.

## 🎮 Interactions

| Action                      | Effect                                                  |
| --------------------------- | ------------------------------------------------------- |
| **Hover** a flower          | Glow intensifies, label reveals, gentle sway            |
| **Click** a flower          | Re-bloom + light ripple + particle burst at your cursor |
| **‹ › / dots / arrow keys** | Flip between flowers                                    |
| **Wait**                    | Ambient dust drifts, sunflower sheds gold, petals fall  |

## 🛠️ How It's Built

- **Petals** — SVG `<path>` shapes with per-petal CSS custom properties (`--d` delay, `--p0` closed transform, `--dur` duration) driving springy bloom transitions
- **Seeds** — placed by phyllotaxis: `r = c·√n`, `θ = n·137.5°`
- **Stems** — `stroke-dashoffset` animation makes the stem _grow_ upward from the ground
- **Leaves & sepals** — double-wrapped `<g>` elements: outer group carries the SVG positioning transform, inner group carries the CSS bloom animation (a CSS transform would otherwise override the attribute)
- **Particles** — pre-rendered radial-gradient sprites drawn to one fixed canvas; types: ambient (`a`), burst (`b`), gold (`e`), petal (`p`)
- **Reduced motion** — respects `prefers-reduced-motion` with lighter ambient effects

## 📁 Project

```
index.html   ← the entire site (HTML + CSS + SVG + JS)
README.md
```

---

_hand-coded svg · no images · no frameworks_
