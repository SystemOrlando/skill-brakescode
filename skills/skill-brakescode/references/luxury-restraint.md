# The mat register

The house has two registers, not one. This file documents the second, because
the first — the object register in SKILL.md's "The two registers" — was for a
long time the only one written down, and a page that needed this one got built
in that one and came out wrong.

Call it **the mat**: the page behaves like a gallery mount. The work hangs on
it; the page's job is to not be seen.

---

## Measured evidence

Taken off the live sites, September 2026, 1614×914 viewport. Where a figure is
computed rather than read, it says so.

| | **Cartier** | **Toteme** |
|---|---|---|
| Typefaces | Brilliant Cut (primary), Fancy Cut (secondary) | Toteme Sans, alone |
| Largest text **anywhere on the page** | **32px** | **20px** |
| Dominant style | 12px / 400 / uppercase / +0.5px | 11.2px / 400 & 700 / sentence case |
| Tracking | 0.5px at 12px and 16px, 0.4px at 22px and 30px | `normal` at every size |
| Line height | 18/12, 24/16, 33/22, 45/30 — **flat 1.5** | 15.4/11.2 = 1.375; 21/14 and 24/16 = 1.5 |
| Ink | `#1D1C1C` | `#090909` |
| Ground | `#FFFFFF` | `#FFFFFF` |
| Accent | `#E60000` / `#D50032`, **5 uses on the whole homepage** | none |
| Transition durations | 0.5s (376 els), 0.2s (281), 0.3s (157) | 0.3s (175 els), 0.6s (7) |
| Image area ÷ text area | — | **3.1 : 1** (computed over the full 3320px scroll) |

Aesop is in the same register and could not be measured: the site is behind bot
protection, and getting around that is not something we do. Its type system is
documented rather than measured — **Suisse Int'l** on the web, **Optima** (as
Zapf Humanist) in the logo, per Fonts In Use. Treat it as corroboration, not as
a measurement.

**The headline number is the type ceiling.** Two independent luxury houses, and
the largest text on either homepage is 32px and 20px. Neither site has display
type at all. That is not an omission — it is the register.

---

## The precondition, and it is absolute

**This register requires that you actually have the photography.**

The mat works because something is hanging on it. Toteme's images occupy 3.1×
the area of its text; Cartier's cover essentially the whole scroll. Strip the
imagery and what remains is 11px grey text on white with a lot of air — which
is precisely the thin, template-shaped page this standard exists to prevent.

So, before choosing this register, answer in writing:

> What is hanging on the mat, and do I have it?

Real product photography, real art direction, real film. Not a gradient, not an
icon set, not a placeholder, not a CSS shape standing in for a photograph. If
the honest answer is "I don't have it," **this register is unavailable** and the
object register is the one to build in. Choosing the mat without the work is the
single most common way to produce an empty page that passes every negative
check, and it is Tell 0 in `anti-slop.md` wearing a nicer coat.

---

## The laws of this register

These **replace** the corresponding defaults while the register is in force.
Every one of them is contradicted by the object register, which is the point:
the two are alternatives, not a blend.

**1. Type has a ceiling, and it is low.** Nothing above ~32px. The page's
hierarchy comes from image scale and from position, not from type scale. If you
find yourself setting a 96px headline, you have left this register.

**2. Leading is a flat grid, not an inverse ladder.** Cartier runs 1.5 at 12px
*and* at 30px. Because nothing gets big, nothing needs to be pulled down. Set
one ratio between 1.375 and 1.5 and hold it at every size.

**3. One family.** Both measured sites have a proprietary face and use it for
everything; Cartier's second face appears 43 times against thousands. The
two-face allowance is a ceiling, not a target, and here the target is one.

**4. The ground may be pure white — here, and only here.** The standing rule is
warm grounds, and it holds everywhere else. It is suspended in this register for
a stated reason: when photography covers the page, the ground is a **mount**,
and a tinted mount casts its tint onto every image sitting on it. White is
neutral because the work is the colour. The ink is still not pure black —
`#1D1C1C` and `#090909`, both measured, both deliberately off.

**5. The accent budget is nearly zero.** Cartier's red appears **five times on
the entire homepage**. Not five places per screen — five, total. Toteme has no
accent at all. This is the loud-once test taken to its limit.

**6. Motion is slower than app motion.** Cartier's most common duration is
**0.5s**, well past the 300ms ceiling that governs application UI. Nothing here
is a control being operated dozens of times a day; these are images being
revealed. `motion.md`'s ceiling is a rule about *frequency*, and at this
frequency the ceiling lifts. Do not carry 0.5s back into a dropdown.

**7. Tracking discipline changes shape.** Cartier opens its uppercase micro-type
to 0.5px at 12px (0.042em) and tightens toward 0.4px at 30px — the inverse law,
intact. Toteme ships `normal` at every size and is not worse for it, because a
proprietary face is drawn with its own spacing and second-guessing it is how a
good face is made to look cheap. So: **open the tracking on uppercase micro-type;
leave a well-drawn face alone in sentence case.** The ban that stands is
unconsidered tracking, not zero tracking.

**8. Copy is short and declares nothing.** "Fall Winter 26" is a whole heading.
The adjective ban from SKILL.md is not relaxed here; it is barely needed,
because there is nowhere to put an adjective.

---

## Choosing between the registers

Ask what carries the page.

| The page is carried by… | Register | Because |
|---|---|---|
| Photography or film you actually have | **Mat** | The type's job is to caption and get out of the way |
| An idea, a mechanism, an argument, a catalogue | **Object** | Nothing is hanging on the mat, so the page must be the thing |
| A physical product that exists in space | Either — decide, then commit | The mat if you have the shoot; the object if you have to build it |

Two failure shapes come from getting this wrong, and both are common:

- **The mat without the work.** Empty. Reads as an unfinished template. This is
  the failure that produced the complaint that this file was written in answer
  to.
- **The object over real photography.** Loud frames and heavy condensed display
  fighting an art-directed image. The image loses, and the reason to have paid
  for it is gone.

**Do not blend them.** A page with 3.1:1 photography *and* a 96px condensed
headline *and* saturated colour fields is not "the best of both" — it is a page
with no decision in it. Pick the register in the commitment sheet, name it
there, and hold it to the footer.

---

## What does not change

The register changes values, never the criterion. Still binding, both registers:

- One idea, carried into the parts nobody designs. A restrained page still has
  to answer the spine test, and the mat register makes that *harder*, not
  easier — with less on screen, the 404 and the empty state carry more of the
  proof, not less.
- One loud moment, one focal point per section. In this register the loud moment
  is an **image**, at a scale nothing else on the page gets.
- 4.5:1 on body text. `#1D1C1C` on `#FFFFFF` measures **17.0:1**; `#090909` measures
  **19.9:1**. Restraint has never required low contrast, and grey-on-white at 11px
  is the register's most common counterfeit.
- `prefers-reduced-motion`, keyboard access, the locked-out test. A slow,
  image-heavy page is exactly the one that fails these, and "it's luxury" is not
  a defence — it is the reason to be stricter.
- Never the scaffold's typeface. Both measured houses commissioned a face. When
  a commission isn't on the table, pick a face with the same restraint and
  record it in the ledger like any other.
- Number things. Sequence still reads as curation.

---

## The self-check for this register

1. Name what is hanging on the mat. If you cannot, stop — wrong register.
2. Largest type on the page: is it under ~32px?
3. One family? Second face under ~2% of runs if there is one?
4. Ground white **because** the images need a neutral mount — or warm, per the
   standing rule?
5. Ink off-black, and measured against the ground?
6. Accent uses on the whole page: countable on one hand?
7. Image area ÷ text area: is it above 2:1? Below that, the mat is showing.
8. One leading ratio, held at every size?
9. Is the loud moment an image, and is there exactly one?
10. Does it still work with reduced motion, on a keyboard, on a slow line?
