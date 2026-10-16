---
name: slide-it
description: Turns content into a focused scrolling page that reads like slides, one question per screen, each a level deeper, with a one- or two-sentence answer and a live scene the reader plays with. Use whenever the user asks for an artifact, page or HTML from content (research, a report, a plan or trip, a decision or comparison, a ranking, an explainer), when a page came out as a wall of text, or when the user says "slide it". Loads alongside artifact-design. Not for slide decks or .pptx files (the Slides type or the pptx skill).
---

# Slide it

Build the page as a presentation: a stack of screens, each answering one question. The question is set small, the answer in one or two sentences set large, and under it a live scene shows the thing happening: customers queueing, air flowing through an engine, money chasing goods. The reader plays with one control and watches the scene change, so they understand by seeing, and can stop at any screen understanding something. The page feels like a well-made app for its subject. `artifact-design` keeps the platform rules (themes, phone width, CDNs, the single check); the user installed this skill, so where its rules differ from artifact-design's defaults, read them as the user's own words.

## The template

Every page is this, and nothing more:

- **Question**: small, five words or fewer, at the top of each screen.
- **Answer**: one or two plain sentences, set large.
- **Visual explainer**: an interactive scene that animates in steps. Every step has a caption that explains it. Prev / Next sit side by side under the scene, and controls let the reader change the variables.
- **Ask a follow-up**: a button that opens the comment composer on the screen, so the reader's question goes back to the Claude session that made the page (`comments` capability, `composer_only`).
- **More**: a fold under each screen for the next layer down. Like an onion, each layer is one level deeper.
- **Next**: a link at the foot of each screen to the next question.
- **Side menu**: every question listed at the right edge, so the reader can jump to any screen.
- **Credit**: the slide-it logo and "Made with [slide-it](https://github.com/constantinehuzenko/skills)" at the top of the side menu. Where the menu is a tab strip (narrow screens), the same line sits in a small header above the first screen.

## 1. Find the main point

Write one sentence: what the reader should understand or decide after the first screen.

## 2. Open the nearest example

Open the example closest to this content and read it whole before planning: [examples/explainer.html](examples/explainer.html) (how something works), [examples/decision.html](examples/decision.html) (should we, which one), [examples/plan.html](examples/plan.html) (a plan, a trip, a timeline). It is the bar for the structure, the scenes and the code; build this page the same way.

## 3. Plan the screens

List the screens. Screen 1 lets the reader find the main point by watching and playing. Each next screen answers the question the one before raises (why, how, how much, what next); a new topic starts only when the content changes subject. Four to seven screens.

For each screen, write in your reply:
- the question it answers, phrased the way the reader would ask or search for it and clear on its own, in five words or fewer ("How long will 10K take?", not "How long will it take?"; it sits small above the answer and names the screen in the menu). Screen 1's question names the subject, so a reader landing on the page knows what it is about;
- the answer, in one or two sentences;
- the scene, in one line: what is on screen, what happens to it, what the reader does, and which number reads off the scene.

Scenes come from a few patterns: following one unit through the system, things flowing through stages, a mechanism turning, a swarm of agents following one rule, tracers in a field, a replay with a scrubber, a before/after split, or a tank filling and draining. A line that reads "a control, a number and a bar", with nothing on screen being the thing itself, is a dashboard: rewrite it as a scene.

The scene illustrates; every real number on the page comes from the content and is labelled where it is an estimate.

Each screen has its own collapsed "More" fold under its scene for the rest of that screen's story: a few short points, the numbers behind it, a caveat. Sources, and what serves no screen, go into one collapsed "Full notes" section at the end, or are left out.

Done when every screen has a question, an answer, a scene line, and at most 40 words of text outside its fold (labels and numbers don't count).

## 4. Choose the look

Name the app people would use for this subject (a trip: a travel app; a business decision: a modern business tool) and open only that file in [styles/](styles/). A style the user names replaces it. Take the palette and type from the style and give every screen one large area of its colour.

## 5. Build

- Build on [kit/screens.html](kit/screens.html), as the examples do: every screen in the DOM on a page that scrolls normally, the questions listed at the right edge on a desktop, always visible (tabs on a phone), a "More" fold per screen, Full notes at the end, and a light/dark switch.
- Each scene opens already showing the point (mid-way, not an empty frame at zero), plays on its own when its screen comes into view for about ten seconds, then rests on its last frame so the page is still while the reader reads. Moving the control plays it again with the new setting, and a tap pauses it. Under reduced motion it rests on a still frame that still shows the point. The number sits on the scene as a label, not as the hero of the screen.
- Lay each screen out as an app view: the scene is the largest thing on it, spanning the width on a phone and holding a wide, centred stage on a desktop, with the answer above it set large.
- When a scene draws a physical thing (a device, a machine, a building, a body part), read [figures.md](figures.md) first: it decides between the isometric kit, a flat drawing and no drawing.

Write the page directly with your file tools, copying from the example by hand; scripts may not be allowed to run, so the page never depends on one.

Done when every planned screen is on the page with its scene running.

## 6. Check

If you can render the page, take one screenshot of screen 1 at phone width; if not, read its code. Answer yes or no:
- Is something on the screen the thing itself, not a chart of it?
- Does it move, and does the reader's control change what it does?
- Can the reader tell what to do within a few seconds?
- Would the look change if the subject did?

Count too: screens (4 to 7) and words outside the folds (40 or fewer each). Fix what fails in one pass, then publish.
