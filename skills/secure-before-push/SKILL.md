---
name: secure-before-push
description: |
  Security-by-design check that runs before you push code to GitHub. Reviews
  your pending changes for OWASP Top 10 issues, hardcoded secrets, insecure
  defaults, and gaps in logging and access control that would fail a SOC 2
  audit. Run /secure-before-push before committing; it tells you what to fix,
  what to think about, and what is fine.
license: MIT
compatibility: claude-code
allowed-tools:
  - Read
  - Grep
  - Bash
---

# Secure Before Push

A gentle security reviewer for the code you are about to push. Catches common mistakes before they reach GitHub.

## When to invoke

- User types `/secure-before-push` (or invokes the skill by name).
- User says "review this before I push", "check my staged changes for security issues", or similar.
- Always before the user asks Claude to commit or push work that will become public.

## Workflow

### Step 1. Collect the change set

Run:

```bash
git diff --staged          # if changes are staged
git diff HEAD              # if nothing staged yet, diff the working tree
git status --short
```

If nothing is staged and the working tree is clean, tell the user there is nothing to review and stop.

### Step 2. Secret scan

Scan the change set for hardcoded credentials. Look for:

- AWS keys (`AKIA[0-9A-Z]{16}`, `ASIA[0-9A-Z]{16}`)
- GitHub tokens (`ghp_`, `gho_`, `ghu_`, `ghs_`, `ghr_`)
- Stripe keys (`sk_live_`, `sk_test_`, `pk_live_`)
- Slack tokens (`xoxb-`, `xoxp-`, `xoxa-`)
- Generic patterns: `password =`, `api_key =`, `secret =`, `token =` with literal string values
- Private keys (`-----BEGIN RSA PRIVATE KEY-----`, `-----BEGIN OPENSSH PRIVATE KEY-----`)
- Connection strings with embedded passwords (`postgres://user:pass@host`, `mongodb+srv://user:pass@`)

Any match is a BLOCK finding. Recommend moving the value to an environment variable and rotating the compromised credential.

### Step 3. OWASP Top 10 review (2021 edition)

For each changed file, consider each category and report any concerns.

1. **A01 Broken Access Control.** New routes, endpoints, or pages without explicit authorization checks. Look for missing `requireAuth`, missing role checks, missing tenant-scope checks.
2. **A02 Cryptographic Failures.** New use of `MD5`, `SHA1`, `DES`, hardcoded encryption keys, plain-text storage of sensitive data, non-HTTPS URLs for sensitive operations.
3. **A03 Injection.** Raw SQL with string concatenation, shell commands built from user input, unparameterized template rendering, `eval()` / `exec()` on user input.
4. **A04 Insecure Design.** Authentication flows that skip rate limiting, password reset that does not verify identity, session tokens that do not rotate on privilege change.
5. **A05 Security Misconfiguration.** `DEBUG = True`, verbose error pages in production, CORS set to `*`, missing security headers (CSP, HSTS, X-Frame-Options), default admin credentials.
6. **A06 Vulnerable and Outdated Components.** Package updates that pin to known-vulnerable versions. Suggest `npm audit` / `pip-audit` / `cargo audit` run before push.
7. **A07 Identification and Authentication Failures.** Missing MFA on privileged endpoints, session timeouts not set, password strength not enforced, credential stuffing not rate-limited.
8. **A08 Software and Data Integrity Failures.** Unsigned package installs from arbitrary sources, CI/CD workflows without commit signature verification, deserialization of untrusted data.
9. **A09 Security Logging and Monitoring Failures.** Sensitive actions (login, password change, payment) with no log entry, logs that include tokens or passwords, absence of a correlation id.
10. **A10 Server-Side Request Forgery.** Fetch/axios calls where the URL comes from user input without allowlist validation, webhook handlers that re-fetch arbitrary URLs.

For each finding, output: file, line range, category, short explanation, recommended fix.

### Step 4. SOC 2 relevance check

SOC 2 is not a code review but an evidence review. The skill flags patterns that would complicate a Common Criteria audit later:

- **Access control (CC6).** New admin action without an audit log entry. New role without a documented permission matrix.
- **Encryption (CC6.7, CC6.8).** New sensitive field stored without encryption at rest. New network call without TLS.
- **Change management (CC8.1).** Commit touching production configs without a clear "why" in the commit message.
- **Monitoring (CC7.2).** New error path that silently swallows exceptions. New metric that could indicate abuse (failed logins, rate limit hits) that is not emitted.
- **Data retention and disposal (CC3.1).** New place where user data is stored without a documented retention period.

Do not fail the push for SOC 2 findings. Annotate them as "think about this" items with a short note on what evidence a future auditor would want.

### Step 5. Produce the verdict

Output a single structured block:

```
SECURE-BEFORE-PUSH RESULTS

Verdict: PASS / WARN / BLOCK

BLOCK findings (must fix before push):
- <file:line> - <category> - <what is wrong> - <how to fix>

WARN findings (should review):
- <file:line> - <category> - <what to consider>

SOC 2 annotations (think about before the next audit):
- <file:line> - <control> - <what the auditor would want>

Summary:
<one sentence on overall posture>
```

If verdict is BLOCK, tell the user clearly that the push should wait until BLOCK findings are fixed. If WARN, let the user decide. If PASS, congratulate briefly and note anything particularly nice the user did (consistent auth checks, good error handling, clear naming).

## Constraints

- Do not modify any files during the review.
- Do not run the commit or push on behalf of the user after the review. The user runs those commands; the skill's job is to inform.
- Never write discovered secret values to logs or screen. Redact to `<value-redacted>` when reporting.
- False positives are preferable to false negatives. If a pattern looks suspicious but context is unclear, flag it as WARN rather than ignoring.

## Scope

This skill reviews the pending change set only. It does not:

- Audit the entire repository history.
- Replace a full penetration test or third-party security assessment.
- Replace `npm audit`, `pip-audit`, `trivy`, or similar dependency scanners. (Recommend running those as complementary checks.)

## References

- OWASP Top 10 (2021 edition): https://owasp.org/Top10/
- SOC 2 Common Criteria: https://www.aicpa-cima.com/resources/download/2017-trust-services-criteria-with-revised-points-of-focus-2022
- See `commands/secure-before-push.md` for the slash command definition and `references/owasp-top10.md` for the pattern cheat sheet this skill uses.

## Credit

Authored for the ChaiTech AI Assistant seed by Alexander Madaniev, CISSP, Cohort 7. Grounded in OWASP Top 10 (2021) and SOC 2 Common Criteria.
