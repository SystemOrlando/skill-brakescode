# Orchestration

brakescode is the conductor. The other skills are the sections of the orchestra: each one knows its instrument better than this standard does, and none of them knows the house character. This file says who plays when, and who wins when two disagree.

## Contents

- [The rule of authority](#the-rule-of-authority)
- [The phases](#the-phases)
- [The roster](#the-roster)
- [Conflict resolution](#conflict-resolution)
- [What not to load](#what-not-to-load)

## The rule of authority

**brakescode decides *what kind of thing* this is. The specialist decides *how to build it well*.**

Character, palette, type, timing, the single loud moment, the anti-slop verdict — this standard owns those, because they are what make the work recognizable as ours. Craft depth — how a spring is tuned, how a gesture hands off, how a focus order works, which library to use — belongs to whoever specializes in it.

Where a specialist's *value* contradicts a house law (a color, a duration, a tracking figure, a typeface count), the house law wins. Where a specialist's *technique* is better than anything here, take it. This standard is opinionated about outcomes, not about methods.

## The phases

Run these in order. Skip a phase only when the task genuinely has none of it.

### 1 — Direction

Load: **this SKILL.md** (the criterion and its four tests), then **`impeccable`** for a new surface or a replacement world.

`impeccable` owns the machinery: the concept seed roll, the challenger weighing, the direction contract, the surface brief. brakescode supplies the character the roll has to survive, and its pinned constraints (warm ground, cool ink, ≤2 faces, one loud moment) beat the roll, always. The seed still binds through topology, controls, state vocabulary and ritual — translate materials rather than discarding the assignment, and name the translation.

For an existing site being reworked rather than replaced, load **`redesign-existing-projects`** instead: it audits the incumbent before touching it, which is the right first move when there is something to preserve.

### 2 — Anti-slop gate — before writing any UI

Load: **`references/anti-slop.md`**.

Run it against the *plan*, not the finished page. Catching the alternating stack, the flat ground, or the unspent restraint budget while it is still a paragraph in a brief costs nothing; catching it in a built page costs a rebuild. Tell 0 in particular is a planning failure, not a styling one — you cannot fix a page that committed to nothing by adjusting its CSS.

### 3 — Visual system

Load: **`references/color.md`**, **`references/typography.md`**, and **`impeccable`'s `craft-floor.md`** immediately before editing UI.

brakescode's laws are the floor for palette and type. craft-floor covers the mechanics this standard does not — contrast checks, spacing reads, browser surfaces (selection, caret, scrollbar, focus ring, tabular numerals), and the ban list.

Reach for **`design-taste-frontend`** or **`emil-design-eng`** when the work needs taste calibration beyond the laws — the former for landing pages and portfolios that must not look templated, the latter for component-level polish and the invisible details. Treat both as taste references, not as a second standard.

### 4 — Components

Load: **`pick-ui-library`** when the stack is undecided; **`magic-ui`** when the project already uses it or wants that catalogue; **`ask-sonner`** or **`sileo-react-toasts`** for toasts.

Non-negotiable from `anti-slop.md`: **a library component ships modified.** Keep its geometry and its accessibility baseline; replace border weight, elevation, radius, density, and all four interaction states. A stock component inside a committed world is a costume with the tag still on.

### 5 — Motion

Load: **`references/motion.md`** for the timing and the signature-moment rule, then the specialist:

| Situation | Skill |
|---|---|
| Building an animation from scratch, web | **`animate`** |
| React Native / Expo | **`animate-expo`** |
| Project uses Framer Motion | `framer-motion-react`, then the one that matches: `-gestures`, `-layout`, `-scroll`, `-variants` |
| Gesture-driven, physical, iOS-feeling motion | **`apple-design`** |
| You need the name of an effect you can only describe | **`animation-vocabulary`** |
| 3D, depth, parallax, WebGL, ambient motion | **`references/dimension.md`** first, then the specialist |

brakescode caps the durations and allows exactly one signature moment; the specialist decides the curve, the interruption, the handoff, and the degradation. Everything respects `prefers-reduced-motion` — no specialist overrides that.

### 6 — Review

Load: **`references/anti-slop.md`** again (the self-check at the end), then run this standard's **four tests** — spine, loud-once, 8px, locked-out.

Then hand off: **`impeccable`'s finish reviewer** for the surface as a whole, **`review-animations`** for a motion diff, **`improve-animations`** for a whole-codebase motion audit, **`find-animation-opportunities`** when the page is inert and should not be.

A review you run on your own work in the same context inherits your framing and your optimism. Spawn the reviewer fresh whenever the harness allows it.

### 7 — Long or exhaustive output

Load **`full-output-enforcement`** when the deliverable must be complete and the risk is truncation or placeholder stubs — a full design system, a long migration, a file that must ship whole.

## The roster

Everything installed, and the one line that says when it earns loading.

| Skill | Load it when |
|---|---|
| `impeccable` | Any new surface, replacement world, or finish review — the craft spine |
| `redesign-existing-projects` | Reworking something that already exists and must be preserved |
| `design-taste-frontend` | Landing pages and portfolios at risk of looking templated |
| `emil-design-eng` | Component polish and the invisible details |
| `apple-design` | Gesture, spring, sheet, momentum, translucency, physical motion |
| `animate` / `animate-expo` | Building motion, web / Expo |
| `framer-motion-*` | The project uses Framer Motion; pick by concern |
| `animation-vocabulary` | You can describe the effect but not name it |
| `review-animations` | Critiquing motion in a diff |
| `improve-animations` | Auditing motion across a codebase |
| `find-animation-opportunities` | The UI is inert and should not be |
| `pick-ui-library` | Component stack undecided |
| `magic-ui` | Project uses Magic UI |
| `ask-sonner` / `sileo-react-toasts` | Toasts |
| `prototype` | Throwaway exploration where the standard's finish rules would only slow you down |
| `full-output-enforcement` | The output must be exhaustive and unabridged |
| `write-swift` | Swift — out of this standard's scope entirely |

## Conflict resolution

Resolve field by field. Never split the difference into a compromise nobody chose.

1. **The user's explicit instruction beats everything**, including this standard.
2. **A brief-pinned constraint beats the roll** and beats every skill's default.
3. **On a specific value** — a color, a duration, a tracking figure, a typeface count, a radius — **brakescode wins.** Those numbers were measured off work chosen deliberately; a general skill's default was not.
4. **On technique and depth** — accessibility, gesture handoff, state machines, library APIs, performance — **the specialist wins.** This standard has no opinion there and should not invent one.
5. **On a ban** — one skill forbids what another encourages — the stricter rule holds unless the brief explicitly earns the exception, and you name the reconciliation out loud rather than silently picking a side.

Two known live conflicts, already reconciled, kept here so nobody re-litigates them:

- **Micro-labels vs. the eyebrow ban.** `craft-floor` bans a kicker above a heading with no exceptions; this standard likes tiny tracked caps. Reconciliation: micro-labels are legitimate as **metadata** (entry numbers, origins, counts, section markers that are themselves the heading). They are never a label sitting above a heading. The ban holds.
- **Ground texture vs. the `feTurbulence` ban.** `craft-floor` bans SVG-filter grain as amateur; `anti-slop.md` calls flat grounds a tell. Reconciliation: no live `feTurbulence` as a visible texture effect. A tiled noise asset under ~4% opacity, or real material from the subject's world, is the answer. If you can see grain rather than feel depth, it is too strong.

## What not to load

Loading a skill you do not need costs context and dilutes the direction with advice aimed at a different problem.

- Do not load motion skills for a static page with no motion.
- Do not load `impeccable`'s full command set for a narrow change to an existing component; the incumbent implementation is the authority there.
- Do not load two taste references at once. Pick the one that matches the surface.
- Do not load this standard's own reference files speculatively. Each one names the decision that earns it.
