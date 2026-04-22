<div align="center">

<img src="../../docs/assets/skill-executive-team.svg" alt="Eight friendly advisors around a table" width="100%"/>

</div>

# Eight friendly advisors

> A full executive team for your one-person (or two-person) business. They remember your numbers. They speak in character. They argue when you need them to.

## What this does, in plain English

You get eight AI advisors. Each one has a role (CEO, Chief Revenue Officer, Chief Marketing Officer, Chief Product Officer, Chief Operations Officer, Chief Financial Officer, Head of Customer Success, Chief Innovation Officer) and each one keeps a little file on your business that you fill in yourself.

When you ask a question, the right advisor answers. The Chief Revenue Officer will not give you generic pricing advice; it will open its notes, see your actual pipeline and customer concentration, and answer based on that. If you want a decision, you can ask two advisors to argue and the CEO will mediate.

## Who is this for?

- Solo founders who wish they had a leadership team.
- Two-person businesses where you are already wearing every hat.
- Anyone who wants AI advice grounded in their real numbers instead of a generic article.

## What you need before using it

- Claude Code installed. (If you have not done this yet, see [the main page](../../README.md#where-do-i-start-if-i-have-never-done-this-before).)
- About 30 minutes to fill in the starter notes for each advisor. You can do it one advisor at a time.

## How to install it (2 steps)

**Step 1.** Copy the helper into your Claude Code folder:

```bash
cp -r skills/executive-team-template/agents ~/.claude/agents/
cp -r skills/executive-team-template/state /your/project/ops/personas/
```

(Replace `/your/project/` with the folder your business lives in.)

**Step 2.** Open each file inside `state/` and fill in the starter template with your real numbers. Start with `BUSINESS_CONTEXT.md` and `CAPACITY.md`. You can come back and fill the rest later.

## What using it looks like

After you have filled in a little bit about your pipeline, ask:

> Ask the CRO if now is a good time to raise my prices.

The CRO opens its notes, sees that you have four active deals with two at late stage quoted at current pricing, and answers:

> Not this quarter. The two late-stage deals were quoted at your current numbers, and a mid-cycle price change gives them a reason to renegotiate. Revisit after those close in May.

That is a real answer, not a generic one, because the advisor read its own file before speaking.

## What each advisor does

| Advisor | What they worry about |
|---|---|
| CEO / Chief of Staff | Keeping everything focused. Arbitrates when advisors disagree. |
| CRO (Revenue) | Your pipeline, deals, and customer relationships. |
| CMO (Marketing) | Who your audience is, what you say to them, where you say it. |
| CPO (Product) | What you build next. What you should stop building. |
| COO (Operations) | Delivery, quality, and whether you have the capacity to do more. |
| CFO (Finance) | Pricing, margins, cash flow, and whether you can afford this hire. |
| Head of Customer Success | Keeping the customers you have happy. Proof and testimonials. |
| CINO (Innovation) | New opportunities. What the market is telling you. |

## Make it yours

- **Fewer advisors is fine.** Most solo founders start with three (CEO, CFO, and one other). Delete the rest and come back to them later.
- **Different roles.** Swap CRO for Head of Growth, or add a General Counsel. Copy the pattern from an existing file.
- **Different voice.** The advisors are polite and measured by default. If you want a blunter CRO, edit the top of `agents/cro.md`. They will still read the notes; they will just sound different.

## Credit

Adapted from a private solo-founder operating system used at Protectyr Security. The public version has been sanitized. No client data, no business secrets.
