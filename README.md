# 🌸 Flowers

A premium interactive generative flower gallery — **hand-coded entirely from SVG paths, gradients, and filters**. No images. No frameworks. No external requests. Everything you see is geometry, math, and light.

![Type](https://img.shields.io/badge/pure-SVG%20%2B%20CSS%20%2B%20JS-ff6b9c) ![Dependencies](https://img.shields.io/badge/dependencies-0-c9a7ff) ![Images](https://img.shields.io/badge/images-0-ffc94d)

---

## 🌹 The Collection

| Flower                            | Meaning             | Details                                                                                                             |
| --------------------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------- |
| 🌹 **Rose** — _Passion_           | Deep crimson layers | 60 petals across 8 rings, phyllotaxis spiral heart, rim-light strokes, dew drops                                    |
| 🌸 **Oriental Lily** — _Elegance_ | Bold magenta star   | 18 broad star petals in 3 whorls, white rims, ruffled recurved edges, dark-pink speckles, long yellow-green stamens |
| 🌻 **Sunflower** — _Joy_          | Golden radial burst | 84 petals, 170 spiral seeds (golden angle 137.5°), glowing disc, sheen highlights                                   |

Each flower grows on a **complete plant** — a self-drawing stem, alternating leaves that unfold as the stem grows, and a green calyx of sepals beneath the blossom.

---

## ✨ Features

- **Generative botany** — every petal, seed, and leaf is placed by code using golden-angle phyllotaxis and layered gradients
- **Dramatic Oriental lily** — six-pointed magenta star with white-edged, ruffled petals that curve outward, speckled throats, and long yellow-green stamens rising from a green-gold heart
- **Blooming animations** — staggered per-petal delays with springy `cubic-bezier` easing; click any flower to re-bloom it
- **Swipe navigation** — on touch devices, swipe left/right to flip flowers (rose → lily → sunflower, wrapping around)
- **Mobile auto-fit** — on phones the page becomes exactly one screen: header, nav, and footer shrink while the flower card absorbs every remaining pixel — no scrolling, any orientation
- **Particle system** — a single lightweight canvas renders ambient star-dust, click bursts, sunflower gold motes, and falling petals
- **Staged gallery** — one flower on stage at a time; navigate with ‹ › buttons, dots, arrow keys, or swipes
- **Cinematic theme** — dark nebula backdrop, glass cards, breathing halos, film grain, and a vignette
- **Zero dependencies** — one HTML file, ~76 KB, works offline

## 🚀 Usage

Just open it:

```bash
# any static server works
python3 -m http.server 8737
# then visit http://localhost:8737
```

Or simply double-click `index.html` — no build step, no install.

## 🎮 Interactions

| Action                         | Effect                                                  |
| ------------------------------ | ------------------------------------------------------- |
| **Hover** a flower             | Glow intensifies, label reveals, gentle sway            |
| **Click / tap** a flower       | Re-bloom + light ripple + particle burst at your cursor |
| **‹ › / dots / arrow keys**    | Flip between flowers                                    |
| **Swipe left / right** (touch) | Next / previous flower, wrapping around                 |
| **Wait**                       | Ambient dust drifts, sunflower sheds gold, petals fall  |

---

## 📐 Document Anatomy

Everything lives in one file — `index.html` (~1,970 lines, ~76 KB). The document is organized into four top-level blocks:

```
index.html
├── <head> … <style>          CSS — 7 numbered sections (see below)
├── <body>
│   ├── .noise, .vignette    atmospheric layers (fixed, pointer-transparent)
│   ├── #fx                  particle canvas (fixed, above the garden)
│   ├── #assets              hidden SVG <defs>: 1 filter, ~25 gradients
│   ├── <header.site-head>   title, subtitle, hint, divider
│   ├── <nav.stage-nav>      ‹ button · 3 dots · › button
│   ├── <main.garden>        the stage — 3 stacked flower cards
│   └── <footer.site-foot>   colophon
└── <script>                 one IIFE: builders, particles, interactions
```

### CSS section map (inside `<style>`)

| §   | Section              | What it covers                                                                                            |
| --- | -------------------- | --------------------------------------------------------------------------------------------------------- |
| 1   | Base & atmosphere    | reset, body nebula wash, film-grain `.noise`, `.vignette`, `#fx` canvas                                   |
| 2   | Header               | `.site-head`, gradient `.title` with glow animation, `.subtitle`, `.divider` vine                         |
| 3   | Garden & cards       | `.garden` grid, `.flower-card` glass environment (all 3 cards share one grid cell — only `.active` shows) |
| 4   | Labels & ripple      | `.flower-label` reveal, `.ripple` click effect                                                            |
| 4b  | Stage navigation     | `.nav-btn` round buttons, `.stage-dots`                                                                   |
| 5   | SVG animation system | arcs/loops, `.petal` bloom transitions, `.stem` draw-on, `.leaf`/`.sepal` unfold, seeds, dew, sparks      |
| 6   | Keyframes            | `spin`, `breathe`, `sway`, `hoverSway`, `dashFlow`, `sparkDash`, `nodePulse`, `rip`, `sweep`, `titleGlow` |
| 7   | Responsive & motion  | media queries (below)                                                                                     |

### Media queries (§ 7)

| Query                                         | Purpose                                                                                                                                                                  |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `(max-width:640px), (max-height:520px)`       | **Auto-fit layout**: page becomes a flex column exactly one screen tall; blossoms resized so petals never clip; tap-zoom disabled so the flower stays pinned on its stem |
| `└ (orientation:landscape)` (nested)          | Card width yields to tight height                                                                                                                                        |
| `(max-width:380px)`                           | Very small phones — smaller type, tighter nav                                                                                                                            |
| `(max-height:480px) and landscape`            | Landscape phones — compact header band, footer hidden                                                                                                                    |
| `(hover:none)`                                | Touch devices — labels stay visible once bloomed                                                                                                                         |
| `(prefers-reduced-motion:reduce)`             | Animations off, faster petal transitions                                                                                                                                 |
| `(max-width:640px), (prefers-reduced-motion)` | Low-end tier — no backdrop blur, no title animation, fewer particles (JS)                                                                                                |

### SVG asset inventory (`#assets`, hidden)

- **Filter**: `fGlow` — gaussian blur + merge for glowing nodes
- **Rose**: `roseHalo`, `rCore`, petal ramps `rg0`–`rg4`, `rgGuard`, `rShadow`, `rRim`
- **Lily**: `lilyHalo`, `lgOuter`, `lgInner`, `lgBack`, `lDorsal`, `lShadow`, `lgCenter`, `lilySweep`
- **Sunflower**: `sunHalo`, `sgOuter`, `sgInner`, `sgBack`, `sgCore`, `sgDisc`, `sgRim`
- **Plant**: `stemGrad`, `leafGrad`, `leafVein`, `sepalGrad`
- **Clip**: `lilyClip` — petal silhouette for the light sweep (built in JS)

### Flower card structure (×3, inside `.garden`)

```
<section.flower-card>            glass environment; --accent / --glow per species
├── .card-glow                   soft radial wash
├── svg.flower-svg               viewBox="-250 -250 500 500" (centered coords)
│   ├── g.decor                  rotating arcs + flowing energy loops (JS-built)
│   ├── circle.halo (+.halo-boost)
│   └── g.flower
│       ├── g.plant              stem + leaves + sepals (JS-built)
│       └── g.flower-hover       hover sway wrapper
│           └── g.flower-live    idle sway wrapper
│               ├── g.petals     all petals (JS-built)
│               └── g.core       heart / disc / stamens (JS-built)
└── .flower-label                emoji · name · meaning
```

> **Why the nested wrappers?** Each level carries exactly one CSS transform
> (`translate` on `.flower-hover`, `rotate/scale` animation on `.flower-live`),
> so they compose instead of overriding each other. All use
> `transform-box: fill-box` — pivoting around each element's own center —
> which is what keeps the blossoms perfectly centered (the viewBox origin is
> `(-250,-250)`, so `view-box` percentages would pivot around the wrong corner).

### Script map (one IIFE, ~650 lines)

| Block                     | Contents                                                                                                                                                               |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Helpers                   | `$`/`$$` queries, `rnd`, `pick`, `E()` SVG element factory                                                                                                             |
| Path constants            | `ROSE_MAIN`, `LILY_PETAL`, `SUN_PETAL`, leaf/sepal shapes…                                                                                                             |
| `ROSE_RINGS`              | 8-ring config: count, offset, scale, gradient, delay, shape                                                                                                            |
| `buildRose()`             | 8 petal rings + phyllotaxis heart + dew drops                                                                                                                          |
| `buildLily()`             | 3 petal whorls + freckles + stamens/pistil + pollen + sweep clip                                                                                                       |
| `buildSunflower()`        | sepals + 3 ray rings + disc + 170 spiral seeds + florets                                                                                                               |
| `buildPlant(f)`           | self-drawing stem, alternating leaves, calyx of sepals                                                                                                                 |
| `buildDecor(svg, accent)` | concentric arcs, energy loops, glowing nodes                                                                                                                           |
| `F` registry              | per-flower card/svg/group refs, build fn, palette, accent                                                                                                              |
| `setBloom` / `rebloom`    | bloom once; click re-bloom with compressed delays (`.fast`)                                                                                                            |
| Particle engine           | `#fx` canvas, DPR-capped resize, cached radial sprites, `frame()` rAF loop, ambient/burst/gold/petal types, `setInterval` emitters                                     |
| `excite` / `ripple`       | temporary glow class; click-point light ripple                                                                                                                         |
| Events                    | card click/keydown (viewport-coord bursts), arrow keys, dot/nav clicks, **touch swipe** (42px threshold, 1.3× horizontal bias, click-guard so a swipe never re-blooms) |
| `showStage(i)`            | flips `.active` card + dot, first-visit auto-bloom                                                                                                                     |
| Init                      | build all flowers & plants & decor → `showStage(0)`                                                                                                                    |

---

## 🛠️ How It's Built

- **Petals** — SVG `<path>` shapes with per-petal CSS custom properties (`--d` delay, `--p0` closed transform, `--dur` duration, `--ease` spring) driving bloom transitions
- **Seeds** — placed by phyllotaxis: `r = c·√n`, `θ = n·137.5°`
- **Stems** — `stroke-dashoffset` animation makes the stem _grow_ upward from the ground
- **Leaves & sepals** — double-wrapped `<g>` elements: outer group carries the SVG positioning transform, inner group carries the CSS bloom animation (a CSS transform would otherwise override the attribute)
- **Particles** — pre-rendered radial-gradient sprites drawn to one fixed canvas; types: ambient (`a`), burst (`b`), gold (`e`), petal (`p`); hard ceiling + device tiering (`LOW` on phones / reduced-motion / single-core)
- **Centering** — all animated groups use `transform-box: fill-box; transform-origin: center`, so rotations and scales pivot around each element's own geometry; with the `(-250,-250)` viewBox, percentage origins against `view-box` would resolve to the visible area's corner and slide flowers sideways
- **Mobile pinning** — on small screens the svg-level hover/tap zoom is disabled, so touching a flower re-blooms it without sliding the blossom down over the stem and leaves
- **Reduced motion** — respects `prefers-reduced-motion` with lighter ambient effects

## 📁 Project

```
index.html   ← the entire site (HTML + CSS + SVG + JS)
README.md
```

---

_hand-coded svg · no images · no frameworks_
