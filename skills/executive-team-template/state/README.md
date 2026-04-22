# State files

Each persona reads one `<ROLE>_state.md` file before responding. State is what makes the persona specific to your business instead of a generic role-playing prompt.

## What to put in a state file

A state file should contain:

- Current goals (1 to 3, ranked).
- Current constraints (capacity, cash, time).
- Active initiatives the persona owns.
- Recent decisions in this persona's domain.
- Open risks the persona is tracking.
- Links to any detailed files the persona needs (pipeline, content calendar, P&L).

Keep it short. The state file is read at the start of every session, so long files cost tokens every time. Aim for 100 to 300 words.

## Starter template

```markdown
# <ROLE> State

## Current goals (ranked)
1. <goal>
2. <goal>
3. <goal>

## Constraints
- <constraint>
- <constraint>

## Active initiatives
- <initiative>: <status>
- <initiative>: <status>

## Recent decisions
- YYYY-MM-DD — <decision> (link to decision memo if archived)

## Open risks
- <risk> — mitigation: <short plan>

## Linked files
- <path>: <what is in it>
```

## Maintaining state

- Update state files weekly at minimum (for example during a Friday retro).
- Any command that produces a material outcome (deal won, content shipped, feature launched) should append the outcome to the relevant persona's state.
- Do not let state files become a journal. Old entries that are no longer relevant should be pruned or moved to an archive.

## Shared state files

Some files are read by every persona:

- `state/BUSINESS_CONTEXT.md` — what the business does, who it serves, the ICP summary.
- `state/CAPACITY.md` — how much time the team has each week, and how much is already committed.

Create these first. The persona state files assume they exist.
