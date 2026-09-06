# Dimension

Depth, 3D and ambitious motion. `motion.md` governs timing and the single signature moment; this file governs when a thing should exist in space at all, and how to build it without wrecking the page.

## Contents

- [The rut](#the-rut)
- [When 3D earns its place](#when-3d-earns-its-place)
- [The ladder](#the-ladder-cheapest-first)
- [CSS 3D](#css-3d)
- [Scroll-driven depth](#scroll-driven-depth)
- [WebGL](#webgl)
- [Worked example: the second face](#worked-example-the-second-face)
- [The measurement trap](#the-measurement-trap)
- [Finishing: light](#finishing-light)
- [Finishing: material](#finishing-material)
- [Finishing: shadow](#finishing-shadow)
- [The finishing checklist](#the-finishing-checklist)
- [Non-negotiables for anything dimensional](#non-negotiables-for-anything-dimensional)
- [Ambient motion](#ambient-motion)

## The rut

Ask a model for 3D and you get the same page every time: a glassy sphere or a soft gradient blob, slowly rotating, lit from nowhere, floating over a dark ground with a particle field behind it. Sometimes a wireframe globe. Sometimes an abstract torus knot.

None of it means anything. It is 3D as texture — a thing that spins because spinning looks expensive — and it is instantly legible as generated. The house position: **an abstract rotating object is never the answer.** If the only reason a shape is in space is that space looks impressive, take it out and spend the budget on the type.

## When 3D earns its place

Three cases, and outside them the answer is no.

**1. The product is a physical object.** A textile, a bottle, a chair, a machine, a printed piece. Letting someone turn it is showing the product, and no photograph does what a turn does. This is the strongest case and the most under-used.

**2. The mechanism is spatial.** A loom, a building section, a stack of layers, an assembly, a map, a signal path. The subject genuinely has a z-axis and flattening it loses information. Here depth is explanation, not decoration.

**3. Depth carries the information hierarchy.** Layers that are actually layers — a comparison where one thing sits over another, an archive where recency is distance. Rare, and easy to fake badly, but real when it holds.

The test is the same as everywhere in this standard: **identity equals mechanism.** If the technique that makes the object possible could also make the marks, the transitions and the loading state, it belongs. If it is a shape you added afterwards, it does not.

## The ladder, cheapest first

Stop at the first rung that does the job. Most requests for "3D" are answered at rung one or two.

| Need | Tool | Cost |
|---|---|---|
| Layered parallax, things that sit over other things | 2D transforms + `z-index` | free |
| A card that turns, a box that opens, real perspective | **CSS 3D transforms** | free |
| Depth tied to scroll position | CSS `animation-timeline: view()` | free |
| A specific object the user can orbit, lit and textured | **WebGL** (Three.js / react-three-fiber) | 150 KB+ and a real budget |
| Physics, many objects, simulation | WebGL + a physics lib | a project, not a feature |

The gap between rung two and rung four is enormous — hundreds of kilobytes, a GPU dependency, an accessibility surface, and a whole class of device failures. Cross it only for case 1 or 2 above, never to make a section feel richer.

## CSS 3D

Genuinely 3D, no library, composited on the GPU. Underrated because it does not look like "3D" in the marketing sense — which is exactly why it reads as craft rather than as a demo.

```css
.stage {
  perspective: 1200px;          /* lower = more dramatic; 800–1600 is sane */
  perspective-origin: 50% 40%;
}

.object {
  transform-style: preserve-3d;
  transition: transform 520ms cubic-bezier(0.23, 1, 0.32, 1);
}

@media (hover: hover) and (pointer: fine) {
  .stage:hover .object { transform: rotateY(-18deg) rotateX(6deg); }
}

.object__face      { backface-visibility: hidden; }
.object__face--back { transform: rotateY(180deg); }
```

Things that go wrong:

- **`preserve-3d` collapses** if any ancestor sets `overflow`, `filter`, `opacity < 1`, `mask` or `contain`. Every one of those forces a flattened stacking context and your 3D silently becomes 2D. Check the whole chain, not just the parent.
- **Perspective belongs on the container**, not the moving element. On the element it recomputes per item and the vanishing points disagree.
- **Text in 3D goes soft.** Rasterization happens before the transform, so rotated type blurs. Keep text on a face that stays parallel to the viewer, or accept it only at display sizes.
- **Hard shadows survive rotation; soft ones do not.** A blurred shadow on a rotating plane reads as a sticker.

## Scroll-driven depth

Depth tied to scroll needs no JavaScript in modern browsers, which removes the main-thread cost that made parallax feel cheap:

```css
@supports (animation-timeline: view()) {
  .layer {
    animation: recede linear both;
    animation-timeline: view();
    animation-range: entry 0% exit 100%;
  }
  @keyframes recede {
    from { transform: translateZ(-120px) translateY(4%); }
    to   { transform: translateZ(0)      translateY(-4%); }
  }
}
```

Keep travel small. Parallax that moves layers hundreds of pixels is the 2014 tell; 20–60px of differential is enough for the eye to read depth and does not fight the scroll.

## WebGL

Only for case 1 or 2, and treat it as a feature with a budget rather than a visual choice.

- **Load it lazily.** Dynamic-import the renderer when the section approaches the viewport. Nothing 3D should be in the initial bundle.
- **Ship a poster frame.** A static render of the object at its default angle, shown until the canvas is ready and kept permanently for reduced-motion, failed contexts, and print. If the poster alone communicates the thing, question whether the canvas is needed.
- **Cap the pixel ratio** at 2 (`renderer.setPixelRatio(Math.min(devicePixelRatio, 2))`). Uncapped DPR on a phone renders four times the pixels for no visible gain and cooks the battery.
- **Pause offscreen and on blur.** An `IntersectionObserver` that stops the render loop, plus `visibilitychange`. A canvas spinning in a background tab is a real cost to a real person.
- **`powerPreference: 'low-power'`** unless the scene genuinely needs the discrete GPU.
- **Handle context loss.** `webglcontextlost` fires on mobile more than people expect; without a handler the section goes permanently blank.
- **glTF, Draco-compressed**, and check the actual transferred size. A "simple" model is routinely 5–20 MB before compression.

Order of magnitude for a single lit object with orbit: **~180 KB** of runtime plus the model. Say that number out loud before agreeing to it.

## Worked example: the second face

Built and verified, and the clearest case the standard has for CSS 3D over WebGL.

A woven pallay in complementary-warp weave has a reverse that is the **exact negative** of its face: every thread that floated on top is underneath on the back. So a control that turns the cloth is not a card-flip effect — it is the one view a photograph cannot give, and the product's own material fact.

Two things made it work, and both generalize:

**The second face has to be true.** A flip that reveals a decorative back, a logo, or a repeat of the front is the card-flip cliché and reads as a widget. A flip that reveals real information — the reverse of the cloth, the inside of the box, the section behind the elevation — is the product. If you cannot say what is on the other side and why someone would want it, there is no other side; there is a rotation.

**Verify the truth numerically, not by eye.** The face carried 23 filled cells and the reverse 26, summing to the grid's 49. That arithmetic is what proves the negative is exact rather than approximate, and it caught nothing wrong only because it was run — an inverted pattern that is subtly not the true inverse looks completely convincing in a screenshot.

The whole thing is `transform-style: preserve-3d`, `rotateY(180deg)` on a toggle, and `backface-visibility: hidden`. No library, no model, nothing in the bundle.

## The measurement trap

**`getComputedStyle(el).transform` can report a 2D identity matrix for an element that is rendering a correct 3D rotation.** Observed in a real build: an inline `rotateY(60deg)` returned `matrix(1, 0, 0, 1, 0, 0)` while the element was visibly foreshortened on screen, with the near edge larger and the far edge receding.

Several checks were spent chasing a bug that did not exist, and the fix was to take a screenshot. So:

**Verify 3D by looking at it.** The CSSOM is not a reliable witness here. Read computed styles for the things they do report faithfully — `transform-style`, `perspective`, `backface-visibility`, and the ancestor chain that might be flattening the scene — and settle the rotation itself visually.

This is the house rule about verifying in the browser rather than the compiler, turned on the measurement itself: an instrument that disagrees with the render is the instrument being wrong, and the render is the deliverable.

## Finishing: light

**Nothing separates a render that looks made from one that looks generated more than the lighting**, and the generated one is always lit from everywhere. Ambient-only light — a uniform environment with no dominant source — removes every gradient across a surface, and without gradients there is no form. The object reads as a flat sticker of itself.

**Decide one key light and commit to it.** Direction, height, and colour, written down. Everything else on the page then obeys the same sun: the 2D shadows in `space-and-depth.md`, the hard offsets, the highlight side of any photograph. A page whose CSS shadows fall down-right and whose 3D object is lit from the left is a page with two suns.

The three-light convention, in the proportions that actually matter:

| Light | Job | Relative intensity |
|---|---|---|
| **Key** | Makes the form. Above and 30–45° to one side. | 1.0 |
| **Fill** | Opens the shadow so it is not black. Opposite the key, low. | 0.15–0.25 |
| **Rim** | Separates the object from the ground. Behind, high, narrow. | 0.3–0.6, optional |

**The key-to-fill ratio is the entire mood.** 8:1 is dramatic and material; 4:1 is a product shot; 1:1 is the flat generated look. Start at 5:1 and move deliberately.

**Never light from below.** Millions of years of the sun being overhead means under-lighting reads as uncanny, and no brief asks for that by accident.

**Give the key and the fill opposite colour temperatures.** A warm key with a cool fill (or the reverse) is what makes the shadow side read as *in shadow* rather than as *darker*. This is the same law as warm-ground/cool-ink in `color.md`, applied to photons: two neutral lights produce a grey object no matter what colour it is.

```js
key.color.set('#fff1dc');  key.intensity = 1.0;   // cálida
fill.color.set('#cfe0ff'); fill.intensity = 0.2;  // fría, opuesta
```

**On environment maps:** in a physically-based renderer the environment *is* most of the lighting, not a backdrop. This is why every generated 3D page looks alike — the default studio HDRI, with its softbox rectangles and grey seamless, is baked into every starter. Its reflections are recognisable. Either author an environment from the subject's own world, or use a plain gradient environment and do the work with real lights.

## Finishing: material

Two knobs carry almost everything. The rest is detail people reach for before they have got these right.

**Metalness is binary.** In reality a surface either has free electrons or it does not. Values between 0 and 1 are physically meaningless outside of transitions and layered coatings, so ship 0 or 1 and treat anything else as a mistake. Half-metal is the single most common giveaway of a material nobody authored.

**Roughness carries the character**, and the useful range is narrower than it looks:

| Material | Roughness |
|---|---|
| Polished metal, glass | 0.05–0.15 |
| Brushed metal, glazed ceramic | 0.25–0.4 |
| Plastic, painted wood | 0.4–0.6 |
| Paper, unglazed clay, leather | 0.7–0.85 |
| **Fabric, wool, felt** | 0.85–0.98 |

The 3D rut lives at 0.1–0.2 with a clearcoat on everything, which is why generated objects all look like injection-moulded showroom props. **Most real things are rough.** If the subject is cloth, paper, wood, stone or skin, you are above 0.7 and the glossy default is actively wrong.

**A varying roughness map beats a colour texture.** Uniform roughness is what makes a surface look like a computer surface; real materials are polished where they are handled and dull where they are not. Given one texture budget, spend it on roughness and normal maps and leave the colour flat. A flat-coloured object with authored roughness reads as real; a photo-textured object with uniform roughness reads as a decal.

**Fabric needs sheen.** Cloth scatters at grazing angles in a way the standard model gets wrong — that soft halo at the silhouette edge. Most renderers expose `sheen` and `sheenRoughness`; without it, wool looks like painted plastic no matter how high the roughness is. Woven material also has *anisotropy* along the weave direction, which is what makes a textile catch light in bands as it turns.

**Scale the material to the object's real size.** A weave pattern tiled without reference to physical dimensions makes a blanket read as a doll's blanket or a stadium tarpaulin. Set the texture repeat from the object's actual measurements, and state them.

## Finishing: shadow

**The contact shadow is the one that matters.** An object without a dark, tight occlusion where it meets the ground floats, and no amount of lighting fixes it. It is also the cheapest: for a single hero object, a baked shadow plane underneath beats a real-time shadow map on every axis — cost, quality, and control.

**The penumbra is not uniform.** A real shadow is sharp where the object touches and softens with distance from the contact point, because the light source has size. A shadow that is equally blurry along its whole length is the tell that a single blur radius was applied to a silhouette. Renderers expose this as the light's `radius` / area size; use it rather than blurring the map.

**Shadows are never black**, and this is the same rule as the 2D one in `space-and-depth.md`. A shadow is a region lit only by bounce, so it carries the colour of whatever is bouncing — the ground, the wall, the sky. Tint it toward the environment and lift it off zero. Pure black shadow is the absence of a decision, in three dimensions exactly as in two.

**Ambient occlusion is what makes crevices read.** Without it, every recess and seam is lit as brightly as the surface around it and the object looks inflated. Bake it into the model where possible; screen-space AO is a fallback that costs frames and misses exactly the small contacts it is there for.

**Shadow map resolution is a budget, not a quality setting.** One 1024 map on the key light, with the camera frustum tightened around the object, beats 2048 maps on three lights. If the shadow is soft anyway, the resolution matters far less than the tightness of the frustum.

## The finishing checklist

Run it before calling a 3D element done. Each one is a difference you can see.

1. **One sun.** The 3D key and the page's CSS shadows fall the same way.
2. **Key-to-fill is deliberate**, and not 1:1.
3. **Key and fill have opposite temperatures.**
4. **Metalness is 0 or 1.**
5. **Roughness matches the real material** — above 0.7 for anything soft or fibrous.
6. **There is a contact shadow**, tight and dark where the object meets the ground.
7. **No shadow is pure black.**
8. **The environment is not the default studio HDRI.**
9. **Material scale is tied to the object's stated real dimensions.**
10. **The static poster frame** — the one reduced-motion and failed contexts get — looks good on its own. If it does not, the lighting is doing the work the composition should be doing.

## Non-negotiables for anything dimensional

- **`prefers-reduced-motion` gets a static frame**, not a slower spin. Vestibular sensitivity is triggered by the movement itself, and continuous rotation is among the worst offenders.
- **Never gate content behind the canvas.** Text, price, description and actions render in the DOM regardless of whether the 3D ever loads. See the locked-out test in the criterion.
- **Keyboard reach.** If the object is interactive, orbit must be operable from the keyboard or the same information must exist elsewhere. A drag-only control is unreachable for a lot of people.
- **One dimensional element per page.** The loud-once rule applies here with force: two 3D moments is a demo reel, and each halves the other.
- **Test on a mid-range phone with the CPU throttled.** Desktop framerate tells you nothing about the device most people will use.

## Ambient motion

Motion that runs without being triggered — a drifting field, a slow pulse, a looping shimmer. Almost always a mistake, and worth a rule because it is the easiest thing to add and the hardest to remove.

Continuous motion in the reader's periphery competes with the content for attention forever, costs battery for the whole session, and is precisely what reduced-motion exists to suppress. If something must move without input, it should be **slow enough to be doubted** — a cycle measured in tens of seconds, an amplitude the eye can barely resolve — and it should stop when the element leaves the viewport.

The alternative is almost always better: make the motion **respond** to something. Scroll position, pointer proximity, a state change, the passage of real time in the product's own terms. Motion that answers something is craft; motion that runs regardless is a screensaver.
