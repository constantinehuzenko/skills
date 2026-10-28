---
name: slide-it
description: For a page or artifact that explains or answers something, such as a pull request or its review comments, a technical decision, how a system works, a report, a plan or a money question. The page scrolls through screens, one question each, with a menu of the questions; on each screen a drawn scene changes step by step. Also for a page that came out as a wall of text, or "slide it". Slide decks and .pptx go to the Slides type or the pptx skill.
---

# Slide it

`kit/template.html` is the page's engine. `examples/live-scores.html` is the bar: one finished screen, "WebSockets or SSE for live scores?". Read the example whole before you write anything, and make your page the way it is made:

- The things themselves, drawn: servers, pipes, phones with their real screens. Side by side when you compare.
- One colour per thing, and the same colour on its word in the step text: `[[SSE|chart-1]]`.
- Next and Back move through steps; each step changes one thing, and its text is one short sentence.
- A new screen only when one would get too complicated.

1. Copy `kit/template.html` to the working file with `cp`. Never retype or edit the engine. Read only its three FILL blocks (`grep -n FILL` gives their lines).
2. Replace each FILL block's sample with your own: THEME, PAGE and SCENES. Each block's comment gives its shape; the example shows them filled.
3. Open the page wrapped as the template's first comment says, and fix whatever a red box names.
4. Save or publish it.
