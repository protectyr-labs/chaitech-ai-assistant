---
name: executive-team-template
description: |
  Eight-persona AI executive team for solo founders. Each persona (CEO, CRO,
  CMO, CPO, COO, CFO, CS, CINO) is a specialized Claude Code agent with
  identity, operating rules, and a state file that persists across sessions.
  Fork and customize for your own company. Use when you want consistent,
  in-character strategic input from a full leadership team instead of generic
  advice.
license: MIT
compatibility: claude-code
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

# Executive Team Template

A generic, sanitized version of an eight-persona AI leadership team. Originally built for a solo-founder security consulting business and generalized for community use.

## What you get

Eight agents, each with a distinct role, voice, and scope of responsibility:

| Role | Scope |
|---|---|
| CEO / Chief of Staff | Orchestration, prioritization, arbitration |
| CRO | Pipeline, deals, partnerships, outreach |
| CMO | Content, positioning, brand, distribution |
| CPO | Roadmap, PRDs, sprints, packaging |
| COO | SOPs, QA, delivery, capacity management |
| CFO | Pricing, margins, cash flow, financial sustainability |
| Head of CS | Proof, retention, case studies, expansion |
| CINO | Market intelligence, opportunity discovery, innovation portfolio |

Each agent has:

- A markdown file under `agents/<role>.md` with identity and rules.
- A state file under `state/<ROLE>_state.md` that persists business context across sessions.
- A shared operating model (read state first, speak in character, cite evidence, stay silent if nothing useful to add).

## How to use

1. Copy `agents/` and `state/` into your project's `.claude/` directory.
2. Fill in the state files with your real business context (goals, constraints, current metrics). A starter template lives in each state file.
3. Invoke a persona from Claude Code:

```
> Ask the CRO about our Q2 pipeline.
> Ask the CFO whether we can afford this hire.
> Have the CMO and CPO debate whether to ship the landing page now or next sprint.
```

Claude will load the relevant agent, read its state file, and respond in character.

## Customize

- **Different roles.** Swap CRO for Head of Growth, or add a General Counsel. The pattern is the same.
- **Fewer personas.** Start with 3 or 4 if 8 feels excessive. Most solo founders use CEO plus CFO plus one other to start.
- **Different tone.** Edit the identity section in each `agents/<role>.md`. The persona voice is fully yours to change.

## Sanitization note

This template ships with **placeholder business context only**. The originating version contained real client names, revenue figures, and engagement details. Those were stripped. Your first task when adopting this template is to fill `state/<ROLE>_state.md` with your own data.

## Design principles (keep these if you fork)

- **State first.** Every invocation reads the state file before speaking.
- **In character.** Personas use their voice, priorities, and data, not generic advice.
- **Real data.** Every claim cites specific data from the state file.
- **Silence over filler.** A persona with nothing useful to add stays quiet.

## Credit

Adapted from Protectyr Operating System v3. Original design lives in a private solo-founder ops project; this template is the stripped, generic version released for the ChaiTech Claude Commons.
