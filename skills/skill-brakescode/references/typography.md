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

House defaults when nothing is specified:

- **Grotesque:** Inter Tight, Geist, or Söhne if licensed. Avoid stock Inter at default settings — it's the visual signature of a template.
- **Mono for labels:** Geist Mono, JetBrains Mono, Berkeley Mono.
- **Serif for voice:** Instrument Serif (display only), Fraunces (variable, has real character), Newsreader (reads well at text sizes).

Load through `next/font` — self-hosted, no layout shift, no third-party request. All reference sites self-host.

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
  font-size: 0.6875rem;            /* 11px */
  font-weight: 500;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--ink-soft);          /* 60% ink — recedes, still legible */
}
```

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

Line height, inverse to size for the same optical reason as tracking:

| Role | Line height |
|---|---|
| Display ≥ 72px | 0.95–1.05 |
| Headline 40–72px | 1.05–1.15 |
| Subhead 24–40px | 1.2 |
| Body | 1.5–1.65 |
| Micro label | 1 (it's a single line) |

Measure: **60–75 characters** for body. Iventions holds its body copy to roughly this and it's why a page that long stays readable.

One more, and it matters more than the numbers: **set display type in as few lines as the breakpoint allows, and control the breaks yourself.** Iventions ships three separate markup copies of its headline for different breakpoints rather than letting one string reflow arbitrarily. A headline that wraps where the browser decides is a headline nobody art-directed.
