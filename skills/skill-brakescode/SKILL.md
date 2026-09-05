---
name: skill-brakescode
description: brakescode's house standard for web work — the design criterion (one idea, carried into the parts nobody designs), a measured typographic tracking ladder, warm-ground/cool-ink color law, a two-tier motion system, fifteen signature interaction patterns drawn from studied reference sites, and the Next.js build/deploy discipline. Use this whenever building, designing, redesigning, reviewing or polishing any web interface — landing page, portfolio, product UI, marketing site, dashboard — for brakescode or for Orlando, and whenever starting a new web project from scratch. Reach for it even when the request sounds purely technical ("build the hero", "add a pricing section", "make this page"), because the house standard governs how the thing looks, moves and reads, not merely that it works. Also use it when picking type, tracking, color, spacing, easing, loaders, empty states or microcopy.
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

**The 8px test.** Find the smallest text on the page. Is its tracking set deliberately? Is its case deliberate? If the micro-label is running at browser defaults, the craft is decorative — it stopped where it got tedious. Every reference site treats sub-11px type as a designed system voice, not as leftovers.

**The locked-out test.** Can a person on a slow connection, with reduced motion on, using a keyboard, get to the content? *Minh Pham's* portfolio failed this in testing — canvas plus three videos behind a blocking loader, stalled at 20% across two full attempts, and the site was never seen. Ambition that locks the user out is not ambition. It's a broken site with good taste.

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
- **Two typefaces maximum.** One is a legitimate choice; *In Pieces* runs the entire site on one family in one weight and gets its hierarchy from size and tracking alone.
- **One signature moment per site.** Not five.
- **Every animation respects `prefers-reduced-motion`.** Non-negotiable, no exceptions, including the signature moment.
- **Body text hits 4.5:1.** Warmth is not an excuse for low contrast — `#111214` on `#F4F2ED` measures **16.9:1**. Softness and contrast are not in tension.
- **Number things.** `01 / 02 / 03`, `PIECE 1`, `/08`. Sequence makes a page read as curated rather than dumped.
- **No spinner. Ever.** If it must load, the loading state says something true about what's loading.

## How to use this skill

Start with the criterion and the four tests — those do most of the work. Pull in a reference file when you're making that specific class of decision:

| File | Read it when |
|---|---|
| `references/typography.md` | Choosing faces, sizes, weights, tracking, or building the type scale |
| `references/color.md` | Building a palette, picking grounds and inks, checking contrast |
| `references/motion.md` | Any animation, transition, easing, loader, or scroll behavior |
| `references/patterns.md` | You want a specific signature interaction, with implementation |
| `references/casebook.md` | You want the exact measured evidence — fonts, hexes, timings, per site |

`patterns.md` is a catalog, not a menu to work through. Take one. A page that uses eight of them has failed the loud-once test.

**Relationship to other design skills.** `impeccable` and the general frontend-design skills are broad craft references and remain useful for anything this standard doesn't cover — accessibility depth, form design, information architecture, dashboard layout. Where they and this standard disagree on a specific value — a color, a duration, a tracking figure, a typeface count — **this standard wins**, because these numbers were measured off work we chose deliberately. Use them together: this decides the house character; they fill in the general craft.

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
