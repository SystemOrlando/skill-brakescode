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

## Declare elevation once

A 1px border *under* a soft shadow is the ghost card: two elevation systems arguing, and the result reads as neither raised nor flat.

Choose one per surface:

- **A hairline rule** — the quietest, and the right default for editorial and documentary worlds.
- **A shadow** — for things that genuinely float above the page: menus, popovers, drag states.
- **A background step** — a surface a shade different from its parent. The most robust, and the only one that works equally in light and dark.

Related, from `anti-slop.md`: a flat ground is its own tell. The answer is texture or material from the subject's world, not a shadow scattered around to fake depth.
