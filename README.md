# slide-it

**One question per screen, and a drawing that changes as you press Next.**

A Claude skill that turns an explanation, a decision, a report or a pull request into a focused page. Each screen answers one question with a short sentence and a drawn scene: the things themselves (servers, pipes, phones with their real screens), side by side when two options are compared. Next and Back step through it, and each step changes one thing.

On [skills.sh](https://skills.sh/constantinehuzenko/skills/slide-it).

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

Use one of the two, not both. To update later, run the same command again (for the plugin, `/plugin marketplace update constantinehuzenko` first).

Then add this line to your `CLAUDE.md` (`~/.claude/CLAUDE.md` for every project):

```
For any artifact, page or HTML built from content, use the slide-it skill; it works alongside artifact-design.
```

Claude's built-in `artifact-design` skill usually wins the trigger for pages. You can also just say "slide it".

## Use it

> Make an artifact that helps me understand this pull request. Slide it.

> Should we use WebSockets or SSE? Slide it.

## What you get

- **Screens, one question each**, listed in a menu at the right edge on a desktop.
- **A short answer** under each question.
- **A drawn scene** that changes step by step: press Next and one thing moves or changes. Reset starts it over.
- **One card for the current step**, a short sentence whose key words carry the colour of the part they name, so the words point at the picture.
- **Folds** for detail and code, light and dark themes, and keyboard shortcuts.

## Examples

Open them in a browser:

- [WebSockets or SSE for live scores?](examples/websockets-or-sse.html). Two lanes, SSE and a WebSocket, each with a server, its pipe and a phone. A goal goes down both; a cheer comes back up only one.
- [List virtualization](examples/list-virtualization.html). Why a long list downloads every image, and how virtualizing it against a scrolling panel fixes it. A product list sits beside a grid of every row in the DOM, rulers show where each list starts, and the last screen has before and after numbers.

## How it works

`kit/template.html` is the engine: screens, menu, stepping, the step card, themes, and a red box that names any mistake. Claude fills three blocks (a theme, the page's text and the scenes) and leaves the engine alone. `SKILL.md` points it at one finished example as the bar to match. It runs no scripts, so it works in claude.ai artifacts as well as Claude Code.

**Not for** slide decks or .pptx files: use the Slides type or the pptx skill.

## Credits

Icons from Lucide (ISC) and Feather (MIT); details and licences in [THIRD_PARTY.md](skills/slide-it/THIRD_PARTY.md).

MIT licence.
