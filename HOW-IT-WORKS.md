# How it works

The live site is at **https://guru-voyage-booking.vercel.app/**. It's one page, built with Next.js 16, React 19, TypeScript, GSAP ScrollTrigger and a 2D canvas. There's no WebGL. The "3D" comes from pre-rendered camera moves played back by scroll, plus CSS perspective.

## Page order

| # | Section | What moves |
|---|---|---|
| 0 | Preloader | NAVIS wordmark shimmer, progress bar (2.6s, then a 0.9s fade) |
| – | Nav and ticker | Frosted fixed nav; blue ticker at the bottom loops every 30s and pauses on hover |
| 1 | **Hero**: "Built for the Open Sea" | 300-frame scroll sequence, intro fades out, 4 captions |
| 2 | Everything You Need At Sea | Accordion cards with pointer tilt and shine |
| 3 | Swimming Pool & Drinks | Hover gallery |
| 4 | **NAVIS Craftsmanship** | Scroll sequence (hero frames) with 4 chapters and dots |
| 5 | Fine Dining at Sea | Endless photo marquee (36s loop) |
| 6 | The Day Is Yours | Nightlife bento with a purple hover wash |
| 7 | The Ocean Is Your World. | Stats and a 3D tilt card with a moving glow |
| 8 | **The NAVIS Experience** | Scroll sequence (voyage frames) with 4 chapters |
| 9 | Plan Your Visit | Info columns and the "Set Sail With NAVIS" card |

## 1. Scroll-scrubbed frame sequences

![Six frames from the voyage sequence](assets/frames-voyage.jpg)

Each sequence is a tall block (`height: 500vh`) with a sticky, full-viewport stage inside. The stage holds a `<canvas>`, two gradient shades for legibility, and the captions.

```text
on mount:
  images = cache[folder] ?? preload 300 JPEGs (1920×1080), frame 1 first
  size canvas to the viewport × devicePixelRatio (capped at 2)

ScrollTrigger(trigger = block, start = "top top", end = "bottom bottom"):
  onUpdate(progress):
    frame = floor(progress × 299)
    if frame changed:
      draw images[frame] cover-fit (scale = max(cw/iw, ch/ih), centred)
        — if not loaded yet, draw the nearest earlier frame that is
      scene = the caption whose [from, to] range contains frame
```

- The hero and the craftsmanship chapter use the **same 300 hero frames**, so one shared cache means each file downloads once.
- **Hero captions** only show inside their ranges (60–110, 130–180, 200–248, 260–299), so the picture sits clear between them. **Chapter captions** stay on the last scene between ranges, and four dots show progress.
- The hero intro (headline, buttons) fades out and rises 40px over the first 8% of the block, using a second, scrubbed ScrollTrigger tween.
- Scrolling up plays everything in reverse, because frame and caption are pure functions of scroll position.

## 2. Pointer-driven 3D tilt

```text
on pointer move over card:
  x, y = pointer position inside the card, 0..1
  rotateX = (y − 0.5) × −14°    rotateY = (x − 0.5) × 14°
  shine   = radial-gradient(circle at x% y%, white 10% → transparent)
on leave: ease back to flat
```

- **Experience cards** sit in a flex row with `perspective: 1200px`. The open card gets `flex: 3.2` (the others stay at 1), so it widens with a 0.55s ease. Its text layers sit at `translateZ(20–30px)`, so they float above the photo as it tilts. Leaving the row reopens card 1, and the arrow buttons step through the cards.
- **The fleet card** in the about section tilts ±9°, scales to 1.02, and a blue glow behind it follows the pointer.

## 3. Galleries

- **Hover tiles** (pool and nightlife) are CSS-only. On hover the photo zooms to 1.06–1.08, a darker gradient fades in, the label lifts, and the description and ↗ arrow appear. These effects only apply under `@media (hover: hover)`, so taps on phones don't leave tiles stuck open. Keyboard focus shows the same state.
- **The dining marquee** repeats eight photos twice in a row and slides the track by −50% on a 36s linear loop, so the loop is seamless.

## 4. Phones (under 768px)

The original page was desktop-only. On phones the rebuild keeps every section, in the same order:

- the nav shows only the logo
- hero copy uses the full width
- experience cards stack vertically: the open card is 3.2× taller, and closed cards become one-line strips
- the pool and nightlife grids use two columns
- the about section and the info columns stack

At 390px nothing scrolls sideways.

## 5. Checked in a real browser

Automated headless-Chrome passes on the live site, at 1440×900 and 390×844:

- wheel scrolling drives the hero
- captions appear at the right frames
- all 4 scenes and dots work in both chapters
- card hover, leave, arrows and tap
- tile hover, fleet tilt, the marquee moving, and nav anchors
- no horizontal overflow, console errors, failed requests or broken images
