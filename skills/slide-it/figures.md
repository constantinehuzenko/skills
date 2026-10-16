# Figures: draw the thing as itself

Read this before drawing anything. It decides whether a screen gets the isometric kit, a flat drawing or no drawing.

## 1. Decide

**A drawing must earn its build time.** Draw only when watching the thing work explains it better than a chart or a sentence. Keep it a small share of the build: a few minutes, 15–30 parts, 40 at most. If it can't be done in that, use the simpler visual and offer the full drawing as a follow-up.

| Subject | Draw it as |
|---|---|
| A machine, vehicle, building or device whose inside or mechanism is the subject (a jet engine, a lock, a gearbox) | Isometric solids from the kit (sections 2–8), 15–30 parts, with a live readout |
| A process between devices or people (a message going phone → server → phone, a payment, a delivery) | Flat inline-SVG drawings that look like the real things: a phone with its rounded body and screen, a server rack with slots and status lights. One stroke weight, colours from the tokens, and the thing that travels (a dot, an envelope) moving between them. Not the kit |
| An organic thing (a body part, plant, animal, food) | A flat side view or cross-section: a few closed SVG paths for the outline, the moving part as its own `<g>` driven by the control, one accent on the part that matters, labelled "schematic, not to scale". The readout (degrees, millimetres) and the interaction carry the idea |
| An idea with no object (money, time, a decision) | No figure: a live scene of simple actors instead (money as dots, customers as dots, a jar that fills), as in the examples |
| Real 3D (three.js, pinned from cdnjs) | Only when the user asks for 3D ("3D", "rotate", "orbit"), and never for an organic subject |

A drawn thing is the screen's interaction: one control moves its parts, a readout reports them, and the screen's sentence can be seen in it. Images from other sites can't load in an artifact, so there are no photos; draw instead.

## 2. The isometric kit

Function names below are Anatomy's, exposed as `window.Iso` by `kit/figures/iso-kit.js` (CSS: `kit/figures/iso.css`; working page: `kit/figure-iso.html`). `kit/figures/README.md` lists what exists; where this file and that list disagree, the list wins. Call nothing that is not listed there.

## 3. Size first

Inside an artifact build, draw a **Figure**: 15–30 parts by default, 40 at most, built in a few minutes and written straight into the page with no build script. The kit's functions write the SVG when the page loads. The figure stays a small share of the whole build; if it is growing past that, stop and fall back to the simpler visual (section 1).
- 15 parts is the floor. Even a small figure is a real machine: a base on feet, a frame or rail, the mechanism, one control, one scale, a few screws. Put the detail on the subject and the mechanism first; plain edges are fine. If the idea can't be a real object at 15 parts, it fails the gate: use a chart or a flat diagram.
- Anatomy's larger sizes are **Hero** (80–150 parts, several layers, hours) and **Epic** (a whole vehicle or plant, many hours). Do not start either. After delivering, offer one line: "Want this at Hero detail? That is an hours-long job done with the Anatomy skill itself (`npx skills add wheresryan22/anatomy`)."

## 4. Invent the object

Before any geometry, write one sentence: **what moves, and what the reader learns from it.** Pick a machine, tool, instrument or piece of furniture whose mechanism maps one to one onto the concept. Never trace a reference image.

| Concept | Object (invented examples) | What moves, what it teaches |
|---|---|---|
| A token bucket rate limit | A water tank with a tap and a float | The tap refills at a fixed rate; a burst empties the tank and the next request waits |
| A cache that skips work | A lock and key | A key that matches every pin turns the plug and no work is redone; a worn key fails |
| How a jaw opens | Hinged solids: condyle in its socket, the disc between, muscles as bands | Opening slides the condyle forward over the disc; the bands shorten; past the range the disc strains |
| A message crossing a network | Two phones, a server cabinet, cables between them | A packet rides the cable; with the receiver offline it waits in a tray at the server |

Two failures to avoid:
- **Too abstract:** floating plates, labelled boxes and arrows. Layers become drawers, trays in a rack, plates on pillars or cards in a holder.
- **Too flat:** one big slab with a few lines. A phone is a rounded body with a bezel, a screen plane showing its own tiny bubble lines, a camera dot and a home bar; never a text box. A server is a cabinet with drawer fronts, pulls, ports and LEDs.

## 5. Workflow

Work in this order. Most of the quality is decided in steps 1 to 3.

1. **Truth first.** Put the real numbers into a small model: sizes, counts, thresholds, curves. One function maps the control's value to every part's target and to the readout string. Done when one value produces both, and nothing on screen is typed in by hand.
2. **Parts list.** 15–30 parts (40 max), grouped: base (plate, feet, groove, screws), structure (posts, rails, frame), mechanism (carriage, spring, plunger, needle), controls (knob, slot), the subject. Each part rests on another part. Name the subject: it becomes the lit part. Done when the list is written and every part has a job.
3. **Camera.** `P = Iso.fitProjection(points, W, H, { pad: 24–34, azimuth, elevation })`. Feed it every extreme point: `boxCorners(plan, z0, z1)` for each plan, the tallest tip, and each moving part at both ends of its travel. Azimuth 45 and elevation 30 by default; 35–60 to turn the mechanism's long side toward the viewer; higher elevation to look into something open. Use a viewBox near 4:3 (about 480×360) so it reads at phone width. World units are about 1 px, x and y on the floor, z up. Plans are `{ x, y, w, d, r }`. Done when nothing clips at either end of the control and the figure fills 55–65% of the card.
4. **Build geometry once.** Static parts are built once from `slabOf`, `cylinder`, `extrude`, `roundedPlan`, `insetPlan`, `topTicks`, `radialTicks` and painted with `solidSvg`, `lineSvg`, `wireSvg`, `dotsSvg`, `fadeLineSvg`. Moving parts are built at rest and moved with a transform (`translateAlong`). Only parts that change shape (a needle, a compressing spring) are rebuilt per frame. Done when the page draws at load and a frame costs well under a millisecond of script.
5. **Paint back to front.** Base first, then what rests on it. Within a level sort by `Iso.depthOf(centre, P)` ascending, far to near. Split anything that wraps another part (a spring round a rod, a frame round a carriage) into back half, inner part, front half. Draw a moving part in its own slot inside a `<g>` that moves; if it would pass in front of and behind the same neighbour, split the neighbour or limit the travel. Done when the nearer part covers the farther one at both ends of travel and nothing is sunk into another part (contacts are flush or tangent).
6. **Frame the plate.** A square-cornered card with a 1 px rule: `Fig n` top left, a short title top right, the interaction hint bottom left, the live readout bottom right. Legend keys and a true caption go below the card. Done when the card carries all four corners and the drawing carries at most one small engraved label.
7. **Make it live.** One control sets a target, and every part eases toward it. The control is a real `<input type="range">` or a row of buttons next to the plate (keyboard, screen reader and touch come free); dragging the figure itself is a bonus that sets the same value, with `touch-action: pan-y`. One `requestAnimationFrame` loop, `dt` clamped to 1/30 s, writing attributes on refs (`setAttribute("transform" | "d")`, `textContent`), never re-rendering. It stops when everything has settled or the figure is offscreen (IntersectionObserver, read the last entry). Done when dragging never snaps a part and the loop idles at rest.
8. **Accessibility.** The `<svg>` is `role="img"` with an `aria-label` saying what the object is and what it shows. The control is labelled and has `aria-valuetext` in words ("Open 24 mm, disc forward"), written when the reader's choice changes, never per frame. One visually hidden `aria-live="polite"` region gets phase changes only ("sent", "at server", "delivered"). Keys: arrows step, Shift steps bigger, Home and End go to the extremes, Space or Enter toggles. Keep a visible focus ring. Done when the figure works with the keyboard alone.
9. **Reduced motion = a still frame.** Read `matchMedia("(prefers-reduced-motion: reduce)")` each tick and pass it as `calm` to `Iso.follow` and `Iso.settle`, so parts jump to their targets. No tour, no flow dashes, no bursts. The figure still answers input, and the frame at rest already shows the subject lit and the readout complete.
10. **Check once.** Both themes, at 360 px and desktop. Every line ends on a face, another line or a dot. Exactly one part is lit. Both ends of the control look right, and one reachable end shows the bad state (overflow, strain, a jammed lock, a packet waiting). The readout matches where the parts are now. Zoom to 2×: a bare face next to the subject needs the real part that is missing. If you can render the page, screenshot it; if you cannot, say it was not looked at.

Skeleton, in the order the page script runs:

```js
const model = (v) => ({ open: 8 + 32 * v, say: `open ${(8 + 32 * v).toFixed(0)} mm` });   // step 1
const P = Iso.fitProjection(extremes, 480, 360, { pad: 28, azimuth: 45 });               // step 3
const still = parts.map(([paint, plan, z, h]) => paint(Iso.slabOf(plan, z, h, P, 6, 1)));  // step 4, sorted by depthOf
let x = 0, target = 0.5;                                                                  // step 7
function tick(dt, calm) {
  x = Iso.follow(x, target, dt, 0.28, calm);          // exponential ease, tau 0.1–0.3 s
  jaw.setAttribute("transform", Iso.translateAlong(P, [0, 0, model(x).open]));
  readout.textContent = model(x).say;                 // read from where the parts are, not the target
}
```

## 6. Craft rules

1. **A real object, not boxes and arrows.** The reader should name it at a glance.
2. **Everything is held.** Every solid rests on another and traces back to the base. A heavy base on feet, parts meeting flush or tangent. A part sunk into another is a bug.
3. **Density from structure, not texture.** Feet, rails, stops, bushings, knobs, screws, a label plate. Never one plain slab; never scattered noise.
4. **Volume.** Build with `slabOf`, `cylinder` and `extrude` so each part gets four side tones by facing and a lighter top. Bevel 0.4–1.6. Use flat shapes only for inlays under 1 unit thick.
5. **Exactly one lit part**, the one to watch (the subject, or the part the reader selected). It is the only part drawn in the lit tone.
6. **Tone hierarchy.** Base and feet `lo`; structure `mid`; the subject `hi`; grooves and inset outlines `faint`; minor ticks `lo`, major ticks `mid`, the zero mark and pointers `hi`; screws as 0.4–0.55 dots.
7. **Colour comes from the page's tokens.** `iso.css` maps the tones onto slide-it's tokens, so the figure takes the genre's palette and both themes. Keep it monochrome plus the one lit accent; use `--bad` or `--good` only for a state, never for decoration. Paper fills equal the card colour, so a nearer part hides a farther one with no patches.
8. **Lines resolve.** Every line ends on a face, another line or a terminal dot. Connectors are `wireSvg` with dots that land on objects. No leader lines, balloons, dimension arrows, dashed hidden edges or floating labels. Fills hide what is behind them: no see-through wireframes.
9. **Textures end on an edge or fade out.** Ticks hang from a ruler strip's edge; a seam wraps a box's visible corners; a line that must stop mid-face uses `fadeLineSvg`. Printed-text rule lines on a label plate are the one exception.
10. **Text around the figure, not on it.** Corner labels, legend and caption carry the words, with at most one small engraved label (`faceTextSvg`). Text a device itself displays (a phone screen, a gauge) belongs to the object: keep it at the screen's own size, clip it to the window, and fit the longest string.
11. **A soft halo under the base** (`haloOf`) and under anything lifted. No other shadows or glows.
12. **Thin, constant strokes.** 0.6–1 px, non-scaling, so lines keep their weight when the SVG scales.
13. **Parts ease toward targets.** `Iso.follow` with tau 0.1–0.3 s; a real spring only where the object is springy; `Iso.settle` for values that must not overshoot (a hue, a level); `Iso.burst` for one-off events (a click, a pulse). Never snap a part to the pointer.
14. **Flow dashes for things that travel** (`lineSvg(..., { flow: true })`): a packet, water, current. Turn them on only while something is travelling and off at rest; at rest the page has no ambient loops.
15. **A tour runs once**, when the figure first scrolls into view, to show the point; offer Replay. No endless loop. Touching the control stops it.
16. **The readout is true and short.** Real units, tabular numbers, from the same model and the same instant as the parts: `open 24 mm · disc forward`. Pair a phase word only with a number read at the same moment.
17. **Composition.** Centre the figure, 55–65% of the card, air around it, clear of the corner labels. If parts are too small at 360 px, tighten the camera or stretch the SVG to 110–118% inside a card with `overflow: hidden`.
18. **Phone first.** Hit areas are generous, the control is at least 44 px tall, the hint line says what to do ("Drag the jaw open"), and the figure looks interactive at rest.

## 7. The figure on the page

- **Its screen:** the plate (figure, hint, readout), the screen's sentence, and the control. Cover the sentence: the figure and its readout should still show the point.
- **Long reads.** The figure stays the same size however long the source is; the depth lives on later screens and in "Full notes". Keep it to one figure at its planned part count.
- **Tap a part, open its card.** Parts and 3–6 numbered legend buttons both select; the legend is the keyboard and screen-reader path, so use real `<button>`s. Selecting takes the lit tone and steps the other parts down one tone; the card shows the part's number as a bar or a zoomed piece first, then its name and one line on what it does, within the screen's 40 words.
- **Full notes:** the real names, measurements, what the model leaves out, and sources.
- The figure's corner labels and legend count as labels, not running text.

## 8. Using the kit

- Paste `kit/figures/iso.css` into the page's `<style>` after the token block, and `kit/figures/iso-kit.js` into one `<script>`, keeping its licence header. Everything is inline, with no CDN. Start from `kit/figure-iso.html`: copy its structure (model, geometry, paint, live) and replace the content.
- Wrap the figure in an element with the kit's class so the tone variables apply; the theme toggle already flips them.
- Write the plate's markup once, then fill the drawing from the script. Do not leave geometry as hand-typed path strings.

## Credit

The figure style and kit are **Anatomy** by Ryan (wheresryan22/anatomy, https://github.com/wheresryan22/anatomy), MIT licence, Copyright (c) 2026 Ryan. The kit is ported into `kit/figures/` with its licence notice kept; the Figure/Hero/Epic sizes, the tone hierarchy and the craft rules above are adapted from it in our own words. The line-figure option follows the ideas of Hairline by Lucas Marques (MIT); no Hairline code is used. See `THIRD_PARTY.md`.
