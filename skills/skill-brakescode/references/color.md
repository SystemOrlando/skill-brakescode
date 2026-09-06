# Color

**Measured** values were sampled from the live DOM. **Approximate** values were read off screenshots and are directionally right, not exact — never paste them as final tokens without sampling.

## Contents

- [The two laws](#the-two-laws)
- [Measured grounds and inks](#measured-grounds-and-inks)
- [Warm ground, cool ink](#warm-ground-cool-ink)
- [Contrast: the actual arithmetic](#contrast-the-actual-arithmetic)
- [The opacity floor](#the-opacity-floor)
- [Tone-on-tone](#tone-on-tone)
- [Accent](#accent)
- [Subject-derived palettes](#subject-derived-palettes)
- [Building the token set](#building-the-token-set)

## The two laws

**1. Never `#FFFFFF`, never `#000000`.**

Not one reference site uses either. Pure white is the color of an unstyled document; pure black is a hole in the screen that no physical ink or pigment matches. Both read as *absence of a decision*. The moment you shift white to a warm bone and black to a near-black with a hint of blue, the page starts looking like an object someone made.

**2. Warm ground, cool ink.**

The paper leans warm, the ink leans cool. This is measured, not folklore — see below. It's the same reason ink on paper looks right in the physical world, and it produces a subtle vibration between ground and text that pure neutrals don't have.

## Measured grounds and inks

| Site | Role | Value | Channel reading |
|---|---|---|---|
| 'kin | ground | `#F4F2ED` — `rgb(244,242,237)` | R>G>B, **warm** (R−B = 7) |
| 'kin | ink | `#111214` — `rgb(17,18,20)` | B>G>R, **cool** (B−R = 3) |
| Iventions | ground | `#F3EFEB` — `rgb(243,239,235)` | R>G>B, **warm** (R−B = 8) |
| In Pieces | ground | `#1A1A1D` — `rgb(26,26,29)` | B>R, **cool** (B−R = 3) |
| Minh Pham | ground | `#0D0D0D` — `rgb(13,13,13)` | neutral |
| Simply Chocolate | ground | `#EFEFEF` — `rgb(239,239,239)` | neutral |

The warm grounds cluster tightly: `#F4F2ED` and `#F3EFEB` are four points apart across three channels. That is effectively **one color**, arrived at independently by two studios. Treat it as the house paper and stop redesigning it.

## Warm ground, cool ink

Look at `#111214` closely: red 17, green 18, blue 20. The ink is **bluer than it is red** — while the paper it sits on is redder than it is blue. The two lean in opposite directions by a nearly identical amount (7 and 3 points).

*In Pieces* does the same on a dark ground: `#1A1A1D` is blue-leaning near-black.

The rule that falls out: **give the ground and the ink opposite temperature bias, 5–10 points of channel spread, no more.** Past ~12 points it stops reading as a temperature and starts reading as a tint, and the page looks like it has a color cast.

Ready to use:

```css
--paper:      #F4F2ED;   /* warm bone — the house ground */
--paper-sunk: #EAE7E0;   /* recessed panels, table stripes */
--ink:        #111214;   /* cool near-black */
--ink-soft:   #3A3B3F;   /* secondary text */
--night:      #1A1A1D;   /* dark-mode ground, cool */
--night-lift: #232327;   /* raised surfaces on night */
```

## Contrast: the actual arithmetic

The most common objection to warm, soft palettes is that they cost contrast. **They don't.** Computed WCAG 2.1 ratios for the measured pairs:

| Pair | Ratio | Verdict |
|---|---|---|
| `#111214` on `#F4F2ED` | **16.93 : 1** | Passes AAA with enormous headroom |
| `#F4F2ED` on `#1A1A1D` | **15.52 : 1** | Passes AAA |

For reference, pure `#000` on `#FFF` is 21:1. Going warm cost about four points of a ratio that only needed to clear 7:1 to pass AAA for body text. **There is no tradeoff here.** Anyone shipping `#FFF`/`#000` "for accessibility" is solving a problem that doesn't exist.

## The opacity floor

This is where warm palettes actually do get into trouble, and it's worth being precise because the failure is invisible to the person who designed it.

The micro-label pattern wants ink at reduced opacity so it recedes. Computed, for `#111214` composited on `#F4F2ED`:

| Ink opacity | Effective color | Contrast | Usable for |
|---|---|---|---|
| 100% | `#111214` | 16.93 : 1 | anything |
| 60% | ≈ `#6C6C6B` | **4.70 : 1** | **body text — this is the floor** |
| 50% | ≈ `#828280` | ≈ 3.5 : 1 | large text only (≥24px) |
| 46% | ≈ `#8D8C8A` | ≈ 3.03 : 1 | large text, at the limit |
| 40% | ≈ `#999896` | **2.58 : 1** | **decorative only — fails for text** |

So:

- **60% is the hard floor for any text a person must read.**
- 46–50% is permitted only for text at 24px+ (or 18.66px+ bold), where WCAG allows 3:1.
- **40% and below carries no information.** If a label at 40% is the only place something is stated, it is not stated.

The 11px micro-label is the exact case where this bites — it is both the smallest text and the most tempting to fade. Set it at **60% minimum**, and if it still feels too present, make it smaller or track it wider rather than fading it further.

## Tone-on-tone

*Iventions* runs an enormous `IVENTIONS` wordmark in a beige only slightly darker than its beige ground — roughly `#E0D8CE` on `#F3EFEB` *(approximate)*, somewhere near 1.3:1. It looks superb and it is completely illegible as text.

That's fine, under one condition: **it is decoration, not information.** The brand name is in the `<title>`, the nav, and the footer. The giant wordmark is texture.

The rule: tone-on-tone at sub-3:1 is allowed **only** when the same information exists elsewhere in an accessible form, and the decorative element is `aria-hidden="true"`. The instant it's the only carrier — a heading, a label, a price, a nav item — it must clear its contrast requirement.

## Accent

**One accent.** It is the loud moment from the criterion, expressed in color, and a second accent halves the first one's power.

Observed accents *(all approximate — sampled from screenshots)*:

| Site | Accent | Used for |
|---|---|---|
| Iventions | acid chartreuse ≈ `#E6FF7A` | one full section, against two screens of beige |
| In Pieces | crimson→magenta ≈ `#E01B24` → `#E1195B` | the logo only; slowly cycles |
| Simply Chocolate | burgundy ≈ `#7B1B2E`, forest ≈ `#1F5B3A` | per-product ground |

Note what *Iventions* does: the accent isn't a button color, it's an **entire section's ground**. That's the higher-leverage move. Small accents on buttons and links are how every template uses color; flooding one full viewport is how a page gets remembered.

If the accent is used on text or controls, it still has to pass contrast. Chartreuse `#E6FF7A` is a *ground* color — near-black on it reads fine; it is useless as text on white.

## Filled and outlined in the same set

A set where **every** item is a solid saturated field is heavy, and heavy in a way that flattens: with everything shouting at the same volume the set has no internal order, and the blocks start reading as software chrome rather than as objects.

Mix the two treatments. Give the ones that matter a filled field; give the rest the page's own ground with a **fine rule in that item's color**. The color still identifies each item, the set gains a hierarchy it did not have, and the page gets lighter without losing any commitment.

```css
.item        { border: 1px solid var(--tinte); background: transparent; }
.item--lleno { background: var(--tinte); color: var(--sobre); border-color: transparent; }
```

Two or three filled among five or six outlined is a good starting ratio. Which ones get filled is a content decision — the newest, the one in season, the one being recommended — and it should mean something, not alternate.

**A filled field takes its own ink.** Never assume the page's text color survives on top of it: a light field needs dark text and a dark field needs light, and which is which is decided by measuring, not by eye. Store the ink alongside the color so the pair travels together.

```ts
{ nombre: "Chilca", color: "#7E9A16", sobre: "#16130F" }  // campo claro, tinta oscura
{ nombre: "Añil",   color: "#1B4B8F", sobre: "#F2EDE4" }  // campo oscuro, tinta clara
```

Check the small text too, not just the heading. Micro-labels on a saturated field are where contrast quietly fails, and a label at reduced opacity on a mid-tone field almost always lands under 4.5:1.

## Texture belongs on the fields too

`anti-slop.md` calls a flat ground a tell. The same is true of a flat *field*: a solid block of pure color is the "elegant dark mode" default, and it is what separates a page that looks printed from one that looks rendered.

Give the fields the subject's own material at very low strength — a thread-fine line pattern for something woven, a paper tooth for something printed, a screen dot for something posted. Keep it under ~4% contrast against the field, tile a real asset rather than filtering live, and check it on both the lightest and the darkest field in the set. If you can see a pattern rather than feel a surface, it is too strong.

## Subject-derived palettes

*In Pieces* changes the entire page background per species — lavender for the hornbill, cyan for the vaquita — and cross-fades it during the triangle morph. *Simply Chocolate* gives each product its own saturated ground.

This is the strongest color idea in the whole set, because the palette stops being applied *to* the content and starts being generated *by* it. When the content has natural variety — projects, products, chapters, categories — derive a ground per item and let navigation change the world.

Two constraints, or it falls apart:

1. **Ink stays fixed.** Only the ground changes. If both move, nothing is stable and the page loses its spine.
2. **Every ground must clear contrast against that one fixed ink.** Choose grounds from a band of similar luminance — pick them all at roughly the same lightness in HSL/OKLCH and vary hue and saturation. Then the transition is a hue rotation, which is smooth, rather than a lightness jump, which flashes.

```css
/* set per item; everything else reads from these */
:root { --ground: #B39DDB; --ink: #111214; }
body { background: var(--ground); transition: background-color 1.2s cubic-bezier(0.22,1,0.36,1); }
```

## Building the token set

Semantic names, not literal ones — `--paper`, not `--beige-100`. When the palette changes, literal names become lies.

```css
:root {
  --ground:      #F4F2ED;
  --ground-sunk: #EAE7E0;
  --ink:         #111214;
  --ink-soft:    color-mix(in srgb, var(--ink) 60%, var(--ground));  /* 4.7:1 — the floor */
  --ink-mute:    color-mix(in srgb, var(--ink) 40%, var(--ground));  /* decorative only */
  --line:        color-mix(in srgb, var(--ink) 14%, var(--ground));
  --accent:      #E6FF7A;
}

:root[data-theme="dark"] {
  --ground:      #1A1A1D;
  --ground-sunk: #232327;
  --ink:         #F4F2ED;
  --line:        color-mix(in srgb, var(--ink) 18%, var(--ground));
}
```

Define the full light palette on bare `:root`, then override only what changes for dark. Never let a color's only definition live inside a media query or a `[data-theme]` block — that's how a page ends up transparent or unstyled in the state you didn't test.

**Hairline rules matter more than they look.** `--line` at 14% ink is the editorial device that makes data tables, indices and section dividers read as considered. Every reference site uses fine rules heavily; none uses heavy borders or shadows. If you're reaching for a `box-shadow` to separate two things, try a 1px rule first.
