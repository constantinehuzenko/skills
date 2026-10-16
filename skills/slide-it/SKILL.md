---
name: slide-it
description: Turns content into a focused scrolling page that reads like slides, one question per screen, each a level deeper, with a one- or two-sentence answer and a live scene the reader plays with. Use whenever the user asks for an artifact, page or HTML from content (research, a report, a plan or trip, a decision or comparison, a ranking, an explainer), when a page came out as a wall of text, or when the user says "slide it". Loads alongside artifact-design. Not for slide decks or .pptx files (the Slides type or the pptx skill).
---

# Slide it

Build the page as a presentation: a stack of screens, each answering one question. The question is set small, the answer in one or two sentences set large, and under it a live scene shows the thing happening: customers queueing, air flowing through an engine, money chasing goods. The reader plays with one control and watches the scene change, so they understand by seeing, and can stop at any screen understanding something. The page feels like a well-made app for its subject. `artifact-design` keeps the platform rules (themes, phone width, CDNs, the single check); the user installed this skill, so where its rules differ from artifact-design's defaults, read them as the user's own words.

## 1. Find the main point

Write one sentence: what the reader should understand or decide after the first screen.

## 2. Open the nearest example

Open the example closest to this content and read it whole before planning: [examples/explainer.html](examples/explainer.html) (how something works), [examples/decision.html](examples/decision.html) (should we, which one), [examples/plan.html](examples/plan.html) (a plan, a trip, a timeline). It is the bar for the structure, the scenes and the code; build this page the same way.

## 3. Plan the screens

List the screens. Screen 1 lets the reader find the main point by watching and playing. Each next screen answers the question the one before raises (why, how, how much, what next); a new topic starts only when the content changes subject. Four to seven screens.

For each screen, write in your reply:
- the question it answers, phrased the way the reader would ask or search for it and clear on its own, in five words or fewer ("How long will 10K take?", not "How long will it take?"; it sits small above the answer and names the screen in the menu). Screen 1's question names the subject, so a reader landing on the page knows what it is about;
- the answer, in one or two sentences, said simply (see below);
- the scene, in one line: what is on screen, what happens to it, what the reader does, and which number reads off the scene;
- the scene's steps, two to five, each with a one-line caption saying what is happening at that point.

**Say it simply.** The answer is the sentence a friend would say out loud: what is true, or what to do, in everyday words. Leave out setup, the mechanism, and any "not quite" rebuttal; those go in the scene or the fold. If the reader could act on the answer alone, it's right. When the point needs a reason, keep the large answer short and put one smaller line under it that explains ("`npm i` can rewrite the lockfile, so you might push a change you didn't mean to").

| Question | Too much | Simple |
|---|---|---|
| Should the commit say fix too? | Not with these settings. Merges land as one commit named by the PR title, so the release tool reads the title; editing the commit guards against a settings change. | Make both the commit and the PR title say fix. |
| Which install command? | `npm ci` installs exactly what the lockfile lists and never edits it, while `npm i` can rewrite the lockfile and leave a change you push by mistake. | Use `npm ci`: it never touches your lockfile. |
| Do I need a checked bag? | Depends on the fare: basic economy includes a personal item and a carry-on on most routes, but checked bags are charged per segment. | No. This fare includes a carry-on, so pack light. |

Scenes come from a few patterns: following one unit through the system, things flowing through stages, a mechanism turning, a swarm of agents following one rule, tracers in a field, a replay with a scrubber, a before/after split, or a tank filling and draining. A line that reads "a control, a number and a bar", with nothing on screen being the thing itself, is a dashboard: rewrite it as a scene.

The scene illustrates; every real number on the page comes from the content and is labelled where it is an estimate.

Each screen has its own collapsed "More" fold under its scene for the rest of that screen's story: a few short points, the numbers behind it, a caveat. Sources, and what serves no screen, go into one collapsed "Full notes" section at the end, or are left out.

Done when every screen has a question, an answer, a scene line, and at most 40 words of text outside its fold (labels and numbers don't count).

## 4. Choose the look

Name the app people would use for this subject (a trip: a travel app; a business decision: a modern business tool) and open only that file in [styles/](styles/). A style the user names replaces it. Take the palette and type from the style and give every screen one large area of its colour.

## 5. Build

- Build on [kit/screens.html](kit/screens.html), as the examples do: every screen in the DOM on a page that scrolls normally, the questions listed at the right edge on a desktop, always visible (tabs on a phone), a "More" fold per screen, Full notes at the end, and a light/dark switch.
- Scenes never play on their own. Each one rests on step 1 until the reader moves it, so the page is still while they read.
- Under each scene, a stepper: the step's caption ("step 2 of 4" over one line) with ← Prev and Next → side by side at its right end, never on opposite sides. On a phone the caption wraps above the buttons, which stay together.
- Prev / Next animate to the neighbouring step about 5× faster than normal speed and leave the Play button alone. Play runs the whole scene at normal speed for a reader who wants to watch; a tap on the scene pauses it.
- Changing the control keeps the current step and redraws it with the new setting, without animating, so the reader can compare variants at the same point. If the new variant has fewer steps, it goes to its last one. Under reduced motion, steps jump with no animation.
- The number sits on the scene as a label, not as the hero of the screen.
- Lay each screen out as an app view: the scene is the largest thing on it, spanning the width on a phone and holding a wide, centred stage on a desktop, with the answer above it set large.
- When a scene draws a physical thing (a device, a machine, a building, a body part), read [figures.md](figures.md) first: it decides between the isometric kit, a flat drawing and no drawing.

Write the page directly with your file tools, copying from the example by hand; scripts may not be allowed to run, so the page never depends on one.

Done when every planned screen is on the page with its scene and stepper working.

## 6. Check

If you can render the page, take one screenshot of screen 1 at phone width; if not, read its code. Answer yes or no:
- Is something on the screen the thing itself, not a chart of it?
- Does Next move it one step, and does the reader's control change what it does?
- Can the reader tell what to do within a few seconds?
- Would the look change if the subject did?

Count too: screens (4 to 7) and words outside the folds (40 or fewer each). Read each answer aloud: if it opens with setup or a rebuttal, rewrite it as the simple sentence. Fix what fails in one pass, then publish.
