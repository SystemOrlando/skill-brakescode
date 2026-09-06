# Space and depth

Two of the fastest tells that a page was generated rather than composed: spacing that is uniform everywhere, and elevation borrowed from a framework default.

## Contents

- [White space is hierarchical](#white-space-is-hierarchical)
- [The proximity law](#the-proximity-law)
- [The scale](#the-scale)
- [Rhythm: dense earns quiet](#rhythm-dense-earns-quiet)
- [Borders and shadows are tinted](#borders-and-shadows-are-tinted)
- [Dark surfaces](#dark-surfaces)
- [Light surfaces](#light-surfaces)
- [Declare elevation once](#declare-elevation-once)

## The zoom trap

**The failure this catches:** the page is bold, committed, non-generic — and it feels like a screen held against your face. Nothing is wrong with any single element, yet the whole thing reads as *enlarged* rather than as *designed*.

It happens when "make it bold" is applied to everything at once: the display goes to 7rem, and the body follows to 19px, and the cards grow to fill their columns, and the padding grows with them. Every element got bigger and every relationship stayed identical, so no hierarchy was created. Zoom is not scale.

**Hierarchy is the ratio, not the size.** A 112px headline over 15px body is a 7.5:1 step and reads as authored. The same headline over 19px body is 5.9:1 and reads as a page someone zoomed. So when the display grows, everything else **holds still or shrinks** — that is what pays for it.

Two consequences worth stating as rules:

**Reading text does not scale with ambition.** Body copy has a correct absolute range — **15–17px** — set by how eyes work, not by how bold the page is. Pushing it to 18–20px because the design is confident is the tell. The one legitimate exception is a single short lead paragraph immediately under a hero, and even there 18px is the ceiling.

**Reading text and annotation are two different registers, and collapsing them is what makes a page feel gigantic.** Body is what someone sits down and reads. Annotation is everything that explains, qualifies, captions or footnotes — and it belongs at **12–13px in a receded color**, not at body scale. Setting an explanatory aside at 16px in full ink gives it the same weight as the thing it explains, which flattens the page and eats the air.

| Register | Size | Color |
|---|---|---|
| Reading body | 15–17px | full ink |
| Annotation, caption, footnote, aside | 12–13px | 55–65% ink |
| Micro-label | 10–11px caps, tracked | 60% ink |

**Shrinking text is how you create negative space.** This is the counter-intuitive move and the one that fixes a page that feels zoomed: the ground did not change, but with the type smaller there is visibly more of it, and the page starts breathing. Reach for it before adding padding — it is free, and it fixes the cause rather than the symptom.

**Containers do not scale with their contents' importance.** A card holding forty words does not need a 24rem column and 24px of padding because the page's display type is 112px. Size the container to the content, then let the page's scale come from the one element that earns it.

## Negative space is the luxury signal

The fastest single move from "software interface" to "gallery" is to **make the objects smaller and the ground larger.**

A grid of big filled blocks that reach the container edges reads as an app, whatever the palette. The same content at roughly 70% of that size, with ground visible around and between each object, reads as a collection someone curated. Nothing about the content changed — only how much of the page it was allowed to claim.

**The squint test:** cover the type and look at the ratio of ink to ground. If ink dominates, it reads as an interface no matter how good the typography is. Premium work is mostly empty, and the emptiness is the point: it is what tells the reader that each object was chosen rather than accumulated.

This is the discipline that makes the house tilt work rather than shout. Saturated fields and heavy display earn their force from the quiet around them; filling the viewport with them spends the contrast that made them strong.

## White space is hierarchical

**The tell:** `p-4` on every card, `p-6` on every section, `gap-4` everywhere. Mathematically consistent, visually dead. A page spaced this way has no structure — every relationship reads as equally close, so the reader gets no help deciding what belongs to what.

Uniform spacing feels safe because nothing looks *wrong*. That is exactly the problem: nothing looks like anything either.

## The proximity law

**The gap between two things is inversely proportional to how related they are.**

A heading and its own paragraph are the most related pair on the page — they get the smallest gap. Two major sections are the least related — they get the largest. Everything else falls between.

This is the whole rule, and applying it honestly produces a spacing range of roughly **20:1** between the largest and smallest gaps on a page. If your largest gap is only three or four times your smallest, the page is flat regardless of what the numbers are.

And the asymmetry that follows from it: **more space above a heading than below it.** A heading belongs to what comes after, not to what came before. Equal margins orphan it between two blocks and the eye cannot tell which it introduces.

```css
h2 { margin-block: 4.5rem 1rem; }   /* 72px above, 16px below */
```

## The scale

Prescribed. Start here, then adjust by eye — a dense data page compresses these, an editorial page opens them.

| Relationship | Gap | Tailwind |
|---|---|---|
| Inside a tight group (label to value, icon to text) | 4–8px | `gap-1` / `gap-2` |
| Heading to its own paragraph | 8–16px | `mb-2` / `mb-4` |
| Between paragraphs in one block | 16–24px | `space-y-4` / `space-y-6` |
| Between blocks inside a section | 32–56px | `mb-8` … `mb-14` |
| Above a heading (its own space) | 56–96px | `mt-14` … `mt-24` |
| **Between major sections** | **96–192px** | **`py-24` … `py-48`** |

The section number is the one most often left far too small. A landing page whose sections are separated by `py-12` reads as a list of blocks; the same page at `py-32` reads as chapters. Fear of "too much space" is the single most reliable way to make a page look cheap.

**On a project with a rhythm token** (a baseline grid, a ledger rule, a musical scale), every value above becomes a multiple of that token instead of a free number. The hierarchy stays; the units change.

## Editorial padding inside a color field

Space *inside* a filled block is not the same problem as space between blocks, and it is the one most often left at a framework default.

Text sitting close to the edges of a color field reads as a `div` that happens to have a background. The same text with generous interior space reads as a printed plate — a poster, a label, a card someone had made. Nothing changes but the padding.

**Give a color field 40–56px of vertical padding**, and make it noticeably more than the horizontal. A field padded `24px` all round is a UI component; the same field at `48px` top and bottom with `28px` sides is an object. The asymmetry matters: equal padding on all four sides is the default nobody chose, and vertical breathing room is what the eye reads as care.

```css
.field { padding: 3rem 1.75rem; }   /* 48 / 28 — not p-6 */
```

This costs height, which is exactly the trade. If the set gets too tall, the answer is fewer or smaller items, never tighter padding — because the padding is what makes them read as objects at all.

## Stagger with a real offset

Offsetting a column by 8 or 12px is not a stagger, it is a rounding error, and it reads as a misalignment bug rather than as rhythm. If you are going to break the row, break it: **48–80px** so the eye reads two deliberate registers rather than one row that failed to line up.

```css
/* La segunda columna baja de verdad. */
.set > *:nth-child(2n) { margin-block-start: 4rem; }
```

Offset by *column*, not by index, so the pattern holds when the grid reflows. And check the single-column breakpoint: a stagger that becomes a random gap on mobile is worse than none.

**Gaps are not square.** A grid with equal `gap-x` and `gap-y` is the framework default. Vertical separation needs to be **larger** than horizontal — roughly 1.5–2× — because items in the same row already read as a group while items in different rows need visible air to stop reading as a wall. `gap-x-6 gap-y-12` is a decision; `gap-6` is not.

## Controlled misalignment

Two blocks flanking a centre object, each perfectly aligned to the same top edge, produce a sandwich: symmetric, predictable, and it encases the thing in the middle instead of composing around it. The blocks are correct individually and the arrangement is a default.

**Offset them vertically on purpose.** Let the right block start where the left block's second paragraph does. Let a data list sit lower than the headline it belongs to. The eye reads two related things at different heights as *placed*, and reads them at the same height as *laid out by a function*.

This is small and it is the difference between competent and considered: **40–90px of deliberate vertical mismatch** between two flanking blocks, enough to be visible and not so much that the relationship breaks. It costs nothing and no auto-layout produces it.

The same instinct applies to alignment edges. Two columns both flush to their outer edges make a frame; letting one go flush and the other hang inside breaks the frame and gives the composition a direction.

## The intentional void

Five items in a three-column grid produce a last row of two, and the machine's answer is to center them or stretch them to fill. Both are the algorithm showing.

**Leave the cell empty on purpose.** Put the fifth item under the first, let the final column end in ground, and the composition suddenly reads as laid out by someone rather than distributed by a function. A deliberate hole in a grid is one of the most reliable signals of human authorship, precisely because no auto-layout produces it and no engineer feels comfortable shipping it.

```css
/* La quinta pieza baja bajo la primera; la última columna queda en vacío. */
.set > *:nth-child(5) { grid-column: 1; }
```

It has to look intentional rather than broken, which means: keep the empty cell at an **edge or corner**, never in the middle of the set; leave exactly one; and make sure the items that remain still align to real columns. A hole in the middle reads as a loading failure. A hole in the corner reads as air.

The same instinct applies wherever content nearly fills a container: a page that ends its last row flush is a page that was packed. Letting it end short is what makes the grid feel like a canvas.

## Rhythm: dense earns quiet

Consistent spacing is a floor, not a goal. Once the hierarchy is right, **vary section padding deliberately** so the page has pace.

A passage of real density — a table, a specification, a tight list — earns a passage of real air after it. A page where every section breathes identically has correct spacing and no rhythm, which reads as competent and forgettable.

Practical: pick two or three section rhythms and alternate them with intent. Never let it become a mechanical A-B-A-B; that is uniformity wearing a costume.

## Borders and shadows are tinted

**The tell:** `border-white/10` and `border-gray-700` on dark; `box-shadow: 0 4px 12px rgba(0,0,0,0.1)` on light. Both are the framework's answer, not yours, and both read as gray plastic laid over whatever palette you chose.

The principle: **a border or a shadow is not a separate color. It is the surface it sits on, moved.** Derive it, never pick it.

## Dark surfaces

Do not reach for gray. Build the border out of the **text color at very low opacity**, so it inherits the palette's temperature:

```css
--line: rgb(from var(--ink) r g b / 0.08);          /* ink is the light text here */
--line-strong: rgb(from var(--ink) r g b / 0.16);
```

Or, better on a branded surface, mix a trace of the accent in so edges carry the identity:

```css
--line: color-mix(in srgb, var(--accent) 22%, transparent);
```

Range: **0.05–0.10** for a quiet divider, **0.14–0.20** for a border that must be seen. Above 0.25 it stops reading as an edge and starts reading as a line someone drew.

On dark surfaces, prefer a lighter background step over a shadow. Shadows are nearly invisible against dark ground; elevation there comes from the surface getting *lighter*, which is how light actually behaves.

## Light surfaces

Pure black shadows are the giveaway. Real shadows carry the color of the light and the surface around them — on a warm paper ground, the shadow is a warm brown-gray; on a cool blue-gray ground, a cool one.

Tint the shadow toward the ground's hue and keep it low:

```css
/* Ground is warm bone #F4F2ED, so the shadow is warm, never neutral black. */
--shadow-tint: 28 26% 14%;   /* hsl: the ground's hue, deep and desaturated */

--elev-1:
  0 1px 2px hsl(var(--shadow-tint) / 0.06),
  0 3px 8px hsl(var(--shadow-tint) / 0.05);

--elev-2:
  0 2px 4px hsl(var(--shadow-tint) / 0.07),
  0 8px 24px hsl(var(--shadow-tint) / 0.06);
```

Three things make a shadow read as real rather than as a CSS default:

1. **Two or three layers**, with blur increasing and opacity decreasing. A single-layer shadow is a smudge; stacked layers are how light falls off.
2. **A vertical offset.** A zero-offset shadow is a halo, not a shadow — it implies light from directly in front, which no room has.
3. **Low opacity.** 0.05–0.08 per layer. The `rgba(0,0,0,0.1)` default is both too dark and too flat once you compare them.

Pick a light direction once — almost always from above — and let every shadow on the page obey it.

## When the hard shadow is earned

`craft-floor.md` treats `box-shadow: 4px 4px 0` as a costume, and it is right about the general case: a zero-blur block shadow dropped onto a soft world is neobrutalist cosplay.

It stops being a costume when **the world is already made of hard edges** — a pixel or thread grid, print registration, cut paper, stencil, screen-printed stock. There, a blurred shadow is the foreign object: nothing in that world has a soft penumbra, so a soft shadow contradicts the material exactly the way a hollow outline contradicts a dyed field.

The test is not "is this neobrutalist" but **"does anything else on this page have a soft edge?"** If the answer is no, the hard shadow is the consistent choice and the soft one is the lapse.

```css
/* Mundo de cuadrícula y canto vivo: la sombra también tiene canto. */
.plate { box-shadow: 4px 4px 0 0 var(--sombra); }
```

Keep the offset small (3–5px), use a color derived from the ground rather than black, and apply it consistently to every raised object in the set. One hard-shadowed element among soft ones is worse than either choice made throughout.

## Declare elevation once

A 1px border *under* a soft shadow is the ghost card: two elevation systems arguing, and the result reads as neither raised nor flat.

Choose one per surface:

- **A hairline rule** — the quietest, and the right default for editorial and documentary worlds.
- **A shadow** — for things that genuinely float above the page: menus, popovers, drag states.
- **A background step** — a surface a shade different from its parent. The most robust, and the only one that works equally in light and dark.

Related, from `anti-slop.md`: a flat ground is its own tell. The answer is texture or material from the subject's world, not a shadow scattered around to fake depth.
