# Patterns

Signature interactions observed across the reference sites, with implementations.

**This is a catalog, not a checklist.** Take one, maybe two. A page carrying eight of these has failed the loud-once test and will read as a demo reel. Each entry says when it's the wrong choice — that part matters more than the code.

## Contents

**Structural** — [Split hero](#1-split-hero) · [Receding chrome](#2-receding-chrome) · [Density toggle](#3-density-toggle) · [Editorial data table](#4-editorial-data-table)
**Type** — [Micro system label](#5-micro-system-label) · [Numbered index](#6-numbered-index) · [Word-split reveal](#7-word-split-reveal) · [Type as mask](#8-type-as-mask) · [Tone-on-tone wordmark](#9-tone-on-tone-wordmark)
**Signature** — [Compressed-strip unfold](#10-compressed-strip-unfold) · [Subject-derived ground](#11-subject-derived-ground) · [Identity equals mechanism](#12-identity-equals-mechanism) · [Torn frame edge](#13-torn-frame-edge)
**Detail** — [Dual-label swap](#14-dual-label-swap) · [Suffix-split counter](#15-suffix-split-counter)

---

## 1. Split hero

*Simply Chocolate.* The viewport divides in two: media on one side, a solid color panel carrying the message on the other. No text over photography, so nothing fights for legibility, and the brand color gets a full half-screen to assert itself.

Reach for it when you have one strong image and a single message. It's the most reliable hero in the set — hard to make ugly, and it sidesteps the perennial problem of text contrast over a photo that changes.

```css
.hero { display: grid; grid-template-columns: 1fr 1fr; min-height: 88vh; }
.hero__media { position: relative; overflow: hidden; }
.hero__media img, .hero__media video { width: 100%; height: 100%; object-fit: cover; }
.hero__panel {
  background: var(--accent-ground);
  color: var(--on-accent);
  display: grid; align-content: center; justify-items: center;
  gap: 1.25rem; padding: clamp(2rem, 5vw, 5rem); text-align: center;
}
@media (max-width: 768px) { .hero { grid-template-columns: 1fr; } }
```

**Wrong when** the image *is* the message (use fullbleed) or you have three things to say (use a section, not a hero).

---

## 2. Receding chrome

*'kin.* Navigation and labels fade out while the user is idle and return on intent — pointer movement, scroll, keypress. The work occupies the screen alone.

```js
let idle;
const show = () => {
  document.body.dataset.chrome = 'visible';
  clearTimeout(idle);
  idle = setTimeout(() => { document.body.dataset.chrome = 'hidden'; }, 2600);
};
['pointermove', 'keydown', 'scroll', 'touchstart'].forEach(
  (evt) => addEventListener(evt, show, { passive: true })
);
show();
```

```css
.chrome { transition: opacity 400ms var(--ease-out); }
[data-chrome='hidden'] .chrome { opacity: 0; }
[data-chrome='hidden'] { cursor: none; }
.chrome:focus-within { opacity: 1 !important; }   /* keyboard users must never lose it */
```

**Wrong when** the chrome contains anything the user needs continuously — a cart, a filter, a form. Portfolio and gallery only. Never hide chrome on touch devices, where there's no pointer-move to bring it back before a tap.

---

## 3. Density toggle

*'kin* ("LAYOUT 1 / 2") and *Simply Chocolate* (three grid densities) independently ship the same idea: let the visitor choose how much they see at once. Some people scan, some people study.

```jsx
const DENSITIES = [2, 3, 5];

function Grid({ items }) {
  const [cols, setCols] = useState(3);

  useEffect(() => {
    try {
      const saved = Number(localStorage.getItem('density'));
      if (DENSITIES.includes(saved)) setCols(saved);
    } catch {}
  }, []);

  const choose = (n) => {
    setCols(n);
    try { localStorage.setItem('density', String(n)); } catch {}
  };

  return (
    <>
      <div role="group" aria-label="Grid density">
        {DENSITIES.map((n) => (
          <button key={n} onClick={() => choose(n)} aria-pressed={cols === n}>
            {n} across
          </button>
        ))}
      </div>
      <ul style={{ '--cols': cols }} className="grid">{/* … */}</ul>
    </>
  );
}
```

```css
.grid { display: grid; gap: 1.5rem; grid-template-columns: repeat(var(--cols), minmax(0, 1fr)); }
@media (max-width: 900px) { .grid { grid-template-columns: repeat(2, minmax(0, 1fr)); } }
```

Wrap every `localStorage` access in `try/catch` — it throws outright in some privacy contexts, and a thrown error here takes the whole grid down.

**Wrong when** there are fewer than ~9 items. Below that the toggle changes nothing worth changing.

---

## 4. Editorial data table

*Iventions* presents project facts as a real table — `PARTICIPANTS / INDUSTRY / EVENT TYPE / LOCATION` — with micro-label headers and hairline rules. It reads as a publication rather than a marketing page, and it makes the numbers feel audited.

```css
.data { width: 100%; border-collapse: collapse; }
.data th {
  font-size: 0.6875rem; font-weight: 500; letter-spacing: 0.16em;
  text-transform: uppercase; color: var(--ink-soft);
  text-align: left; padding-bottom: 0.75rem;
}
.data td { padding: 1rem 0; border-top: 1px solid var(--line); }
.data td:last-child { text-align: right; font-variant-numeric: tabular-nums; }
```

Use a real `<table>` with real `<th>` elements. A grid of divs looks the same and tells a screen reader nothing.

`font-variant-numeric: tabular-nums` on every numeric column — proportional digits make columns wobble.

---

## 5. Micro system label

Present on all five sites. The 11px uppercase tracked label is the fastest single move for making a page look authored. Full recipe and the contrast floor are in `typography.md` and `color.md`.

Short version: 11px, weight 500, `letter-spacing: 0.16em`, uppercase, ink at **60%** (not 40% — 40% measures 2.58:1 and fails as text).

---

## 6. Numbered index

`01 / 02 / 03` on *'kin*, `PIECE 1` on *In Pieces*, `/08` counters on *Iventions*. Sequence signals curation — these were selected and ordered, not dumped.

Let CSS do it so the numbers can't drift out of sync with the content:

```css
.index { counter-reset: item; }
.index > li { counter-increment: item; }
.index > li::before {
  content: counter(item, decimal-leading-zero);   /* 01, 02, 03 … */
  font-variant-numeric: tabular-nums;
  letter-spacing: 0.16em;
  color: var(--ink-soft);
  margin-right: 1rem;
}
```

For an "N of total" counter, show both: `03 / 08` tells the user where the end is, which a bare `03` doesn't.

---

## 7. Word-split reveal

*'kin* splits its one paragraph into per-word spans and staggers them upward from a clipped baseline. Restrained and expensive-looking.

```jsx
function SplitWords({ text, revealed, delay = 0, step = 45 }) {
  return (
    <span aria-label={text}>
      {text.split(' ').map((word, i) => (
        <span className="word" key={i} aria-hidden="true">
          <span
            data-in={revealed || undefined}
            style={{ transitionDelay: `${delay + i * step}ms` }}
          >
            {word}
          </span>
        </span>
      ))}
    </span>
  );
}
```

```css
.word { display: inline-block; overflow: hidden; vertical-align: bottom; margin-right: 0.25em; }
.word > span {
  display: inline-block;
  transform: translateY(105%);
  transition: transform 700ms var(--ease-out);
}
.word > span[data-in] { transform: none; }

@media (prefers-reduced-motion: reduce) {
  .word > span { transform: none; transition: none; }
}
```

Two things people get wrong. **The `aria-label` on the parent with `aria-hidden` on the fragments is required** — otherwise assistive tech reads the text one word at a time as separate nodes. And **use `margin-right`, not a literal space**, because `overflow: hidden` on the word wrapper clips a trailing space and the sentence closes up.

**Wrong when** the text is more than about 25 words. Staggering a paragraph makes people wait to read.

---

## 8. Type as mask

*Iventions.* Event footage plays inside the letterforms of the word "remember." The claim and the evidence occupy the same pixels.

**For an image or gradient** — trivial and well supported:

```css
.masked-text {
  background: url('/hero.jpg') center / cover;
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
```

**For video**, `background-clip` doesn't apply. Use an SVG knockout: a solid panel in the ground color with the text cut out of it, laid over the playing video.

```html
<div class="knockout">
  <video src="/reel.mp4" autoplay muted loop playsinline></video>
  <svg viewBox="0 0 1200 300" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
    <defs>
      <mask id="cut">
        <rect width="100%" height="100%" fill="#fff" />
        <text x="50%" y="50%" text-anchor="middle" dominant-baseline="middle"
              font-size="180" font-weight="500" fill="#000">remember</text>
      </mask>
    </defs>
    <rect width="100%" height="100%" fill="var(--ground)" mask="url(#cut)" />
  </svg>
</div>
```

```css
.knockout { position: relative; isolation: isolate; }
.knockout video { width: 100%; display: block; }
.knockout svg { position: absolute; inset: 0; width: 100%; height: 100%; }
```

Three requirements or it breaks in production: the real text must also exist as an accessible heading (the SVG is `aria-hidden`); the webfont must be loaded before the SVG paints, so gate it on `document.fonts.ready` or ship the letterforms as outlined paths; and there must be a solid-color fallback for `prefers-reduced-motion` and for failed video loads.

**Wrong when** the footage is busy. It needs high-contrast, slow, simple motion or the word stops being readable.

---

## 9. Tone-on-tone wordmark

*Iventions* sets an enormous `IVENTIONS` in a beige barely darker than the ground (~1.3:1). Texture, not text. Adds scale and confidence without adding noise.

```css
.wordmark {
  font-size: clamp(4rem, 18vw, 16rem);
  font-weight: 500;
  letter-spacing: -0.035em;
  color: color-mix(in srgb, var(--ink) 9%, var(--ground));
  user-select: none;
}
```

Always `aria-hidden="true"`, and the brand name must appear in accessible form elsewhere on the page. Covered in `color.md` — decorative sub-3:1 is fine, informational sub-3:1 never is.

---

## 10. Compressed-strip unfold

*'kin's* signature moment. The project photography is pre-squashed into a hairline a few pixels tall, then decompresses vertically over roughly twenty seconds until it fills the screen.

There are two different effects here and it's worth knowing which you want:

- **Decompression** (what *'kin* does) — the whole image is squashed and stretches back to true proportion. Use `scaleY`.
- **Slit reveal** — a narrow window widens onto an undistorted image. Use a growing container with `object-fit: cover`.

Decompression, done on the GPU:

```css
.unfold {
  transform: scaleY(0.006);
  transform-origin: center;
  transition: transform 20s var(--ease-expo);
  will-change: transform;
}
.unfold[data-open] { transform: none; }
```

```js
requestAnimationFrame(() => el.dataset.open = 'true');
el.addEventListener('transitionend', () => el.style.willChange = '');
```

Animating `transform` rather than `height` keeps it off the layout thread — a height animation on a full-viewport element repaints every frame for twenty seconds.

The container must hold **only imagery**. `scaleY` squashes text too, and stretched type looks like a mistake rather than an effect.

Must be interruptible and must respect reduced motion — see `motion.md`. And it must be the site's only long moment.

---

## 11. Subject-derived ground

*In Pieces* recolors the entire page per species; *Simply Chocolate* gives each product its own ground. The palette is generated by the content instead of applied to it. The strongest color idea in the set — full treatment in `color.md`.

Two constraints: the ink stays fixed while only the ground moves, and all grounds sit at similar luminance so transitions are hue rotations rather than lightness flashes.

---

## 12. Identity equals mechanism

*In Pieces* builds its logo out of the same triangles that build the animals — and the loader copy, "RE-ARRANGING THE PIECES," describes the same operation. One technique produces the content, the identity, the transitions, and the voice.

No code. It's a question to ask at the start of a project: **what is the one technique here, and can it also make the logo, the icons, the transitions, the loading state, the 404?** When the answer is yes, the site becomes impossible to mistake for another one, and every subsequent decision gets easier because there's a rule to follow.

Worked examples: a data product whose logo is drawn by its own charting engine; a type foundry whose loading state is a font rendering progressively; a photo studio whose page transitions are shutter-speed exposures.

---

## 13. Torn frame edge

*In Pieces* frames the viewport with an irregular, torn-paper edge instead of a straight crop. Tiny detail, disproportionate warmth — it stops the page from feeling like a rectangle.

```css
.torn {
  filter: url(#roughen);
}
```

```html
<svg width="0" height="0" aria-hidden="true">
  <filter id="roughen">
    <feTurbulence type="fractalNoise" baseFrequency="0.02 0.06" numOctaves="3" seed="7" result="noise" />
    <feDisplacementMap in="SourceGraphic" in2="noise" scale="9" xChannelSelector="R" yChannelSelector="G" />
  </filter>
</svg>
```

Apply to the frame element, never to a container holding text — displacement will chew the letterforms. Keep `scale` under ~12; past that it stops reading as torn paper and starts reading as a rendering bug.

---

## 14. Dual-label swap

*Minh Pham's* CV. Every role carries its official title and, on hover, an honest one: Art Director ↔ Photoshop Doodler, Flash Designer ↔ Jurassic Designer, Design Lead ↔ Self-lead Designer. The whole personality of the site lives in this one interaction.

```html
<span class="swap">
  <span>Art Director</span>
  <span>Photoshop Doodler</span>
</span>
```

```css
.swap { display: inline-grid; overflow: hidden; vertical-align: bottom; }
.swap > span { grid-area: 1 / 1; transition: transform 320ms var(--ease-out); }
.swap > span:last-child { transform: translateY(100%); }
.swap:hover > span:first-child,
.swap:focus-visible > span:first-child { transform: translateY(-100%); }
.swap:hover > span:last-child,
.swap:focus-visible > span:last-child { transform: none; }
```

`inline-grid` with both children on `grid-area: 1/1` stacks them without absolute positioning, so the element sizes itself to the wider label and nothing shifts.

**Touch devices have no hover.** Either make it tappable (`tabindex="0"` plus the `:focus-visible` rules above) or accept that the joke is desktop-only — which is acceptable for a joke, and unacceptable for information.

---

## 15. Suffix-split counter

*Iventions* renders stats as separate elements for value and suffix — `270` + `+`, `1.2` + `K`, `90` + `%` — so the number animates while the unit stays fixed. Each stat carries a caption with actual wit: *"That's ideas, not coffee. Brilliant ones, brewed daily."*

```jsx
function Stat({ value, suffix, label, caption }) {
  const ref = useRef(null);
  const [shown, setShown] = useState(0);

  useEffect(() => {
    const el = ref.current;
    if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
      setShown(value);
      return;
    }
    const io = new IntersectionObserver(([e]) => {
      if (!e.isIntersecting) return;
      io.disconnect();
      const t0 = performance.now(), dur = 1400;
      const tick = (t) => {
        const p = Math.min((t - t0) / dur, 1);
        setShown(value * (1 - Math.pow(1 - p, 4)));   // ease-out quart
        if (p < 1) requestAnimationFrame(tick);
      };
      requestAnimationFrame(tick);
    }, { threshold: 0.5 });
    io.observe(el);
    return () => io.disconnect();
  }, [value]);

  return (
    <div ref={ref}>
      <p className="stat">
        <span className="stat__num">{Number.isInteger(value) ? Math.round(shown) : shown.toFixed(1)}</span>
        <span className="stat__suf">{suffix}</span>
      </p>
      <p className="label">{label}</p>
      <p className="caption">{caption}</p>
    </div>
  );
}
```

```css
.stat { display: flex; align-items: baseline; gap: 0.1em; }
.stat__num { font-size: clamp(3rem, 7vw, 7rem); letter-spacing: -0.03em; font-variant-numeric: tabular-nums; }
.stat__suf { font-size: 0.4em; color: var(--ink-soft); }
```

`tabular-nums` is essential — without it the number jitters horizontally as digits change and the whole row twitches.

**Write the caption.** A number with a generic label is a stat; a number with a line of real voice is the thing people quote. This is the cheapest personality in the entire catalog and almost everyone skips it.
