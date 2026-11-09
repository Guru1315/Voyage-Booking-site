# How it was built

- **Read the reference.** The repo turned out to be a full Next.js app, not just docs. Despite its "cafe" name, its page is **NAVIS**, a luxury cruise landing page with three 300-frame scroll sequences. Its `UI layout/` folder holds four phone screenshots of a different design (a cocktail bar called ONDA), which NAVIS borrows its section rhythm from. The rebuild follows the page the code actually renders.
- **Mapped sections to files.** Ten sections became small components: a shared frame-sequence hook, the hero, a reusable chapter, cards, galleries, about, and plan/CTA.
- **Copied the real assets.** That means 600 scroll frames and 28 photos. A third frame folder in the repo was left out because no rendered section uses it.
- **Ported the code.** The original used inline styles everywhere. These were moved into one scoped stylesheet, and the values were kept: sizes, colors, timings and easing curves.
- **Fixed what the original left broken.** Its buttons did nothing (they now scroll to sections or open the booking email). A section label was hidden under the fixed nav. And it had no phone layout.
- **Checked it.** Lint, typecheck and production build all pass. Headless-Chrome passes at 1440px and 390px compare the measured geometry with the original's values, and drive every interaction with real wheel, mouse and touch input.

### 2. Ship it

```text
Push and deploy
```

```text
https://github.com/Guru1315/3D-cafe-site push here
```

### 3. Point the root at the page

```text
Yes, redirect it
```

This added a `/` → `/cafe` redirect, so **https://3d-cafe-site-iota.vercel.app** opens straight on NAVIS.

### 4. Turn the repo into a showcase

```text
push and commit only what are the assessts and screenshots and how it done and how it works if otherthen this commited kindly remove and add this only also make 3d animated README section with the live demo
```

This replaced the repo's contents with this showcase:

- screenshots from the live site at desktop and phone width
- `assets/hero-scroll.gif`, recorded by scrolling the live hero in headless Chrome
- `assets/banner.svg`, a hand-written animated SVG: waves roll toward you over a perspective ocean, a ship sails closer, and a frame counter runs
- filmstrips of both frame sequences
- this file and [HOW-IT-WORKS.md](HOW-IT-WORKS.md)
