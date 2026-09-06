# Typography

Everything marked **measured** was read out of the live DOM with `getComputedStyle`. Everything marked **prescribed** is a house rule derived from that evidence. Keep the distinction — it's what lets you break a rule knowingly.

## Contents

- [The tracking law](#the-tracking-law)
- [Measured evidence](#measured-evidence)
- [The house ladder](#the-house-ladder)
- [When to leave tracking alone](#when-to-leave-tracking-alone)
- [Choosing faces](#choosing-faces)
- [Weight discipline](#weight-discipline)
- [The micro-label](#the-micro-label)
- [Scale and rhythm](#scale-and-rhythm)

## The tracking law

**Tracking is inversely proportional to size.** Large type tightens; small type opens.

This is optical, not stylistic. At display sizes the counters and sidebearings drawn into the face are already generous relative to the eye's reading distance, so default spacing reads as loose and the word falls apart into letters. At micro sizes the same spacing collapses — strokes crowd, and uppercase in particular becomes a smear. So you subtract at the top of the scale and add at the bottom.

Two of the three reference sites that set tracking at all follow this law precisely, in completely different registers — one lowercase grotesque, one all-caps condensed. That convergence is why it's a law here and not a preference.

## Measured evidence

**Iventions** — Söhne, mixed case except where noted:

| Size | Tracking | Ratio |
|---|---|---|
| 106.67px | −3.2px | **−0.030em** |
| 53.33px | −1.6px | **−0.030em** |
| 32px | −0.64px | −0.020em |
| 16px | −0.16px | −0.010em |
| 12px | −0.12px | −0.010em |
| 9.33px `uppercase` | +0.187px | **+0.020em** |
| 8px `uppercase` | +0.16px | **+0.020em** |

Same site, ABC Arizona Mix (the serif) — consistently tighter than the grotesque at equivalent sizes:

| Size | Tracking | Ratio |
|---|---|---|
| 24px | −0.96px | −0.040em |
| 16px | −0.96px | −0.060em |
| 14.67px | −0.587px | −0.040em |

**In Pieces** — BlocExtCond, weight 300, uppercase throughout. All positive, because all-caps has no descender rhythm to carry it and needs air at every size — but the *gradient* is identical:

| Size | Tracking | Ratio |
|---|---|---|
| 147.2px | 4.416px | **+0.030em** |
| 45.68px | 2.284px | +0.050em |
| 22.94px | 1.995px | +0.087em |
| 13.23px | 1.323px | +0.100em |
| 11.58px | 2.315px | **+0.200em** |
| 11.03px | 2.205px | **+0.200em** |

Note the two tiers at the bottom: ~+0.10em for small running text, ~+0.20em for the system-voice labels. The site also runs display labels at +0.20em deliberately (37.9px at 7.58px) — wide tracking is part of its house voice, applied on purpose rather than by scale.

## The house ladder

**Prescribed.** Start here and adjust by eye — the face you pick will shift these by a hair.

| Role | Size | Tracking |
|---|---|---|
| Display | ≥ 72px | −0.03em to −0.04em |
| Headline | 40–72px | −0.025em to −0.03em |
| Subhead | 24–40px | −0.02em |
| Lead | 18–24px | −0.01em to −0.015em |
| Body | 14–17px | −0.005em to 0 |
| Small | 12–14px | 0 to +0.01em |
| Micro label (caps) | ≤ 11px | **+0.02em minimum** |

Two adjustments on top of the ladder:

- **Serif or mix faces: subtract another 0.02em.** Evidenced above — Arizona ran at −0.04em where Söhne ran at −0.02em.
- **All-caps: add 0.02–0.04em at any size.** Caps have no ascender/descender variation to separate the word shape, so they need the air.

As Tailwind tokens:

```js
letterSpacing: {
  display: '-0.035em',
  headline: '-0.028em',
  subhead: '-0.02em',
  lead: '-0.012em',
  body: '-0.005em',
  small: '0.005em',
  micro: '0.02em',
  system: '0.16em',   // the wide system-voice label
}
```

## When to leave tracking alone

**'kin sets no custom tracking at all** — every measured element came back `letter-spacing: normal`, from the 44px display down to the 8px mono label. Measured, and worth understanding rather than dismissing.

It works there for two reasons: Apercu is drawn with tight default metrics that already sit near where the ladder would put them, and the site carries almost no text — a dozen words on the homepage. With that little type, optical correction has nothing to correct.

So: **the ladder is for text-bearing pages.** If the page is six words and a photograph, and the face's defaults are good, leave it. Don't apply the ladder as ritual.

## Choosing faces

**Two families maximum. One is a real option.**

*In Pieces* runs the entire site on one family in one weight (300) and gets its whole hierarchy from size and tracking. That's the ceiling of restraint and it's worth aiming at, because a single-family page is nearly impossible to make look cheap.

The pairings actually in evidence:

- **'kin** — Apercu Pro + Apercu Mono Pro. *Same superfamily, different register.* The mono does labels and metadata only. Safest possible pairing: it can't clash, because it's the same drawing.
- **Iventions** — Söhne + ABC Arizona Mix. *Neo-grotesque + characterful serif.* The grotesque carries structure, the serif carries voice. Classic and hard to get wrong.
- **Simply Chocolate** — a proprietary family (Simply Chocolate, Condensed, and one literally named *Ingredients*). Commissioning type is the strongest brand move available and the least available; note it as the ceiling.

### Never these

These are not bad typefaces. They are the faces that arrive when nobody chose one, and shipping them is indistinguishable from not having made the decision.

**Hard no, no brief earns them back:**

- **Geist and Geist Mono.** The `create-next-app` default. If a page ships in Geist, the honest reading is that the scaffold picked the type.
- **Inter** at any width or weight, as a display face. As UI text in a dense app it is defensible; as the voice of a page it is the signature of a template.
- **The system stack** (`ui-sans-serif`, `-apple-system`, Arial, Helvetica, Segoe UI) as a display face. It is a fallback, and the closest installed font is a failure, not a shortcut.

**Strong no, saturated to the point of being a category tell** — naming one needs a reason no other face could satisfy, and "the subject is bookish / technical / editorial" is never that reason: Space Grotesk, Space Mono, DM Sans, DM Serif, Plus Jakarta Sans, Outfit, Poppins, Montserrat, Playfair Display, Cormorant, Lora, Crimson, Fraunces, Instrument Sans, IBM Plex.

### Choosing instead

Pick the face the way you would pick an object from the subject's world, not from a list of good fonts.

Ask what this thing would have been printed on before the web, and who set it. A market ledger was set in a workhorse grotesque by a jobbing printer. A lotería card was cut in heavy condensed wood type. A pharmacy label, a football programme, a legal notice, a seed catalogue — each has a real typographic tradition with a real register, and every one of them is more specific than "a clean sans."

Then choose for **character at the size you will actually use it.** A face with personality at 96px often falls apart at 15px, and vice versa; that is the honest argument for two faces rather than one.

Practical starting points that are not on the lists above — treat as directions, not defaults, and always check the subject first: Archivo and Archivo Narrow (workhorse grotesque with real width range), Anton and Oswald (condensed display with weight), Bricolage Grotesque (variable, idiosyncratic), Instrument Serif (display only, high contrast), Petrona and Faustina (variable serifs that read at text sizes), Libre Franklin, Public Sans, Redaction, Gambetta, Martian Mono, Courier Prime.

If the project can license commercial type, that is where the real distinction lives — the reference sites run Apercu, Söhne and ABC Arizona Mix, and one commissioned its own family outright. Say so when it is worth the money.

Load through `next/font` — self-hosted, no layout shift, no third-party request. All reference sites self-host. Load only the weights you actually use; six weights shipped for three used is payload nobody asked for.

## Weight discipline

**Three weights maximum, and you rarely need three.**

Measured usage: 'kin ships Apercu at 400/500/700 but does its actual display work at 500. Iventions ships Söhne at 300/400/500/600 and does nearly everything at 500. *In Pieces* uses exactly one weight.

The pattern: **the reference sites set display type at medium (500), not bold (700).** Large type is already emphatic — size is the emphasis. Adding weight on top makes it shout, and shouting reads as insecurity. Reserve 600–700 for small text that must cut through, which is the only place it's genuinely needed.

## The micro-label

The sub-11px uppercase label is the system's voice — section markers, metadata, numbering, categories. It appears on every reference site and it's the single fastest way to make a page read as designed rather than assembled.

The recipe:

```css
.label {
  font-family: var(--font-mono);   /* or the grotesque */
  font-size: 0.625rem;             /* 10px — smaller than feels safe */
  font-weight: 500;
  letter-spacing: 0.2em;           /* and wider than feels safe */
  text-transform: uppercase;
  line-height: 1;
  color: var(--ink-soft);          /* 60% ink — recedes, still legible */
}
```

**Go smaller and wider than instinct says.** 10px at 0.2em tracking reads as a considered technical annotation; 13px at default tracking reads as text someone forgot to style. This is the one place on a page where making type *less* comfortable makes it *more* designed — the label is not there to be read at a glance, it is there to be found when the reader looks.

### The label and its value are two different voices

A micro-label sitting directly above the text it introduces is a pair, and the pair fails when both halves look the same. Two lines at the same size and weight read as one lumpy paragraph, and the label stops doing its job — which is to be scanned past on the way to the value.

Separate them on **three axes at once**, not one:

| | Label | Value |
|---|---|---|
| Size | 10–11px | 13–15px |
| Case | uppercase | sentence case |
| Tracking | 0.16–0.24em | normal to −0.005em |
| Weight | 500–600 | 400 |
| Opacity | full | 0.75–0.85 |

**On a saturated field, drop the opacity axis entirely.** Reducing opacity always pushes the ink toward the field it sits on, so it costs contrast in both directions — light ink on a dark field and dark ink on a light one. Measured on five dyed fields: descriptions at 0.82 opacity landed at 3.3–4.0:1 and at 0.94 they still read 4.4:1, under the floor. On color, the separation has to come from size, case and tracking alone, and those three are enough.

Counter-intuitively the **label** carries the tracking and weight while the **value** goes lighter and slightly transparent — on a neutral ground, where opacity is affordable. The label is a system voice — rigid, technical, always the same shape. The value is content, and content reads best relaxed. Reverse it and the pair looks like a heading with fine print, which is a different relationship.

The range worth working in is **10–11px at 0.16–0.24em**. Below 10px it stops being legible at all; above 0.24em the words fall apart into letters. Push toward the small-and-wide end when the label is pure metadata (a source, a date, a count) and toward the larger end when it names a section the reader navigates by.

Use it for: `FEATURED WORKS`, `01 / 04`, `SPORTS · BUDAPEST`, `PARTICIPANTS`, `SCROLL`.

**Do not fade it below 60% ink.** The temptation is strong — it's the smallest text on the page and the easiest to quiet — but 40% ink measures **2.58:1** against the house ground and fails WCAG for text outright. 60% measures 4.70:1 and clears it. If the label still feels too loud at 60%, make it smaller or track it wider; do not reach for opacity. The arithmetic is in `color.md`.

At 11px it is deliberately quiet, which also makes it the wrong element for instructions, errors, or anything a user must read to proceed.

## Scale and rhythm

**Prescribed** — not measured off the reference sites, which use bespoke per-section sizing.

Use a ~1.25 ratio in the text range and let display sizes break the scale deliberately:

```
12 · 14 · 16 · 20 · 24 · 32 · 40 · 56 · 80 · 120 · 160
```

Fluid display type, clamped so it can't collapse or run away:

```css
font-size: clamp(2.5rem, 1.5rem + 5vw, 10rem);
```

### Line height is inverse to size — and it is not optional

The browser's default is roughly 1.2 at every size, which is wrong at both ends of the scale and most visibly wrong on display type. A 96px headline at default leading has ~19px of space between lines that reads as a gap; the lines stop being one object and the headline breaks apart. The same default at body size is too tight to read comfortably for more than a paragraph.

The reason is the same as for tracking: at display sizes the eye takes in the whole shape at once and wants the lines locked together; at reading sizes it tracks line by line and needs room to find the next one.

| Role | Line height | Tailwind |
|---|---|---|
| Display ≥ 72px | **0.88–1.0** | `leading-none` and below |
| Headline 40–72px | 1.02–1.12 | `leading-none` / `leading-tight` |
| Subhead 24–40px | 1.15–1.25 | `leading-tight` / `leading-snug` |
| Lead 18–24px | 1.4 | `leading-normal` |
| Body 14–17px | **1.5–1.65** | `leading-relaxed` |
| Small ≤ 13px | 1.45–1.55 | `leading-normal` |
| Micro label | 1 | `leading-none` |

Below 1.0 is legitimate on all-caps display, where there are no descenders to collide. On mixed-case display, 1.0 is usually the floor before ascenders and descenders start touching — check the actual worst pair in your real copy, not a placeholder.

Body under 1.5 is the more common failure and the more damaging one, because it makes long text tiring in a way readers feel without being able to name.

Measure: **60–75 characters** for body. Iventions holds its body copy to roughly this and it's why a page that long stays readable.

One more, and it matters more than the numbers: **set display type in as few lines as the breakpoint allows, and control the breaks yourself.** Iventions ships three separate markup copies of its headline for different breakpoints rather than letting one string reflow arbitrarily. A headline that wraps where the browser decides is a headline nobody art-directed.
