# Anti-slop

How to not ship something that reads as machine-made.

## Contents

- [The root cause](#the-root-cause)
- [Tell 0: restraint without a payload](#tell-0-restraint-without-a-payload)
- [Layout tells](#layout-tells)
- [Color and CSS tells](#color-and-css-tells)
- [Component tells](#component-tells)
- [Motion tells](#motion-tells)
- [Code tells](#code-tells)
- [Copy tells](#copy-tells)
- [The self-check](#the-self-check)

## The root cause

Every tell below has one origin: **an arrangement was reached for instead of derived.**

A three-card row appears because three-card rows exist, not because the content has three peer items. `bg-slate-900` appears because it is the first dark that comes to hand. `transition-all duration-300` appears because it is the shape a transition has. None of these are ugly in themselves — they are the visible residue of a decision nobody made.

So the fix is never "avoid this list." The fix is to derive the answer from the subject, and the list is how you *notice* you didn't. When you catch yourself on one of these, do not swap it for a different default. Go back and derive.

## Tell 0: restraint without a payload

**The one the checklists miss, and the easiest to ship while feeling disciplined.**

A page that refuses every cliché — no cards, no gradients, no stock components, correct semantics, a custom palette — and then commits to nothing. Uniform hairline rules, one type size doing all the work, a flat ground, everything on one axis, a single 600ms fade as the entire motion budget. It passes every negative check and it is *flat*.

This is what "be quiet so you can be loud" degrades into when only the first half gets built. Restraint is a **budget**, not a virtue. Spending the page on silence and then never buying anything with it is not discipline; it is an unfinished page with good manners.

Diagnostic: **name the thing you spent the quiet on.** If you cannot point at one element, one moment, or one passage that is genuinely large, dense, saturated, fast, or strange — the budget is unspent and the page is flat. A design where the boldest event is a border-fill on hover has not committed.

The fix is never to add five medium things. It is to take one thing and push it past comfort: type at a scale that feels wrong until you see it in place, a field of color that owns a whole viewport, a single element that breaks the grid it lives in, a passage of real density right against a passage of real air.

## Layout tells

**The alternating-section stack.** Hero with a big centered title → row of three icon cards → benefits with image-left/text-right → the same reversed → testimonials → footer. This is the single most recognizable machine layout in existence.

What replaces it is not "a different stack." It is composition:

- **Asymmetry.** Let the grid be uneven. A 7/5 or 8/4 split reads as decided; 6/6 reads as default. Push a block off the centerline and let the whitespace be unequal on purpose.
- **Overlap.** Elements that share grid cells and sit on top of each other — `grid-area: 1/1` with deliberate offsets — instantly read as art-directed, because no template does it.
- **Break the container once.** One element that runs past the content column into the margin, or full-bleed against everything else being contained. Once per page.
- **Vary the rhythm.** Do not give every section the same vertical padding. A dense passage earns a quiet one; identical spacing everywhere is the stack wearing different content.

```css
/* Elements sharing a cell — the cheapest way out of the stack */
.overlay { display: grid; }
.overlay > * { grid-area: 1 / 1; }
.overlay > .mark { justify-self: end; transform: translate(18%, -12%); }
```

**The three-card row.** Cards are the lazy container: they exist to stop you from deciding what the relationship between items actually is. Before reaching for cards, ask what the items really are — a sequence (number them, rule them, run them as a list), a comparison (a table), a hierarchy (one large, the rest small), or a set with no order (then why is it a row of three?).

**The boring hero.** Flat ground, centered `h1`, centered paragraph, two buttons with 8px radius, one filled and one outlined. Every part of that is a default.

What to do instead, pick one and commit: set the headline at a scale that makes you nervous; break it across lines you choose rather than lines the browser chooses; put the primary action somewhere structural (inline in a rule, at the end of a sentence, in the margin) rather than floating under the text; make the first viewport *do* the thing the product does instead of describing it. If someone left after one viewport, they should be able to describe a specific image an hour later — not a mood.

## Color and CSS tells

**Framework defaults.** `slate-900`, `indigo-600`, `zinc-50`, `gray-500`. These are the palette of "no palette." The house grounds and inks are in `color.md`; the accent comes from the subject, and it must be a color someone chose.

**Flat grounds everywhere.** A single hex on every surface reads as a wireframe that never got art direction. The house standard bans pure white and pure black, but a warm off-white is still flat if it is the only thing on screen. Give the ground something:

- A very fine noise, low opacity, from the subject's material world (paper, film, cloth). Keep it under ~4% or it becomes a texture instead of a suggestion.
- A gradient that is not a straight two-stop linear — an off-axis radial, or a large soft field weighted to one corner.
- Real material: a ruled grid on a ledger, a registration mark on a print, a fold line. Earned by the subject, never applied as decoration.

Note the tension with `craft-floor.md`, which bans `feTurbulence` grain as amateur. It is right about *visible* SVG-filter grain used as a texture effect. A near-imperceptible tiling noise as a ground treatment is a different thing. Keep it under 4%, tile a real asset rather than filtering live, and if you can see grain rather than feel depth, it is too strong.

**The soft box-shadow.** `box-shadow: 0 4px 12px rgba(0,0,0,.08)` on everything is the most common machine tell in CSS. Either declare elevation once and precisely (a hairline rule, a hard-edged offset if the world is actually that world, a real shadow with both offset and blur that matches a light source you decided on) — or do not elevate at all. A 1px border under a wide soft shadow is the ghost card.

**Border radius.** 8px on everything is a default. Pick a radius from the world — 0 for anything printed, industrial, or documentary; large and consistent for something soft; different radii for different roles only if you can say why.

## Component tells

Shipping a shadcn, TailwindUI, or Bootstrap component unmodified is shipping their design system, not yours. Libraries are a starting geometry and an accessibility baseline — that part is genuinely valuable, keep it. What must change is everything visible:

- Border weight. Default 1px is a default; 2px, 2.5px, or none at all is a decision.
- Elevation, per the shadow rule above.
- Radius, per the world.
- `:hover`, `:focus-visible`, `:active`, and `:disabled` — all four, authored. Focus especially: the browser's default ring belongs to no design system.
- Density. Library padding is tuned for a generic app, not for your page.

A committed visual world with one stock component in it reads as a costume with a name tag still on.

## Motion tells

**`transition-all duration-300`.** Three failures at once: `all` animates properties you did not intend and forces the browser to watch everything; 300ms is the shape of "a transition" rather than a duration anyone chose; and the implicit default easing is symmetrical, which nothing in the physical world is.

Replace with named properties, a duration from the two-tier table in `motion.md`, and an authored curve:

```css
/* not: transition: all 300ms ease; */
transition:
  background-color 140ms cubic-bezier(0.4, 0, 0.2, 1),
  transform 220ms cubic-bezier(0.22, 1, 0.36, 1);
```

**One fade as the whole motion budget.** A page whose entire motion vocabulary is opacity 0→1 has no motion design. `motion.md` holds the house curves and the signature-moment rule; the point here is that the signature moment must actually exist and must be *the* moment, not a slightly longer fade.

**Scattered identical entrances.** The same reveal on every section is a loop, not choreography.

## Code tells

**Obvious class names.** `.hero-container`, `.card-features-item`, `.section-wrapper-inner`. These name the position in the template rather than the thing. Name from the subject's vocabulary: `.ledger`, `.impression`, `.entry`, `.rule`. A stranger reading the class list should be able to guess what the product is.

**Comments that restate the markup.** `/* Navbar section */` above the navbar. Delete them. A comment earns its place only when it explains a non-obvious *why* — a workaround, a constraint, a decision that looks wrong and isn't.

**Div soup.** Nested wrappers added to solve a layout problem one level at a time. Each unnecessary `<div>` is a small confession that the parent's layout was not thought through. Use real semantics — `<header>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<ol>` when the order matters — and solve layout on the parent with grid or flex rather than by adding a level. If an element exists only to carry a class, the class usually belongs on its parent or child.

## Copy tells

"Revoluciona tu flujo de trabajo con nuestra solución innovadora." Corporate filler is instantly legible as machine-written because it asserts value instead of demonstrating it, and because it would fit any company in any industry.

The test: **could this sentence appear on a competitor's site unchanged?** If yes, it says nothing.

Write specifics — real names, real places, real quantities, real constraints. Say what the thing *is*, not how good it is. `impeccable`'s truth rule applies: in greenfield work, author illustrative content at full fidelity and label it synthetic; never invent commercial claims, prices, customers, testimonials, or benchmarks.

And per the house standard: the voice lives in the microcopy, not the hero. Write the headline plainly and put the personality in the small print, where it reads as a gift rather than as marketing.

## The self-check

Before shipping, answer these out loud. They are ordered so the most common failure comes first.

1. **What did I spend the quiet on?** Name the one loud thing. If you cannot, the page is flat — go back and buy something with the budget.
2. **Could someone guess my aesthetic from the category alone?** A restaurant that came out warm-cream-and-serif, a tech product that came out dark-with-one-neon, a bookshop that came out cream-and-hand-lettering. If yes, the subject picked the design instead of you.
3. **Which decisions did I derive, and which did I reach for?** Walk the palette, the type, the layout, the radius, the shadow, the easing. Any you cannot trace back to the subject is a default in disguise.
4. **Is there a composition, or only a stack?** Find the asymmetry, the overlap, or the break. If there is none of the three, it is a stack.
5. **Does the first viewport show the mechanism or describe it?**
6. **Would this copy survive on a competitor's site?**
7. **Are all four interaction states authored?** Hover, focus-visible, active, disabled.
8. **Is the spacing hierarchical?** Measure the largest gap and the smallest. Under ~10:1 and the page is uniformly spaced, which reads flat however correct the numbers are.
9. **Does each section have one thing that wins?** If three elements compete on the same screen, the reader is given no order to read in.
10. **Did I theme what the browser draws?** Selection, caret, focus ring, scrollbar, tabular numerals. Skipping these is the most common tell of all, because nothing looks broken when you do.
11. **Did the scaffold pick my typeface?** Geist, Inter-as-display, or the system stack means the answer is yes.
