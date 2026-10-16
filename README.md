# slide-it

**One question per screen, and the answer moving in front of you.**

A Claude skill that turns research, a report, a plan or a decision into a focused page that reads like slides. Each screen answers one question, phrased the way you would search for it, in one or two sentences, with a live scene underneath that you can play with. Every screen goes a level deeper.

<!-- before/after image: plain Claude vs slide-it, same input -->

## Install

**Claude Code** (as a plugin):

```
/plugin marketplace add constantinehuzenko/skills
/plugin install slide-it@constantinehuzenko
```

**Any agent** (with the [skills](https://github.com/vercel-labs/skills) CLI):

```
npx skills@latest add constantinehuzenko/skills --skill slide-it
```

Use one of the two, not both.

Then add this line to your `CLAUDE.md` (`~/.claude/CLAUDE.md` for every project):

```
For any artifact, page or HTML built from content, use the slide-it skill; it works alongside artifact-design.
```

Claude's built-in `artifact-design` skill usually wins the trigger for pages. Without the line, slide-it loaded by itself in 3 of 8 test runs. You can also just say "slide it".

## Use it

> Turn these notes into a page I can share. Slide it.

> Make an artifact from this research.

## What you get

- **4 to 7 screens**, each answering one question the way a reader would ask it.
- **A short answer**, set large: one or two sentences.
- **A live scene** under it, showing the thing itself: customers queueing at a café, air moving in a pair of headphones, a runner on a track. It plays for about ten seconds when the screen comes into view, then rests so you can read. Move the control and it plays again with your setting.
- **A "More" fold** on every screen for the detail, and **full notes with every source** at the end.
- **A look borrowed from the kind of app people use for the subject** (travel, finance, health, developer docs and more), in light and dark.
- **The questions listed at the right edge** on a desktop, tabs on a phone.

## Does it help?

In blind tests, one person picked the better of two pages built from the same input without knowing which was which. Plain Claude (Sonnet) against Claude with slide-it: **7–0 for slide-it** in the first round.
<!-- add the everyday-topics round once tallied -->

It costs more: a slide-it page took 5 to 8 minutes and about three times the tokens of a plain page in our runs.

## Examples

Open them in a browser:

- [How noise cancelling works](skills/slide-it/examples/explainer.html): an explainer
- [Should a café buy a second espresso machine?](skills/slide-it/examples/decision.html): a decision
- [8 weeks to a first 10K](skills/slide-it/examples/plan.html): a plan

## How it works

A short `SKILL.md` in six steps: find the main point, open the nearest example, plan the screens (a question, an answer and a scene line for each), choose the look, build, check. Behind it: the three example pages, a page scaffold, 15 app styles, and an optional isometric drawing kit for when a machine is the subject. It runs no scripts, so it works in claude.ai artifacts as well as Claude Code.

**Not for** slide decks or .pptx files: use the Slides type or the pptx skill.

## Credits

The isometric drawing kit is a browser build of [Anatomy](https://github.com/wheresryan22/anatomy) (MIT). Other ideas and credits are in [THIRD_PARTY.md](skills/slide-it/THIRD_PARTY.md).

MIT licence.
