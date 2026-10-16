# slide-it kit / figures

Isometric figures drawn in Anatomy's style, inside a single-file HTML artifact: no build step, no Node. `iso-kit.js` defines `window.Iso` (pure functions that return SVG path strings and markup); `iso.css` styles it from the page's tokens (`--bg --surface --fg --muted --line --accent --bad --good`, `color-scheme` set per theme, as in `../TOKENS.md`), so a figure takes the genre colours and light/dark with no extra code. The lit part is the accent. `../figure-iso.html` is a worked example (phone, server rack, phone, a packet that travels between them), runnable on its own.

**Paste into a page:** (1) the token block (`../theme-toggle.html`), (2) `iso.css` in a `<style>`, (3) `iso-kit.js` in a `<script>`, (4) your own figure script: build a projection `P = Iso.fitProjection(pts, W, H, {pad})`, build solids, join them back to front, then `el.innerHTML = Iso.plateHtml({fig, title, hint, readout, body: Iso.figureSvg({width: W, height: H, label, body})})`. Keep the licence comments in the first two files. A live figure moves groups with `translateAlong`, toggles `data-lit` on a `.iso-solid`, and writes `[data-readout]`.

The 12 most useful (world coordinates `[x, y, z]`, z up; `plan = {x, y, w, d, r}` is a rounded rectangle on the floor):
- `fitProjection(points, w, h, {pad, azimuth, elevation})`: a projection `P` that centres and fits the extreme points in the viewBox (default 45° / 30°).
- `slabOf(plan, z, h, P, steps, bevel)` / `cylinder(cx, cy, r, z, h, P, steps, bevel)`: the two workhorse solids, returned as `{fill, outline, crease, top, shades}` paths.
- `extrude(ring, z, h, P, {convex: false})`: any floor outline, e.g. an L-shaped cable duct.
- `solidSvg(paths, {tone, crease, halo, lit, inner})`: paints a solid in four tones; tone `hi` for the subject, `mid` structure, `lo` base, `faint` grooves; `lit` for the one part to watch.
- `depthOf(point, P)`: bigger is nearer; sort ascending to paint back to front.
- `onTop(points, z, P)` / `planOutline(plan, z, P)` / `lineOnTop(a, b, z, P)`: lines on a horizontal face (screens, grooves, bubbles).
- `sideSeam(plan, z, P, steps)`: a seam that wraps a box's visible corners (pass it as `inner`; never inset a line from the corners).
- `sideRing(center, r, "x" | "y", P)`: a circle on a vertical face: a port, a lens.
- `wireSvg(from, to, {via, tone, dotted, flow, ends})`: a connector with end dots; `flow` animates dashes (wrap points with `pointsAt`).
- `topTicks(from, to, step, every, edge, z, [minor, major], P)` / `radialTicks(...)`: ruler and dial ticks, rooted on an edge.
- `translateAlong(P, [dx, dy, dz])`: a `translate(...)` string that moves a pre-built group by a world offset.
- `plateHtml({fig, title, hint, readout, keys, caption, body})`: the card with its four corner slots; also `haloOf`, `dotsSvg`, `insetPlan`, `faceTextSvg`, `figureSvg`.
Motion helpers on `Iso`: `follow(x, target, dt, tau, calm)` (exponential), `settle(state, target, dt, seconds, calm)` (critically damped), `burst(age, rise, fall)` (one-shot envelope), `smooth(a, b, x)`.

**Craft rules (Anatomy's):** draw a real object you could build, 15–30 parts (40 at most), each resting on another; thin lines, one lit part; every line lands on something (plugs, edges, rings, not floating ends); at most one tiny label on the object, all other text in the plate corners, caption or the page; ease everything (tau 0.1-0.3 s), stop the loop when settled or offscreen, write phases to an `aria-live` line and numbers only to the readout; `prefers-reduced-motion` gives a still frame.

**Dropped from the port:** `ISO_CSS` and `pageHtml` (the stylesheet and document builder for Node; `figureSvg({standalone})` now sets its class and theme but embeds no style) and the `.tb-*` tube styles (the tube module is not ported). Nothing in the kit needed Node. Built from `iso-kit.ts` with esbuild (`--format=iife --global-name=Iso --target=es2019 --minify`) after cutting that tail and appending the motion helpers.

Credit: [Anatomy](https://github.com/wheresryan22/anatomy) by Ryan, MIT, Copyright (c) 2026 Ryan (`kit/iso-kit.ts`, `kit/iso.css`, `kit/gl.mjs`, `references/craft.md`); the full notice is at the top of `iso-kit.js` and `iso.css`.
