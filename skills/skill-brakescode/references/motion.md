# Motion

## Contents

- [Two tiers](#two-tiers)
- [Durations](#durations)
- [Easing](#easing)
- [The signature moment](#the-signature-moment)
- [Loading states](#loading-states)
- [Reveals](#reveals)
- [Scroll](#scroll)
- [Reduced motion](#reduced-motion)
- [Performance rules](#performance-rules)

## Two tiers

Almost every bad animation decision comes from applying one speed to everything. There are two kinds of motion and they obey opposite rules.

**Functional motion** answers the user. A hover, a press, a toggle, a menu opening. Its job is to be *felt and not noticed* — it confirms that the interface heard you. It must be fast. Anything the user triggered and then has to wait for is a tax they pay every time.

**Expressive motion** says something. The reveal, the transition between projects, the one moment that makes the site memorable. Its job is to be noticed. It can be slow — genuinely slow — because the user isn't waiting on it to accomplish a task.

Confusing the two is the single most common failure: expressive timing applied to a button (sluggish), or functional timing applied to the signature moment (cheap and hurried).

## Durations

| Motion | Duration | Tier |
|---|---|---|
| Hover, focus ring, color shift | 120–160ms | functional |
| Press / active state | 80–120ms | functional |
| Toggle, checkbox, small state change | 160–200ms | functional |
| Dropdown, tooltip, popover | 180–240ms | functional |
| Modal, drawer, sheet | 300–400ms | functional |
| Card or list-item entrance | 400–600ms | expressive |
| Section reveal on scroll | 600–800ms | expressive |
| Page or route transition | 600–900ms | expressive |
| Subject/ground color change | 1000–1400ms | expressive |
| **The signature moment** | **1.5s–20s** | expressive, once |

Stagger between siblings: **40–80ms**. Below 40ms it reads as simultaneous; above ~100ms the last item arrives late enough to feel broken. For a word-by-word text reveal, 40–50ms is the sweet spot.

Cap total stagger at ~600ms. Twenty items at 60ms is 1.2 seconds before the last one lands — too long. When the list is long, stagger the first six and bring the rest in together.

## Easing

**No bounce.** Not one reference site overshoots. Spring physics with overshoot reads as playful, and this house is not playful — it's precise. Bounce is a deliberate exception you can justify, never the default.

Everything decelerates. Motion should arrive and settle, not launch.

```css
--ease-out:   cubic-bezier(0.22, 1, 0.36, 1);    /* default for reveals + entrances */
--ease-expo:  cubic-bezier(0.16, 1, 0.30, 1);    /* dramatic; the signature moment */
--ease-micro: cubic-bezier(0.40, 0, 0.20, 1);    /* hover, press, small states */
--ease-inout: cubic-bezier(0.65, 0, 0.35, 1);    /* only for things that both start and stop offscreen */
```

Use `--ease-out` unless you have a reason. `ease-in` alone is almost always wrong for UI — it makes things accelerate away and feel like they're falling.

## The signature moment

**One per site.** This is the criterion made literal.

*'kin* spends roughly **20 seconds** on its opening: the project photography, pre-compressed into a hairline strip a few pixels tall, unfolding vertically until it fills the viewport. It never bounces, never stutters, and doesn't hurry. It works because the site has decided that this — and nothing else — is where the drama lives. The navigation is silent. There is no scrollbar. There are twelve words of copy.

Three conditions make a long signature moment read as confidence rather than as a bug:

1. **It is the only one.** If the page has three long animations, all three are just slow.
2. **It is interruptible.** Click, scroll, keypress, or Esc must jump to the end state immediately. A user who has seen it twice should never sit through it again.
3. **It is showing something real.** *'kin's* preloader is made of the actual work. A twenty-second abstract shape is twenty seconds of nothing.

Store a flag so returning visitors get a short version:

```js
const seen = sessionStorage.getItem('intro-seen');
playIntro({ duration: seen ? 800 : 20000 });
sessionStorage.setItem('intro-seen', '1');
```

## Loading states

**No spinner. Ever.** A spinner communicates "something is happening, we don't know what, we don't know how long." That's three failures in one 24px circle.

What the reference sites do instead:

- *In Pieces* writes **"RE-ARRANGING THE PIECES"** — the loading copy states, truthfully, what the machine is doing, in the site's own voice. Thirty triangles are literally being repositioned.
- *'kin* makes the loading state **out of the content being loaded**. The images arrive compressed; loading *is* the reveal. There is no separate loading screen to design because the wait and the payoff are the same object.
- *Minh Pham* runs a percentage counter riding the tip of a tracing arc — a genuinely lovely detail, on a loader that **stalled at 20% across two full attempts and never let the site render at all.**

That last one is the lesson worth internalizing. Take the craft, refuse the architecture.

Rules:

- **Nothing blocks past 3 seconds without a way through.** Offer a skip, or render content progressively behind it.
- Prefer **skeletons that match the real layout** over any generic indicator — the page shape appears immediately and fills in.
- If you show progress, it must be **real**. A fake progress bar that jumps to 90% and waits is a lie the user can feel.
- Loading copy is copy. Write it. `Loading…` is a placeholder someone forgot to replace.

## Reveals

Scroll-triggered entrances, done with restraint:

```js
const io = new IntersectionObserver((entries) => {
  entries.forEach((e) => {
    if (e.isIntersecting) {
      e.target.dataset.revealed = 'true';
      io.unobserve(e.target);        // reveal once; re-animating on scroll-up is nauseating
    }
  });
}, { threshold: 0.15, rootMargin: '0px 0px -10% 0px' });
```

```css
[data-reveal] {
  opacity: 0;
  transform: translateY(16px);
  transition: opacity 700ms var(--ease-out), transform 700ms var(--ease-out);
}
[data-reveal][data-revealed] { opacity: 1; transform: none; }
```

**Travel 12–24px, never more.** Elements sliding 100px into place is the signature of a template. The move should be barely perceptible — you should notice that the page feels alive, not that things are flying.

**Never animate a reveal on above-the-fold content.** It's already in view on load; hiding it to fade it in delays the content for no reason and hurts LCP.

**Unobserve after revealing.** Content that re-animates every time it scrolls back into view is actively unpleasant.

## Scroll

*'kin* and *Iventions* both run smooth-scroll libraries (Lenis-class). Worth knowing what that costs before reaching for one: it hijacks native scrolling, can break keyboard paging and find-in-page, adds a dependency, and — verified while researching both sites — **makes programmatic `scrollTo` skip IntersectionObserver reveals entirely**, so content jumped to never appears.

Use it only when the whole page is an art-directed scroll experience. For a normal marketing or product page, native scroll with `scroll-behavior: smooth` on anchors is better.

Two techniques that are worth their weight:

**Scroll-driven scale.** *'kin* scales its hero image as you scroll. In modern CSS this needs no JS at all:

```css
@supports (animation-timeline: view()) {
  .hero-media {
    animation: grow linear both;
    animation-timeline: view();
    animation-range: entry 0% cover 40%;
  }
  @keyframes grow { from { scale: 0.86; } to { scale: 1; } }
}
```

**Sticky sections** for chaptered content — far cheaper and more robust than pinned-scroll libraries.

Note: *'kin's* homepage doesn't scroll at all (`scrollHeight === innerHeight`). Full-viewport, carousel-driven. That's a legitimate choice for a portfolio with six projects, and a bad one for anything with real content depth.

## Reduced motion

Non-negotiable, including the signature moment. Someone with vestibular sensitivity should get the *information* without the movement.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
  [data-reveal] { opacity: 1 !important; transform: none !important; }
}
```

Match it in JS, because CSS can't reach a canvas or a JS-driven timeline:

```js
const reduced = window.matchMedia('(prefers-reduced-motion: reduce)');
if (reduced.matches) skipToEndState();
reduced.addEventListener('change', (e) => e.matches && skipToEndState());
```

Reduced motion means *reduced*, not *removed*: a cross-fade is usually fine where a slide is not. What must go is travel, parallax, scale, and anything continuous.

## Performance rules

- **Animate `transform` and `opacity` only.** Anything else (width, height, top, margin, box-shadow) triggers layout or paint every frame.
- Exception worth knowing: `clip-path` is GPU-composited in modern browsers and is what makes *In Pieces* possible — thirty simultaneous polygon morphs at full frame rate, with **zero SVG elements and zero `<polygon>` tags**, verified in the DOM.
- `will-change` immediately before a known animation, removed after. Leaving it on permanently costs memory and can make things slower.
- Never animate more than a few dozen elements at once without checking a real frame profile.
- Test on a mid-range phone with 4× CPU throttling, not on the machine you built it on.
