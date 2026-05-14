---
description: Render the filled state as a printable HTML deck (DECK.html).
---

# /brand-export

Final command. Reads `brand-workshop/STATE.md` and renders it as a self-contained HTML deck the founder can print, email, or share.

## Behavior

1. Check that `brand-workshop/STATE.md` exists. If not, tell the user to run `/brand-start` first and stop.

2. Run `/brand-review` logic silently. If any **required** section is at status `❌ not started` or `⚠ partial` for a load-bearing field, warn the user before exporting:

   > "Heads up — sections 6 and 7 are empty. The deck will export anyway, but it will have visible gaps. Continue (yes), or hold and finish those first (no)?"

   Wait for confirmation. Default = hold.

3. Read the HTML template at `templates/brand-deck.html` (in this skill folder). The template uses placeholder tokens like `{{COMPANY_NAME}}`, `{{TOP_3_STAKEHOLDERS_CARDS}}`, `{{CASCADE_WHERE}}`, etc. — see the template for the full token list.

4. Substitute every token with content parsed out of `brand-workshop/STATE.md`. For sections that are empty, render the placeholder text `<em class="missing">(not captured — run /brand-&lt;exercise&gt;)</em>` so the deck still reads cleanly.

5. Write the result to `brand-workshop/DECK.html`.

6. Print confirmation:

   > "Wrote `brand-workshop/DECK.html`. Open it in your browser. It is self-contained — no external CSS or JS — and prints cleanly to A4 / Letter PDF (Ctrl+P → Save as PDF)."

## Parsing rules (apply consistently — these matter)

These rules turn the founder's markdown in `STATE.md` into clean HTML. Apply them on every list, every paragraph, every cell.

### R1 · Section extraction

- A section starts at `^## <number>. <name>` and ends at the next `^## ` or end of file.
- A subsection starts at `^### <name>` and ends at the next `^### ` or the next `^## ` or end of file.
- **Strip any trailing `---` horizontal-rule line** from extracted text before further processing. The state file uses `---` as visual separators; never let those leak into rendered HTML.
- Strip leading and trailing whitespace from every extracted block.

### R2 · Inline markdown inside extracted text

When emitting any extracted text into HTML (lists, paragraphs, table cells), apply these conversions:

| Source markdown | Rendered HTML |
|---|---|
| `**bold**` | `<strong>bold</strong>` |
| `*italic*` (single `*` only, not part of `**`) | `<em>italic</em>` |
| `` `code` `` | `<code>code</code>` |
| `[text](url)` | `<a href="url">text</a>` |

Apply these **inside** list items, **inside** paragraphs, **inside** table cells — anywhere user text lands. Do not skip them just because the surrounding container is a `<ul>` or `<div>`.

### R3 · Lists

- A bullet line (`^[-*]\s+`) becomes a `<li>` inside `<ul>`.
- A numbered line (`^\d+\.\s+`) becomes a `<li>` inside `<ol>`. Do **not** treat numbered lists as paragraphs.
- A line like `1. **Name** — Description` (used in the Top-3 stakeholders block) is parsed by the dedicated stakeholder parser, not by the generic list rule.
- Inside any `<li>`, apply R2 (markdown bold / italic / code / links) to the body text.

### R4 · Field rows ("- **Label:** value")

Sections 4 (long-form purpose) and Meta use field-row syntax:

```
- **We exist to:** make things simpler.
- **by:** doing x.
```

For each field row:
- Strip the `- **<Label>:**` prefix.
- Trim whitespace.
- Strip any leading or trailing `"` or `'` from the value (founders sometimes quote their answers).
- Apply R2 to the value.

### R5 · Alternates list (Section 5 short-form purpose)

The "Short purpose sentence (3–7 words)" block looks like:

```
- **Primary:** "Replace a car. Not a bike."
- Alternate: "Bikes that earn the commute."
- Alternate: "Built for the next 20,000 km."
```

For the **primary** field, use R4.

For each **alternate** line:
- Strip the leading `- ` bullet.
- Strip the literal `Alternate:` (or `Alternate -`, or `Alt:`) prefix, trimming surrounding whitespace.
- Strip surrounding `"` or `'` quote pairs symmetrically.
- Emit as `<li>` inside the alternates `<ul>`.

The output `<li>` should contain only the sentence itself — no `Alternate:` label, no stray opening or closing quote.

### R6 · Word cloud (Section 5 word list)

The word list is comma-separated and may include `**bold**` words. Split on commas and newlines. For each word:

- Trim whitespace and trailing periods.
- If wrapped in `**…**`, mark the chip as highlighted (`class="hi"`) and strip the `**`.
- Otherwise emit as a plain `<span>`.

### R7 · Pillars (Section 8)

Each pillar uses this shape:

```
### Pillar 1 — <Short Name>
<One-sentence definition.>

*What this looks like in practice:* <one sentence>
```

When rendering each pillar card:
- The `## Pillar N — Name` heading splits to a number (`01`, `02`, …) and a short name.
- The body up to `*What this looks like in practice:*` is the definition paragraph.
- The line starting with `*What this looks like in practice:*` is rendered as `<em>In practice:</em> <text>`.

### R8 · Cascade (Section 7)

The cascade has five subsections. Each can contain bullets, numbered lists, or paragraphs.

- **Winning aspiration** — usually one paragraph. Wrap in `<p>`.
- **Where to play** — usually a bullet list with `**Label:**` prefixes per line. Convert to `<ul>` with each `<li>` containing `<strong>Label:</strong> value`. Apply R2 to the value.
- **How to win** — may be numbered (`1. … 2. …`) or bulleted. Use `<ol>` for numbered, `<ul>` for bulleted. Apply R2 inside each `<li>`.
- **Capabilities** — has two sub-headings inside (`**Existing:**` and `**Gaps to close:**`). Render as two `<strong>` headers with `<ul>` lists under each.
- **Management systems** — usually a bullet list. Render as `<ul>`.

### R9 · Optional sections 9 (Values) and 10 (Movement)

If section 9 (Values) is empty or contains only the placeholder text "(run `/brand-values` to fill)", render `{{VALUES_SECTION}}` as the empty string — the deck simply omits that section header. Same rule for section 10 (Movement) → `{{MOVEMENT_SECTION}}`.

If filled, render as documented in the template.

### R10 · Empty-section fallback

If a token resolves to genuinely empty content, render it as:

```html
<em class="missing">(not captured — run <code>/brand-&lt;exercise&gt;</code>)</em>
```

Never leave a `{{TOKEN_NAME}}` literal in the output, and never render the cell as blank — the empty-state placeholder is what tells the founder where to come back.

## Self-test before exiting

After rendering, before printing the success message:

1. Search the output for any remaining `{{` token literal. If found, fail loudly: log which tokens did not substitute and stop without writing the file.
2. Search the output for any literal `**` (markdown bold marker). If found, R2 was not applied somewhere — log the line numbers and either fix and re-render, or warn the user that some bold formatting did not convert.
3. Search the output for the literal string `Alternate:`. If found in the alternates list, R5 was not applied — fix.

Only print the success message after these three checks pass.

## Constraints

- The exported HTML must be **fully self-contained**. No external fonts, scripts, or images that require an internet connection. If the template references Google Fonts, fall back to system fonts in the inline CSS.
- Do not invent content. Every cell of the deck must come from `STATE.md` or be marked as missing.
- Preserve the founder's exact wording where possible — apply only the formatting conversions in R1–R10. Never edit, summarize, or "improve" the founder's text.
- Do not auto-open the file or launch a browser. Just write it and tell the user the path.
