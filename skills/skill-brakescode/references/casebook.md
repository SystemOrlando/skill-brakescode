# Casebook

The primary record. Five sites, examined live in-browser on 2026-09-05.

Three levels of confidence, kept separate on purpose:

- **Measured** — read from the live DOM via `getComputedStyle` / DOM inspection. Trust as fact.
- **Observed** — watched happening, timed by wall clock. Directionally accurate; timings ±20%.
- **Approximate** — eyeballed from screenshots. Never paste as a final token.

---

## 1. 'kin — by-kin.com

Commercial interiors, branding and graphic design studio.

**Measured**

| | |
|---|---|
| Framework | Next.js (`_next/image`, `next/font` hashes `__apercupro_24e68c`, `__apercumonopro_3be811`) |
| Typefaces | Apercu Pro (400 / 500 / 700), Apercu Mono Pro (400 / 500) |
| Ground | `rgb(244, 242, 237)` — `#F4F2ED` |
| Ink | `rgb(17, 18, 20)` — `#111214` |
| Tracking | `normal` on **every** element sampled, 44px down to 8px |
| Type sizes | 44 / 32 / 24 / 17.33 / 14 / 10.67px Apercu Pro; 8px Apercu Mono uppercase |
| Document height | `scrollHeight === innerHeight === 720` — **the homepage does not scroll** |
| Carousel | Swiper (`swiper-icons` font loaded) |
| Body classes | `__variable_24e68c __variable_3be811 is-ready` |

**Observed**

The opening runs about **20–27 seconds**. Sequence: a hairline rule with the word "Loading" → the rule fills with horizontally compressed image data → the strip decompresses vertically in one continuous, non-bouncing, decelerating move → fullbleed photography. Wall-clock samples: ~4s hairline with image data, ~12s at roughly 90px tall, ~22s at roughly 230px, ~27s near complete.

The loading state is built from the project photography itself. There is no separate loading screen.

Scroll gestures drive image scale and carousel advance rather than page scroll. UI chrome recedes when idle and returns on intent. A `LAYOUT 1 / 2` control lets the visitor switch grid density.

Full body copy on the homepage: *"'kin are a creative commercial interiors, branding and graphic design studio."* Rendered as one span per word — the markup for a staggered reveal. Section labels: `FEATURED`, `WORKS`, `01`, `02`, `03`.

**What to take**

The loading state made of the content. The nerve to spend twenty seconds on one moment and nothing anywhere else. Twelve words of copy total.

**What not to take**

The non-scrolling homepage — viable for six projects, wrong for anything with content depth. And note the tracking finding: 'kin gets away with default tracking because Apercu's native metrics are tight and there's almost no text. That's a licence earned by restraint, not a general rule. See `typography.md`.

---

## 2. In Pieces — species-in-pieces.com

*30 species, 30 pieces.* A CSS-based interactive exhibition on evolutionary distinction, by Bryan James.

**Measured**

| | |
|---|---|
| Typeface | BlocExtCond — **weight 300 only, entire site** |
| Ground | `rgb(26, 26, 29)` — `#1A1A1D` (cool near-black) |
| `<svg>` elements | **0** |
| `<polygon>` elements | **0** |

The animals are built from **30 DOM elements per species, shaped with CSS `clip-path`** — no SVG anywhere. Verified directly.

Tracking, all uppercase, showing the inverse-size law within a single typeface:

| Size | Tracking | em |
|---|---|---|
| 147.2px | 4.416px | +0.030 |
| 45.68px | 2.284px | +0.050 |
| 22.94px | 1.995px | +0.087 |
| 13.23px | 1.323px | +0.100 |
| 11.58px | 2.315px | +0.200 |
| 11.03px | 2.205px | +0.200 |

**Observed**

Loading copy reads **"RE-ARRANGING THE PIECES"**, then **"30 UNIQUE SPECIES FACE A FRAGMENTED SURVIVAL."** — never "Loading."

The title screen logo is built from the same triangles as the animals, and cycles slowly through crimson→magenta.

Transition between species: the 30 triangles fly apart and reassemble into the next animal over roughly 1–3 seconds, while the page background cross-fades to that species' color. Captured mid-flight — the pieces are genuinely in transit, not cross-faded.

Each species has its own ground *(approximate: hornbill lavender ≈ `#B39DDB`, vaquita cyan ≈ `#5BC8D8`)*. The viewport is framed by an irregular torn-paper edge. Controls are circular icon buttons — grid, shuffle, sound — with prev/next and a "WHAT'S THE THREAT?" disc on the right. Items are labelled `PIECE 1`, `PIECE 2`.

**What to take**

The purest example of the criterion in the set. One constraint — thirty triangles, CSS only — generates the artwork, the logo, the palette, the transitions, and the loader copy. Also: an entire site's hierarchy from one family in one weight, using nothing but size and tracking.

---

## 3. Iventions — iventions.com

International event agency.

**Measured**

| | |
|---|---|
| Typefaces | Söhne (300 / 400 / 500 / 600), ABC Arizona Mix (300 / 400) |
| Ground | `rgb(243, 239, 235)` — `#F3EFEB` |
| Document height | 13,601px |

Söhne tracking — the clearest evidence of the inverse-size law:

| Size | Tracking | em |
|---|---|---|
| 106.67px | −3.2px | −0.030 |
| 53.33px | −1.6px | −0.030 |
| 32px | −0.64px | −0.020 |
| 16px | −0.16px | −0.010 |
| 12px | −0.12px | −0.010 |
| 9.33px caps | +0.187px | +0.020 |
| 8px caps | +0.16px | +0.020 |

ABC Arizona Mix, consistently tighter than the grotesque at equivalent size: 24px/−0.96px (−0.040em), 16px/−0.96px (−0.060em), 14.67px/−0.587px (−0.040em).

Display work sits at weight **500**, not 700, despite 600 being loaded.

**Observed**

Opens with an oversized `IVENTIONS` wordmark tone-on-tone against the beige *(approximate `#E0D8CE` on `#F3EFEB`, ~1.3:1)*.

Two screens of calm warm beige, then one section detonates into acid chartreuse *(approximate `#E6FF7A`)* with event footage playing inside the letterforms of "Designed to be remembered." The quiet is what makes it land.

Structure worth stealing: a data table with micro-label headers (`PARTICIPANTS / INDUSTRY / EVENT TYPE / LOCATION`); eight testimonials numbered `01`–`08` with a `/08` counter; stats split into value and suffix spans (`270`+`+`, `90`+`%`, `1.2`+`K`), each with a written caption — *"That's ideas, not coffee. Brilliant ones, brewed daily."*

The headline ships as three separate markup copies for different breakpoints rather than reflowing one string — the line breaks are art-directed, not left to the browser.

**Technical note.** Smooth-scroll library plus `IntersectionObserver` reveals. Programmatic `scrollTo` **skipped the reveals entirely** and left sections blank. If you ship this combination, anchor links and deep links will land on empty screens unless handled.

**What to take**

The tracking ladder, verbatim. Quiet-then-loud pacing. Accent as a full section ground, not a button color. Captions with a voice.

---

## 4. Minh Pham — minhpham.design

Multidisciplinary designer portfolio.

**Measured**

| | |
|---|---|
| Typefaces | Avant Garde, Nunito Sans |
| Ground | `rgb(13, 13, 13)` — `#0D0D0D` |
| Document height | 8,248px |
| Assets | 1 `<canvas>`, 3 `<video>` |

**Observed — the failure**

A circular arc loader with a percentage counter riding the tip of the trace. Genuinely beautiful.

**The site never loaded.** First attempt reached 100% and stopped there; the arc reset and looped. A full reload stalled at 20%. Across roughly 60 seconds of waiting and a reload, the actual site was never seen. The content below was recovered from the DOM, not from the rendered page.

**What to take — the copy**

The voice is the asset, and it survives entirely in text:

> MAKING GOOD SHIT SINCE 2009

> **3D** — "I can produce anything that my 16" laptop can render"
> **MOTION** — "I use fancy motion that makes my design more interesting than it actually is"
> **TUTORIAL** — "I thought I'd make millions of $ from Youtube but I didn't"

The CV carries two titles per role, swapped on hover:

| Year | Official | Honest |
|---|---|---|
| NOW | Design Lead | Self-lead Designer |
| 2016 | Senior Product Designer | Regular Web Designer |
| 2012 | Art Director | Photoshop Doodler |
| 2009 | Flash Designer | Jurassic Designer |

Client credits undercut their own brag: Ford — *"Working on the Next-Generation HMI Experience without no driving experience."* UFC — *"despite not being a sports fan."* Lincoln — *"but never seen it in real life."*

**What not to take**

Canvas plus three videos behind a blocking loader with no skip. This site is the standing argument for the locked-out test. Every craft decision in it is good; the architecture made all of them invisible. **Take the voice, refuse the gate.**

---

## 5. Simply Chocolate — simplychocolate.dk

Danish chocolate brand, full commerce.

**Measured**

| | |
|---|---|
| Proprietary typefaces | **Simply Chocolate**, **Simply Chocolate Condensed**, **Simply Chocolate Ingredients**, Simply Header, SimplyChocolate Regular, Social Gothic |
| Third-party faces | Kanit, Libre Baskerville, Oswald, Poppins, Nunito Sans |
| Ground | `rgb(239, 239, 239)` — `#EFEFEF` (neutral) |

A commissioned type family — including a face drawn specifically for **ingredient lists**. That is the deepest brand-typography investment in the set.

**Observed**

Hero is a 50/50 split: video/photography on the left, a solid deep-burgundy panel on the right carrying the message *(approximate `#7B1B2E`)*. No text over imagery.

Navigation is symmetric with a centered wordmark — `SIMPLY®` — links flanking it, utilities right.

The collection page offers **three grid densities** via icon toggles, plus a product count and sort. Each product photograph sits on its own saturated ground *(approximate: burgundy `#7B1B2E`, forest `#1F5B3A`)*.

Cookie consent appeared on entry; declined all non-essential.

**What to take**

Split hero. Grid density control. Per-product color identity. Proof that a conversion-driven commerce site can stay brand-led rather than becoming a template with a logo dropped in.

**Caution**

Eleven font families load on this site. That's a real performance cost and it contradicts the two-family rule — the proprietary set is the asset; the Poppins/Oswald/Kanit layer is accumulated debt from apps and embeds. Ship the brand faces; audit what your third-party scripts drag in.

---

## Convergent findings

What multiple independent studios arrived at separately — the strongest signal in the whole record.

1. **No pure white, no pure black.** Zero of five.
2. **The warm grounds are effectively one color.** `#F4F2ED` and `#F3EFEB` differ by ≤8 points across all channels, chosen independently.
3. **Warm ground, cool ink.** `#F4F2ED` is red-leaning; `#111214` is blue-leaning. *In Pieces* does the same on dark with `#1A1A1D`.
4. **Tracking is inverse to size** — proven in both a lowercase grotesque (Iventions, −0.030em → +0.020em) and an all-caps condensed (In Pieces, +0.030em → +0.200em).
5. **Display type sits at weight 500,** not 700, on every site that loads a bold.
6. **The micro uppercase label appears on all five.**
7. **Numbering appears on all five** — `01/02/03`, `PIECE 1`, `/08`.
8. **Nothing bounces.** No overshoot observed anywhere.
9. **The loading state is designed** on four of five — and the fifth is the one that failed.
10. **Two sites independently shipped a density toggle.**
11. **Two or fewer typefaces** on every site that isn't carrying commerce-plugin debt.

---

# Casebook II — the mat register

Added September 2026, after the record above proved unable to describe a luxury
house. The five sites above are all in the **object** register; these are in the
**mat**. Measured live at 1614×914 unless a row says otherwise. Laws derived
from them are in `luxury-restraint.md`.

## 6. Cartier — cartier.com  *(measured)*

- **Typefaces:** Brilliant Cut (primary), Fancy Cut (secondary, 43 runs against
  thousands). Both proprietary. Named after diamond cuts — identity equals
  mechanism, in the house's own vocabulary.
- **Largest text on the homepage: 32px.** No display type exists on the page.
- **Dominant voice:** 12px / 400 / uppercase / `letter-spacing: 0.5px`, 382 runs.
  The second most common is the same at 12px with `line-height: 19.8px`, 205 runs.
- **Tracking:** 0.5px at 12px (0.042em) and at 16px (0.031em); 0.4px at 22px
  (0.018em) and at 30px (0.013em). The inverse law, in a luxury house's numbers.
- **Line height: a flat 1.5** — 18/12, 24/16, 33/22, 45/30. Not an inverse ladder.
- **Ink `#1D1C1C`** (3136 runs). Pure black appears 107 times, in borders and
  overlays, never as text. White `#FFFFFF` is the ground.
- **Accent `#E60000` and `#D50032`: five uses on the entire homepage.**
- **Motion:** 0.5s on 376 elements, 0.2s on 281, 0.3s on 157. The commonest
  duration is *above* the 300ms application ceiling. `ease-out` dominant at 588.
- **Imagery** covers essentially the whole scroll area.

## 7. Toteme — toteme.com  *(measured)*

- **One typeface: Toteme Sans.** Proprietary. Weights 300, 400, 700.
- **Largest text on the whole store: 20px** — the words "Fall Winter 26."
- **Dominant voice:** 11.2px at weights 400 and 700, 1040 runs each, line-height
  15.4px (**1.375**).
- **Tracking: `normal` at every size.** A counter-example worth keeping: a
  well-drawn proprietary face, left alone, in sentence case.
- **Ink `#090909`** on `#FFFFFF`. No accent colour at all.
- **Motion:** 0.3s on 175 elements; `ease` dominant.
- **Image area ÷ text area = 3.1 : 1**, computed over the full 3320px scroll.

## 8. Aesop — aesop.com  *(documented, not measured)*

Behind bot protection; the site could not be read, and working around that is
not something we do. Recorded from Fonts In Use: **Suisse Int'l** on the web,
**Optima** (as Zapf Humanist) in the logo, Neue Helvetica on packaging. Treat as
corroboration of the one-restrained-family pattern, never as a measurement.

## Convergent findings — register II

1. **The type ceiling is real and it is low.** 32px and 20px, two independent
   houses. Neither has display type.
2. **One family.** Both commissioned a face rather than picking one.
3. **Pure white grounds** — the only measured exception to the warm-ground law,
   and it holds only because photography covers the page.
4. **Ink is off-black on both,** `#1D1C1C` and `#090909`. The black half of the
   law survives the exception intact.
5. **The accent budget is countable on one hand,** or is zero.
6. **Motion runs slower than app motion** — 0.5s dominant on Cartier.
7. **Imagery outweighs type by more than 3:1** where it could be measured.
8. **Nothing bounces.** Holds across both registers, all eight sites.
