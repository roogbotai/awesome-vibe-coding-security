# Awesome Vibe-Coding Security [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

Curated resources for securing apps built with AI tools — Lovable, Bolt, v0, Cursor, Replit, and the Supabase/Firebase backends behind them.

AI builders optimize for "it works," not "it's safe," and the two are not the same thing. A weekend app can ship with a database anyone can read, a live API key sitting in the page source, or no security headers at all. This list collects the guides, references, and tools that help you find those problems and fix them.

Contributions welcome — see [Contributing](#contributing).

---

## Contents

- [Start here](#start-here)
- [The core risk: exposed databases](#the-core-risk-exposed-databases)
- [By platform](#by-platform)
- [What to check](#what-to-check)
- [Free tools](#free-tools)
- [Standards and references](#standards-and-references)
- [Contributing](#contributing)

---

## Start here

- [Vibe-Coding Security Checklist](https://github.com/alisaeedkw/vibe-coding-security-checklist) — a pre-launch checklist you can run in an afternoon.
- [Scan your app free](https://www.bleek.dev/scan) — paste a URL, get findings with plain-English fixes. No signup.
- [OWASP Top 10](https://owasp.org/www-project-top-ten/) — the baseline web-app risk list every builder should know.

## The core risk: exposed databases

The single most common leak in AI-built apps is a database table with row-level security turned off. When RLS is off, the public "anon" key that ships in your front-end can read that table directly — so a logged-out stranger can pull your users table with a two-line fetch.

- [CVE-2025-48757 explained](https://www.bleek.dev/cve-2025-48757) — the Lovable + Supabase RLS leak, with how it works and how to check yours. A public study found roughly 1 in 10 sampled apps leaking real data this way.
- [Supabase Row Level Security docs](https://supabase.com/docs/guides/database/postgres/row-level-security) — the official guide to turning RLS on and writing policies.
- [Firebase Security Rules](https://firebase.google.com/docs/rules) — the equivalent for Firestore and Realtime Database.

## By platform

Security notes and common footguns per builder:

- [Lovable security](https://www.bleek.dev/lovable-security)
- [Supabase security](https://www.bleek.dev/supabase-security)
- [Firebase security](https://www.bleek.dev/firebase-security)
- [Bolt security](https://www.bleek.dev/bolt-security)
- [v0 security](https://www.bleek.dev/v0-security)
- [Cursor security](https://www.bleek.dev/cursor-security)
- [Replit security](https://www.bleek.dev/replit-security)

## What to check

The categories that matter most for a shipped app:

- **Secrets in the bundle** — Stripe, OpenAI, AWS, and Supabase service-role keys sometimes end up in client JavaScript. Rotate anything exposed and move it server-side.
- **Database access rules** — RLS on Supabase, Security Rules on Firebase. Default-deny, then open only what should be public.
- **Security headers** — Content-Security-Policy, HSTS, X-Content-Type-Options, and friends. [MDN's CSP reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) is the place to start.
- **Exposed files** — `.env`, `.git/config`, database dumps, and backups served by accident.
- **Cookie flags** — `Secure`, `HttpOnly`, `SameSite` on anything that carries a session.
- **Dependencies** — known CVEs in the libraries your builder pulled in.

## Free tools

- [bleek scanner](https://www.bleek.dev/scan) — 26 checks against a live URL, no signup.
- [Security headers checker](https://www.bleek.dev/tools/security-headers)
- [SSL / TLS checker](https://www.bleek.dev/tools/ssl-checker)
- [Email security (SPF / DKIM / DMARC)](https://www.bleek.dev/tools/email-security)
- [Password strength](https://www.bleek.dev/tools/password-strength)
- [Breach checker](https://www.bleek.dev/tools/breach-checker)
- [Have I Been Pwned](https://haveibeenpwned.com/) — check whether an email or password has appeared in a known breach.

## Standards and references

- [OWASP Top 10](https://owasp.org/www-project-top-ten/) — web application security risks.
- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/) — for the APIs behind your app.
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) — practical, per-topic guidance.
- [MDN Web Security](https://developer.mozilla.org/en-US/docs/Web/Security) — headers, CORS, and browser security models.
- [Mozilla Observatory](https://developer.mozilla.org/en-US/observatory) — a free header and TLS grader.

## Contributing

Pull requests are welcome. Add resources that are genuinely useful and specific to AI-built apps, keep entries to one line, and put them in the right section. Please don't add low-quality or purely promotional links.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/80x15.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, this list is released into the public domain under [CC0](LICENSE).

---

Maintained by the team at [bleek.dev](https://www.bleek.dev) — we find the security leaks in vibe-coded apps.
