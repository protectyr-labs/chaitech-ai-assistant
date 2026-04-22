# executive-team-template

Eight AI executives (or fewer, if you prefer) that speak in character, read persistent state files, and give you consistent strategic input instead of generic advice.

## What it does

You ask a question. A specific executive answers. They read their own state file first, then respond from their role's perspective with references to real data you have given them.

## When to use it

- You are a solo founder without a real leadership team.
- You want a persistent advisory board that remembers context across sessions.
- You want to run multi-persona debates on a decision.

## Install

```bash
cp -r executive-team-template/agents /path/to/your-project/.claude/agents/
cp -r executive-team-template/state /path/to/your-project/ops/personas/
```

Then edit each `state/<ROLE>_state.md` to reflect your business.

## Included agents

Three agents are included as **complete examples** to show the pattern:

- `agents/ceo.md`
- `agents/cro.md`
- `agents/cmo.md`

The other five (CPO, COO, CFO, CS, CINO) are described in the table in SKILL.md. Use the three included examples as the pattern and write the remaining five to match your company. Add or remove roles as you see fit.

## Example run

```
> Ask the CRO if it is the right time to raise prices.

[CRO persona loaded]
[Reads state/CRO_state.md: pipeline = 4 active deals, 2 at late stage,
average deal size $12K, win rate 33%]

CRO: No, not this quarter. Our late-stage deals were quoted at current
pricing and a mid-cycle change creates reason to renegotiate, which we
cannot afford given the thin pipeline. Revisit after the two late-stage
deals close in May.
```

The CRO refused to give a generic answer because its state file told it the real situation.

## Credit

Pattern extracted from Protectyr Operating System v3. See SKILL.md for full lineage.
