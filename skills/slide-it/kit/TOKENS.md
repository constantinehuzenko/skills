# Shared token contract (every kit snippet, style and example uses these names)

Colour (light values on bare :root; dark under `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) {…} }` AND `:root[data-theme="dark"] {…}`; `color-scheme` set in each):
--bg (page ground) · --surface (raised/selected area) · --fg (text) · --muted (secondary text) · --line (rules, borders) · --accent · --accent-fg (text on accent) · --good · --warn · --bad
Optional, set by most genres: --accent-2 (a second voice; fills, not text, unless its contrast passes) · --tint (a large wash of the genre colour behind the first screen)

Type: --font-display · --font-body · --font-mono (each with a real fallback stack)
Shape: --radius (a style may set 0)
Motion: --dur-fast: 150ms (feedback) · --dur: 240ms (routine) · --dur-slow: 420ms (layout, overlays) · --ease-out: cubic-bezier(0.16, 1, 0.3, 1) · --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1)

Theme toggle: sets `data-theme` on <html> to "light" | "dark", saved in localStorage key `si.theme` (every read/write in try/catch); with nothing saved the page follows the system.
Reduced motion: under `@media (prefers-reduced-motion: reduce)` movement goes to 0ms but opacity/colour/state changes stay.
