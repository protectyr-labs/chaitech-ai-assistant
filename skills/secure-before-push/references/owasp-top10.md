# OWASP Top 10 (2021) — pattern cheat sheet

A compact reference the `secure-before-push` skill uses to classify findings. For each category: what to look for in the diff, and what to recommend.

## A01: Broken Access Control

**Look for:**
- New HTTP routes, API endpoints, or pages without an explicit authorization check.
- Middleware or decorator absence: `requireAuth`, `@login_required`, role checks, tenant-scope checks.
- Client-side-only checks ("hide the admin menu if not admin") without the server also enforcing.
- Direct object references (`/invoice/:id`) with no ownership check.

**Recommend:** Add the authorization call before any data access. If the app uses a role system, invoke the role check by name at the top of the handler.

## A02: Cryptographic Failures

**Look for:**
- `md5`, `sha1`, or `des` in crypto contexts.
- Literal encryption keys in source.
- Network calls to sensitive endpoints over `http://` rather than `https://`.
- Plain-text storage of sensitive fields (passwords, SSNs, PHI) in database migrations or schemas.

**Recommend:** Use `argon2` or `bcrypt` for passwords, AES-256-GCM for symmetric encryption, move keys to environment variables or a KMS, enforce TLS.

## A03: Injection

**Look for:**
- SQL built with string concatenation or f-strings: `"SELECT ... WHERE id = " + user_id`.
- Shell commands assembled from user input: `exec("ls " + path)`.
- Template rendering where user content is not escaped.
- `eval()`, `Function()`, `exec()` applied to user input.
- ORM raw queries that accept strings.

**Recommend:** Parameterized queries or ORM query builders. For shell, use argument arrays (`subprocess.run(["ls", path])`). For templates, enable auto-escaping.

## A04: Insecure Design

**Look for:**
- Login endpoint without rate limiting.
- Password reset flow that does not verify identity (email-only, no second factor for high-risk operations).
- Session tokens that do not rotate on privilege change (login, password change, 2FA enable).
- "Remember me" cookies with indefinite expiration.

**Recommend:** Rate limit per-IP and per-account. Require reauth for sensitive actions. Rotate session on privilege change. Cap cookie lifetime.

## A05: Security Misconfiguration

**Look for:**
- `DEBUG = True`, `development = true`, verbose stack traces enabled in production configs.
- `CORS origin = "*"` with credentials, or overly permissive `Access-Control-Allow-Origin`.
- Missing `Content-Security-Policy`, `Strict-Transport-Security`, `X-Frame-Options`, `X-Content-Type-Options`.
- Default or example credentials (`admin / admin`) anywhere.

**Recommend:** Environment-specific config. Lock down CORS. Add security headers via middleware or a helmet-style library. Rotate any default credential immediately.

## A06: Vulnerable and Outdated Components

**Look for:**
- `package.json`, `requirements.txt`, `Gemfile`, `Cargo.toml`, `go.mod` changes that pin to versions known to have CVEs.
- Lockfile changes pulling in vulnerable transitive dependencies.

**Recommend:** Run the ecosystem audit tool (`npm audit`, `pip-audit`, `bundle-audit`, `cargo audit`). Upgrade flagged packages. If no patch exists yet, document the acceptance decision.

## A07: Identification and Authentication Failures

**Look for:**
- Privileged actions (delete user, change billing, export data) without MFA.
- Session timeout not set or set to very long durations.
- Password policy absent (allows weak passwords).
- No lockout after repeated failed login attempts.

**Recommend:** Require MFA for privileged actions. Session timeout 15 to 60 minutes for sensitive apps. Enforce minimum password strength. Exponential backoff on failed logins.

## A08: Software and Data Integrity Failures

**Look for:**
- `npm install` or `pip install` from arbitrary URLs without signature verification.
- CI/CD workflows without commit signature verification.
- Deserialization of untrusted data (`pickle.loads`, `unserialize`, `ObjectInputStream`).
- Autoupdate mechanisms without signature checks.

**Recommend:** Pin to trusted registries. Verify commit signatures in CI. Replace `pickle` with JSON for any external-facing deserialization.

## A09: Security Logging and Monitoring Failures

**Look for:**
- Sensitive actions (login, password change, payment, data export) without a log entry.
- Log lines that include tokens, passwords, or full credit card numbers.
- Absence of a correlation ID or request ID across log entries.
- Silent `catch` blocks that swallow exceptions.

**Recommend:** Log every privileged and sensitive action with user, action, resource, timestamp, and correlation ID. Never log secrets. Emit metrics for abuse indicators (failed logins, rate limit hits).

## A10: Server-Side Request Forgery

**Look for:**
- `fetch(userInput)`, `http.get(userInput)`, `axios(userInput)` without URL allowlist validation.
- Webhook handlers that re-fetch arbitrary URLs passed in the payload.
- Server-side rendering of remote images without validation.

**Recommend:** Allowlist destination hosts. Block RFC1918 private ranges, link-local, and localhost. For webhooks, sign payloads and verify the signature before honoring any URL inside.

---

**Reference:** [OWASP Top 10 (2021)](https://owasp.org/Top10/)
