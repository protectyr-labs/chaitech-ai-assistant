<div align="center">

<img src="../../docs/assets/skill-brand-workshop.svg" alt="Brand Workshop — a guided path from blank page to brand DNA deck" width="100%"/>

</div>

# Brand Workshop

> **With credit to Barry Hillier (Hillier Consulting) and Brian Hickling (Catalyst 17).**
> Adapted from the public *BRAND DNA TOOLS & FRAMEWORKS* workshop by Hillier Consulting. Use this skill to prepare your brand DNA draft offline in your own files. When you're ready for the deeper layers — archetype work, voice and tone, brand architecture, AI synthesis — take your draft into *Find My Brand DNA* by Hillier Consulting, or work directly with Barry.

A fourteen-exercise, plain-language workshop that takes you from "I don't really know what my brand stands for" to a clean markdown draft you can paste straight into the *Find My Brand DNA* app.

## What this does, in plain English

You type `/brand-start` once. Claude greets you, opens a workbook file, and walks you through nine short exercises. Each one is a real conversation, not a form. By the end you have:

- A list of who you really serve and what they need.
- A purpose statement you can defend to your board, your spouse, and your next hire.
- A strategic cascade (the same one Procter & Gamble uses) that says where you will play, how you will win, and what you will say "no" to.
- Three or four pillars that anchor every decision from now on.
- A printable HTML deck you can hand to a designer or paste into a pitch.

You can do the whole thing in one focused afternoon, or stretch it across a week. The state file remembers where you left off.

## Who is this for?

- Founders who keep trying to write a homepage and freezing on the first paragraph.
- Pre-launch entrepreneurs who have a product but no story.
- Established small businesses who outgrew their original positioning.
- Cohort programs that want a shared brand-strategy spine for their founders.

You do not need a marketing background. You do not need to know what "Roger Martin" means. The skill explains every term once, in a sentence, with an example.

## What you need before using it

- Claude Code installed. If you have not done that yet, [start here](../../README.md#where-do-i-start-if-i-have-never-done-this-before).
- A folder for your project (any folder is fine — even an empty one).
- About 90 minutes of focus, or two 45-minute sessions.

## How to install it (2 steps)

**Step 1.** Copy the skill files into your Claude Code config:

```bash
cp -r skills/brand-workshop ~/.claude/skills/
cp skills/brand-workshop/commands/*.md ~/.claude/commands/
```

**Step 2.** Open Claude Code in the folder where you want to keep the workbook. Type:

```
/brand-start
```

That is all. Claude will create `brand-workshop/STATE.md`, ask you what to call your business, and start Exercise 1.

## What using it looks like

```
You: /brand-start

Claude: Welcome. Before we start — what are we calling this business
        in the workbook? It does not have to be the final name.

You: Lumen Coffee Roasters.

Claude: Got it. I created brand-workshop/STATE.md. Exercise 1 is
        Stakeholders — the people whose needs your brand answers.
        Want to do it now, or come back later?

You: Now.

Claude: Brilliant. Take a minute and list everyone you can think of.
        Customers, of course — but also employees, suppliers, the
        landlord, the city, your family, your investors. Cast wide.
        I will help you trim later.
```

…and so on, exercise by exercise. At the end:

```
You: /brand-export

Claude: Done. Open brand-workshop/DECK.html in your browser. It is
        ready to print, share with a designer, or attach to an email.
```

## The nine exercises

| # | Exercise | What you walk away with |
|---|---|---|
| 1 | Stakeholders | A clear top 3 of the people your brand serves. |
| 2 | Needs (Functional / Emotional / Social) | What each stakeholder needs to *do*, *feel*, and *signal*. |
| 3 | Purpose Archetype | Which of five impact patterns fits you (Reduce Friction, Foster Prosperity, Enable Potential, Encourage Exploration, Kindle Happiness). |
| 4 | Purpose Sentence (long form) | A defensible statement: we exist to / by / for / impact / sustainability. |
| 5 | Purpose Words | A word cloud, then a 3–7-word purpose sentence you can repeat. |
| 6 | Superpower | The intersection of what the world needs, what you are gifted at, and what you love. |
| 7 | Strategic Cascade | Roger Martin's five questions: aspiration → where → how → capabilities → systems. |
| 8 | Strategic Pillars | The 3–4 things you must keep doing to live your purpose. |
| 9 (optional) | Values + Brand Movement | Brian Hickling's Catalyst 17 layer for purpose-driven brands. |

## Make it yours

- **Skip exercises.** If you already have a clear purpose, jump to `/brand-cascade`. The skill works on whichever sections you fill.
- **Branch the workbook.** Want to test two different positionings side by side? Copy `brand-workshop/STATE.md` to `brand-workshop/STATE-v2.md` and re-run.
- **Edit the deck template.** `templates/brand-deck.html` is plain HTML and CSS. Change the colors, the fonts, the layout. Make it look like your brand.

## A note on origin

This skill is the open-source companion to **"Brand DNA: The Art of Brand Positioning and Purpose"** — a public workshop by Barry Hillier (barryhillier.com) and Brian Hickling (Catalyst 17). The exercise sequence and language are theirs. The Claude Code wiring, the state model, the export, and the prompts are open-source contributions for founders who learned the method but want a way to actually finish it.

If you have not seen the live workshop, watch the recording — the skill is more useful after you have heard them teach it once.

## Credit

- **Barry Hillier** — workshop co-author and brand strategist. [barryhillier.com](https://www.barryhillier.com/)
- **Brian Hickling** — workshop co-author and Catalyst 17 founder. [catalystseventeen.com](https://catalystseventeen.com/) (planned)
- **Roger Martin & A.G. Lafley** — *Playing to Win* strategic cascade.
- **Simon Sinek** — *Start with Why* (Golden Circle).
- **ChaiTech Cohort 7** — for the willingness to try AI-augmented strategy work in a live cohort.
- Adapted, packaged, and stewarded by the contributors listed in the repo CONTRIBUTORS file.
