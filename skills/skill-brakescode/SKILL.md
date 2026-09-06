---
name: skill-brakescode
description: brakescode's house standard for web design and development, and the conductor that decides which other design skills to bring in and in what order. Carries the design criterion (one idea, carried into the parts nobody designs), a measured typographic tracking ladder, the warm-ground/cool-ink color law, a two-tier motion system, fifteen signature interaction patterns, an anti-slop pass that catches work reading as machine-made — generic alternating layouts, default framework palettes, unmodified library components, transition-all, corporate copy, and flatness from restraint that was never spent — plus the Next.js build and deploy discipline. Use this whenever building, designing, redesigning, reviewing or polishing any web interface — landing page, portfolio, product UI, marketing site, dashboard — for brakescode or for Orlando, and whenever starting a new web project from scratch. Reach for it even when the request sounds purely technical ("build the hero", "add a pricing section", "make this page"), because the house standard governs how the thing looks, moves and reads, not merely that it works. Use it too when work feels flat, generic, templated or AI-made and needs a point of view, when picking type, tracking, color, spacing, layout, easing, loaders, empty states or microcopy, and when deciding whether impeccable, animate, apple-design, framer-motion or the other design skills should be running on this task. Use it for anything with a z-axis too — 3D objects, figures, scenes, depth, parallax, WebGL, Three.js, lighting, materials and shadows — where it runs a dedicated seven-step lane that decides whether the thing should exist in space at all, picks the cheapest technique that works, and pulls in every relevant skill in order.
---

# brakescode

The house standard. It exists so that work shipped under this name is recognizable as ours before anyone reads the logo.

## The criterion

**One idea, carried further than is comfortable, into the parts nobody designs.**

This is not a style. It's a test you can apply to any decision. The reference sites this standard is drawn from — documented in `references/casebook.md` — are not united by a look. They're united by the fact that each one picked a single idea and refused to stop applying it.

*In Pieces* decided "thirty species, thirty triangles, CSS only" and then built the logo out of triangles, derived each page's palette from the animal on screen, and wrote its loading message as "RE-ARRANGING THE PIECES." *'kin* decided "the work is the interface" and removed the scrollbar, hid the navigation, and made the twenty-second preloader out of the project photography itself, compressed into a hairline. Neither stopped at the homepage.

Four tests apply this criterion. Run them before shipping anything.

**The spine test.** Say the idea in one sentence. Now check: does the palette come from it? The type? The motion? The loading state? The 404? If the idea only shows up in the hero, there is no idea — there's a hero.

**The loud-once test.** Count the loud moments. There should be exactly one. *Iventions* is warm beige and near-silent for two full screens, and then detonates into acid chartreuse with video playing inside the letterforms. The beige is what makes the chartreuse work. A site that is loud in five places is loud in none.

**The same rule holds one level down: one focal point per section.** Whatever else is on screen yields to it. If the headline carries a bold treatment, the buttons and icons go flat; if the ground carries an effect, the type goes clean and solid. Competing for attention in three places at once means the reader is given no order to read in, and the section reads as busy rather than as designed. Decide what wins each screen, then actively quiet everything else — subordination is a decision you make, not a thing that happens.

**Zero is the more common failure, and the harder one to see.** A page that refuses every cliché and then commits to nothing passes every negative check and is flat. Restraint is a budget, not a virtue — so name what you spent it on. If you cannot point at one element, one moment, or one passage that is genuinely large, dense, saturated, fast, or strange, the budget is unspent and the work is thin. That failure is Tell 0 in `references/anti-slop.md`, and it is a planning failure: no amount of CSS rescues a page that committed to nothing.

**The 8px test.** Find the smallest text on the page. Is its tracking set deliberately? Is its case deliberate? If the micro-label is running at browser defaults, the craft is decorative — it stopped where it got tedious. Every reference site treats sub-11px type as a designed system voice, not as leftovers.

**The locked-out test.** Can a person on a slow connection, with reduced motion on, using a keyboard, get to the content? *Minh Pham's* portfolio failed this in testing — canvas plus three videos behind a blocking loader, stalled at 20% across two full attempts, and the site was never seen. Ambition that locks the user out is not ambition. It's a broken site with good taste.

## The house tilt

The criterion above is neutral about *where* the loud moment sits on the scale from restrained to vernacular. The house is not. This section records the calibration, and it is a stated preference rather than something derived from the casebook — worth knowing, because the casebook sites sit at the restrained end and this house sits well past them.

Given two executions that both pass the criterion, **the house prefers the one that is an object over the one that is a document.**

Concretely, tested head to head on the same content:

| Preferred | Over |
|---|---|
| Color as **fields** — saturated blocks that carry structure | Color as a single ink on a ground |
| Heavy condensed display at genuinely large scale | A refined face at a polite size |
| Frames, edges, hard offset shadows — things with a physical border | Hairline rules and open composition |
| Irregularity as structure — rotation, staggered heights, overlap | Everything squared to one axis |
| **Vernacular** sources: folk printing, packaging, signage, games, market ephemera | Editorial sources: publications, studio identities, archival documents |
| One color per item, changing the world as you move through it | One palette holding still across the page |

The monochrome-and-hairlines register is not banned — it is correct for a genuinely documentary subject, and `references/casebook.md` shows it done superbly. But it is **not the default here**, and reaching for it because it is safe is how a page ends up passing every check while reading thin. When the brief leaves the register open, take the louder reading.

This does not loosen anything. Contrast floors, the tracking and line-height ladders, one loud moment per page, one focal point per section, reduced motion, and the anti-slop pass all still bind. Bold and undisciplined is not the target; **bold and exact** is.

**The tilt's own failure mode: scaling everything.** Read "heavy display at large scale" and the obvious move is to enlarge the whole page — display *and* body *and* cards *and* padding. That produces no hierarchy at all, only zoom, and a page that feels held against the reader's face. The tilt applies to **the one loud element**. Everything else gets smaller and quieter to pay for it, because hierarchy is the *ratio* between them, not the size of either. Full treatment in `references/space-and-depth.md`.

## Dimension

The criterion applies to the z-axis without amendment, and it is where it bites hardest: **identity equals mechanism** means a thing may occupy space only when space is what the thing *is*. A textile has a reverse. A building has a section. A stack has layers. Those earn depth. A shape that rotates because rotation looks expensive does not, and it is the single most recognizable generated move on the web.

The house position, in one line: **take the cheapest rung that does the job.** Most requests for "3D" are answered by CSS 3D transforms — no library, nothing in the bundle — and the jump to WebGL costs hundreds of kilobytes, a GPU dependency and a whole class of device failures. Cross it for a real object or a real mechanism, never to make a section feel richer.

When you do build in space, the finish is three things and they are all in `references/dimension.md`: **light** (one key, a deliberate key-to-fill ratio, opposite temperatures — ambient-only light removes the gradients and without gradients there is no form), **material** (metalness is binary, roughness carries the character, and most real things are rougher than 0.7), and **shadow** (the contact shadow is the one that matters, a real penumbra sharpens at the contact, and no shadow is ever black).

## Working principles

These follow from the criterion. When a specific rule below and the criterion disagree, the criterion wins — the rules are its consequences, not its replacement.

**Be quiet so you can be loud.** Restraint is the budget that pays for the one big move. Spend the page on silence and the signature moment lands. Spend it on effects and nothing lands.

**Show, don't claim.** *Iventions* never writes "we make memorable experiences." It runs event footage inside the word "remember." When you catch yourself writing an adjective about the work, replace it with a demonstration of the work.

**Personality lives in microcopy, not the hero.** Hero copy is almost always forced. The voice shows up in the small print: *Minh Pham* lists his 2009 job as "Flash Designer" and, on hover, "Jurassic Designer." *Iventions* labels its lightbulb-moments stat "That's ideas, not coffee. Brilliant ones, brewed daily." Write the hero plainly and put the wit where it's a gift to whoever reads carefully.

**Design the states nobody opens.** Loading, empty, error, offline, zero-results, the 404. These are where the criterion is proven, because they're where everyone else defaults. A spinner is an admission that nobody thought about this screen.

**Slowness is confidence — once, and never blocking.** A twenty-second reveal reads as certainty when it is the site's single signature moment and the user can move past it. The same twenty seconds spent behind a progress gate reads as a broken site. See `references/motion.md`.

**Give the user control.** Both *'kin* and *Simply Chocolate* let the visitor choose grid density. *In Pieces* offers sound off, shuffle, and a skip. Control is not clutter; it's respect, and it costs almost nothing to implement.

**Identity should equal mechanism.** When the technique that makes the work possible can also make the logo, the marks, the transitions — use it. That's what makes a site feel authored instead of assembled.

## Non-negotiables

These are short because they're absolute. The reasoning is in the reference files.

- **Never `#FFF`, never `#000`.** Warm grounds, cool inks. Not one reference site uses pure white or pure black. → `references/color.md`
- **Tracking is inversely proportional to size.** Large type tightens, micro type opens. Never ship default tracking on display or on labels. → `references/typography.md`
- **Two typefaces maximum**, and **never the scaffold's.** Geist, Inter as display, and the system stack are what arrive when nobody chose — shipping them is indistinguishable from not deciding. Pick the face from the subject's own typographic tradition. → `references/typography.md`
- **Line height is inverse to size.** Display locks down to 0.88–1.0; body opens to 1.5–1.65. Browser defaults are wrong at both ends and visibly break large headlines.
- **Space is hierarchical, never uniform.** The gap between two things is inversely proportional to how related they are, which puts roughly 20:1 between a page's largest and smallest gaps. `p-6` on everything is the absence of a decision. → `references/space-and-depth.md`
- **Borders and shadows are derived, not picked.** On dark, the border is the text color at 0.05–0.10 opacity. On light, the shadow is tinted toward the ground's hue, layered, and offset — never `rgba(0,0,0,0.1)`. Declare elevation once: a rule, a shadow, or a background step, not two of them.
- **Theme what the browser draws.** `::selection`, `caret-color`, `:focus-visible`, the scrollbar, and tabular numerals ship with defaults that belong to no design system. Theming them is the cheapest signal that a page was built rather than assembled, and the one most reliably skipped.
- **One signature moment per site.** Not five.
- **Every animation respects `prefers-reduced-motion`.** Non-negotiable, no exceptions, including the signature moment.
- **Body text hits 4.5:1.** Warmth is not an excuse for low contrast — `#111214` on `#F4F2ED` measures **16.9:1**. Softness and contrast are not in tension.
- **Number things.** `01 / 02 / 03`, `PIECE 1`, `/08`. Sequence makes a page read as curated rather than dumped.
- **No spinner. Ever.** If it must load, the loading state says something true about what's loading.
- **An abstract rotating object is never the answer.** The slowly turning glassy blob over a particle field is the most legible generated page there is. Depth is earned by three cases only — the product *is* a physical object, the mechanism *is* spatial, or depth carries the hierarchy. → `references/dimension.md`
- **One dimensional element per page**, and the static frame it degrades to must stand on its own. If the poster only works because of the lighting, the lighting is doing the composition's job.
- **One sun.** A page's CSS shadows, its hard offsets and its 3D key light all fall the same way. Two light directions on one page is the fastest way to look assembled.

## How to use this skill

Start with the criterion and the four tests — those do most of the work. Pull in a reference file when you're making that specific class of decision:

| File | Read it when |
|---|---|
| `references/orchestration.md` | **Starting any design or build** — who plays when, and who wins conflicts |
| `references/anti-slop.md` | **Before writing UI, and again before shipping** — the machine-made tells |
| `references/typography.md` | Choosing faces, sizes, weights, tracking, line height, or building the type scale |
| `references/color.md` | Building a palette, picking grounds and inks, checking contrast |
| `references/space-and-depth.md` | Spacing, rhythm, borders, shadows, elevation |
| `references/motion.md` | Any animation, transition, easing, loader, or scroll behavior |
| `references/dimension.md` | 3D, depth, parallax, WebGL, ambient motion |
| `references/patterns.md` | You want a specific signature interaction, with implementation |
| `references/casebook.md` | You want the exact measured evidence — fonts, hexes, timings, per site |

The first two are not optional on real work. `orchestration.md` decides which other skills to bring in and in what order; `anti-slop.md` runs twice — against the plan, where the expensive failures are cheap to fix, and against the finished page.

`patterns.md` is a catalog, not a menu to work through. Take one. A page that uses eight of them has failed the loud-once test.

## This standard conducts; it does not play every instrument

brakescode decides **what kind of thing this is**. The specialist skills decide **how to build it well**. Character, palette, type, timing, the single loud moment and the anti-slop verdict belong here, because they are what make the work recognizable as ours. Craft depth — spring tuning, gesture handoff, accessibility, library APIs — belongs to whoever specializes in it.

The short version of the running order, with the full table and the roster in `references/orchestration.md`:

1. **Direction** — this SKILL.md's criterion, then `impeccable` for a new surface (or `redesign-existing-projects` when something must be preserved).
2. **Anti-slop gate** — `references/anti-slop.md` against the *plan*, before any UI exists.
3. **Visual system** — `color.md` and `typography.md` here, plus `impeccable`'s `craft-floor.md` for the mechanics this standard doesn't cover.
4. **Components** — `pick-ui-library`, `magic-ui`, `ask-sonner`, `sileo-react-toasts`. Library components ship **modified**, never stock.
5. **Motion** — `motion.md` sets the timing and the one-moment rule; `animate`, `animate-expo`, `apple-design`, or the `framer-motion-*` set does the building. For anything with a z-axis — 3D, parallax, WebGL, ambient drift — read `dimension.md` first: it decides whether the thing should exist in space at all before anyone picks a library.
6. **Anything with a z-axis** — 3D objects, figures, scenes, depth, WebGL — runs the **seven-step 3D lane** in `references/orchestration.md`, which convenes `dimension.md`, `pick-ui-library`, `vercel:performance-optimizer`, `impeccable`, `animate`, `apple-design`, the `framer-motion-*` set, `emil-design-eng` and `review-animations` in order.
7. **Review** — the four tests and the anti-slop self-check, then `impeccable`'s finish reviewer, `review-animations`, or `improve-animations`.

**Who wins.** The user's instruction beats everything. A brief-pinned constraint beats the roll. On a specific *value* — a color, a duration, a tracking figure, a typeface count — **this standard wins**, because these numbers were measured off work chosen deliberately. On *technique and depth*, the specialist wins and this standard should not invent an opinion. When two skills ban and encourage the same thing, the stricter rule holds and you name the reconciliation out loud instead of silently picking a side.

## Build discipline

The standard governs how the work is made as well as how it looks.

**Default stack.** Next.js + React with Tailwind, conventional structure (`app/`, `components/`). Deviate when the project has a reason, not by default.

**Never run `next build` while the dev server is up.** Both write to the same `.next` directory and the build output corrupts. Stop the dev server first. This has bitten past projects; treat it as a live hazard, not a theoretical one.

**Verify in the browser, not in the compiler.** A clean type-check proves nothing about a visible change. Start the dev server through the project's preview tooling (never a detached `npm run dev` in a shell), click through the actual flow, and check the small viewport and the reduced-motion case. If the change can't be previewed in the current environment, say so plainly rather than implying it was verified.

**Deploy targets.** Frontend → Vercel. Backend and DB-backed services → Render. Cloudflare is fine for static or edge-hosted frontends. No new provider without a reason.

**Write code that reads like the code around it.** No premature abstraction — three similar lines beat a helper built for a fourth case that hasn't appeared. No comments restating what the code does; only non-obvious *why*. No validation, fallbacks, or flags for situations the task doesn't have. No scaffolding "for later."

**Move, then report.** Default to executing without pausing for permission on routine steps, then summarize what changed. This does not extend to destructive or irreversible actions — force-push, dropping data, deleting branches, spending money — which get a check-in regardless.

## What this standard rejects

Recognizing the failure modes is faster than remembering the rules.

- Pure white backgrounds with pure black text
- Default letter-spacing at every size
- Three or more typefaces, or a fourth weight nobody needed
- Generic spinners and "Loading…"
- Copy that asserts quality: "innovative solutions," "cutting-edge," "seamless experience"
- Springy overshoot on everything — bounce is a specific decision, not a default personality
- Blocking loaders past ~3s with no way through
- Auto-advancing carousels the user can't stop
- Motion that ignores `prefers-reduced-motion`
- Effects added because they're impressive rather than because the idea required them
- A hero that carries the entire design while the footer, the 404, and the empty state are stock
