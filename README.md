<div align="center">

<a href="https://3d-cafe-site-iota.vercel.app"><img src="assets/banner.svg" alt="NAVIS: a cruise ship sailing over a 3D perspective ocean while a frame counter runs" width="100%"></a>

# NAVIS · 3D Scroll Experience

A scroll-driven cruise landing page. As you scroll, 300-frame image sequences play on a canvas, story captions appear, and you pass hover-tilt cards, galleries, a looping dining strip and a nightlife grid.

[![Live demo](https://img.shields.io/badge/LIVE_DEMO-3d--cafe--site--iota.vercel.app-2563eb?style=for-the-badge&logo=vercel&logoColor=white)](https://3d-cafe-site-iota.vercel.app)

![Next.js](https://img.shields.io/badge/Next.js-16-000?logo=nextdotjs) ![GSAP](https://img.shields.io/badge/GSAP-ScrollTrigger-88ce02?logo=greensock&logoColor=white) ![Canvas](https://img.shields.io/badge/Canvas_2D-600_frames-3b82f6) ![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178c6?logo=typescript&logoColor=white) ![Built with Claude Code](https://img.shields.io/badge/built_with-Claude_Code-d97757)

</div>

---

## 🎬 The 3D scroll, live

<div align="center">

<a href="https://3d-cafe-site-iota.vercel.app"><img src="assets/hero-scroll.gif" alt="Scrolling the hero: clouds part, a cruise ship sails into view, then the camera moves into the grand lobby while captions change" width="100%"></a>

<sub>Recorded from the live site. Every frame of the camera move comes from your scroll position, not a video. Click it to open the demo.</sub>

</div>

**Try these on the live site:**

| | |
|---|---|
| 🖱️ **Scroll slowly** through the hero: the camera flies from the clouds to the ship to the lobby | 🔁 **Scroll back up**: the sequence plays in reverse |
| 🃏 **Hover the experience cards**: the card widens and tilts toward your pointer | ⬅️➡️ **Arrows** under the cards step through them |
| 🖼️ **Hover any gallery photo** to see its caption | 🛳️ **Move over the fleet card** in "The Ocean Is Your World." to tilt it |
| 📱 **On a phone**, tap a card to open it | 🧭 **Nav links** jump to each section |

---

## 📸 Screenshots

All taken from the live deployment at 1440 × 900.

<table>
  <tr>
    <td width="50%"><img src="screenshots/desktop/01-hero.jpg" alt="Hero: Built for the Open Sea"><br><sub><b>Hero</b>: frame 1, intro copy over the clouds</sub></td>
    <td width="50%"><img src="screenshots/desktop/02-hero-story.jpg" alt="Hero story caption over the ship"><br><sub><b>Hero, mid-scroll</b>: "The Engineering" caption</sub></td>
  </tr>
  <tr>
    <td><img src="screenshots/desktop/03-experience-hover.jpg" alt="Experience cards, third card open and tilted"><br><sub><b>Everything You Need At Sea</b>: hover widens and tilts a card</sub></td>
    <td><img src="screenshots/desktop/04-pool-hover.jpg" alt="Pool gallery with a hovered tile"><br><sub><b>Swimming Pool &amp; Drinks</b>: hover reveals the caption</sub></td>
  </tr>
  <tr>
    <td><img src="screenshots/desktop/05-craft.jpg" alt="Craftsmanship chapter in the lobby"><br><sub><b>NAVIS Craftsmanship</b>: second scroll sequence</sub></td>
    <td><img src="screenshots/desktop/06-dining.jpg" alt="Fine dining marquee"><br><sub><b>Fine Dining at Sea</b>: looping photo strip</sub></td>
  </tr>
  <tr>
    <td><img src="screenshots/desktop/07-night.jpg" alt="Nightlife bento grid"><br><sub><b>The Day Is Yours</b>: nightlife bento</sub></td>
    <td><img src="screenshots/desktop/08-about.jpg" alt="About section with stats and tilt card"><br><sub><b>The Ocean Is Your World.</b>: stats and a 3D tilt card</sub></td>
  </tr>
  <tr>
    <td><img src="screenshots/desktop/09-voyage.jpg" alt="Voyage chapter"><br><sub><b>The NAVIS Experience</b>: third scroll sequence</sub></td>
    <td><img src="screenshots/desktop/10-plan.jpg" alt="Plan your visit and CTA"><br><sub><b>Set Sail With NAVIS</b>: info and booking card</sub></td>
  </tr>
</table>

### 📱 On phones (390 px)

<table>
  <tr>
    <td><img src="screenshots/mobile/01-hero.jpg" alt="Mobile hero"></td>
    <td><img src="screenshots/mobile/02-hero-story.jpg" alt="Mobile hero caption"></td>
    <td><img src="screenshots/mobile/03-experience.jpg" alt="Mobile experience cards"></td>
    <td><img src="screenshots/mobile/04-pool.jpg" alt="Mobile pool gallery"></td>
  </tr>
  <tr>
    <td><img src="screenshots/mobile/05-night.jpg" alt="Mobile nightlife"></td>
    <td><img src="screenshots/mobile/06-about.jpg" alt="Mobile about"></td>
    <td><img src="screenshots/mobile/07-voyage.jpg" alt="Mobile voyage chapter"></td>
    <td><img src="screenshots/mobile/08-plan.jpg" alt="Mobile plan and CTA"></td>
  </tr>
</table>

---

## 🛠️ How it works

<img src="assets/frames-hero.jpg" alt="Six frames from the 300-frame hero sequence: clouds, ship appearing, ship close-up, lobby" width="100%">

- **Scroll is the playhead.** Each 3D section is a 500vh-tall block with a sticky full-screen canvas inside. GSAP ScrollTrigger turns scroll progress into a frame number (0–299), and that frame is drawn "cover"-fit onto the canvas.
- **Three sequences, 600 frames.** The hero and the craftsmanship chapter play the same 300 hero frames from one shared image cache. The voyage chapter plays another 300.
- **Captions follow frame ranges.** For example, frames 130–180 show "The Engineering". Chapter dots track the current scene.
- **No blank canvas while loading.** Frames preload in the background, and until a frame arrives the nearest earlier loaded frame is shown.
- **3D tilt with CSS.** Cards use `perspective`, `rotateX/rotateY` from the pointer position, and a radial "shine" that follows the cursor.

Full details are in **[HOW-IT-WORKS.md](HOW-IT-WORKS.md)**.

## 💬 How it was built

Rebuilt with Claude Code from a handful of prompts, starting with:

```text
/clone-website https://github.com/alagappan567/cafe-3d-scroll
```

**[HOW-IT-WAS-BUILT.md](HOW-IT-WAS-BUILT.md)** lists every prompt word for word, with what each one did: reading the reference, porting it, testing at desktop and phone width, and deploying.

This repo holds the showcase only: screenshots, recordings and write-ups. The site's source code isn't included.

## 🙏 Credits

- Design, copy, photos and frame sequences come from **[alagappan567/cafe-3d-scroll](https://github.com/alagappan567/cafe-3d-scroll)**. This is an independent rebuild of that repo's page.
- Built with [Claude Code](https://claude.com/claude-code).

> **Concept site.** NAVIS is a fictional cruise line. "Book a Voyage" and the contact details are placeholders: nothing is booked or sold.
