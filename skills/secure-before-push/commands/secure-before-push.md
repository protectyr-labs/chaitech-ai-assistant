---
description: Security-by-design check before pushing code to GitHub. Scans staged changes for OWASP Top 10 issues, hardcoded secrets, and SOC 2 gaps.
---

# /secure-before-push

When the user invokes `/secure-before-push`:

1. Run `git diff --staged` and `git status --short` to see the change set.
   - If nothing is staged, run `git diff HEAD` to see working-tree changes.
   - If both are empty, tell the user there is nothing to review and stop.

2. Apply the four-step workflow from the parent skill (`SKILL.md`):
   - Secret scan
   - OWASP Top 10 review
   - SOC 2 relevance check
   - Verdict

3. Output in the structured format documented in `SKILL.md`. Specifically:

   - `Verdict: PASS / WARN / BLOCK`
   - `BLOCK findings:` (must fix before push)
   - `WARN findings:` (should review)
   - `SOC 2 annotations:` (think-about items, non-blocking)
   - `Summary:` one sentence

4. Never print discovered secret values. Redact to `<value-redacted>`.

5. Do not modify files. Do not run commit or push.

## Constraints

- The user is the decision-maker. The skill informs; the user acts.
- If the user asks for help fixing a finding, help fix it. Do not combine that with the scan; run it as a separate conversation after the scan completes.
- If Claude Code lacks `Bash` permission, ask the user to run the git commands and paste the output.
