# NestJS Security — Reflection

## Most common vulnerabilities in a NestJS backend
- Injection: raw TypeORM queries built with string interpolation instead of parameters.
- Broken access control: routes missing guards, or JWTs without a secret / expiry.
- Misconfigured CORS and missing security headers.
- Secret leakage: credentials committed to git or written to logs.
- Abuse of unauthenticated endpoints when there is no rate limiting.


## How helmet improves security
Helmet sets defensive HTTP response headers so the browser enforces extra rules:
`Content-Security-Policy` restricts what scripts/styles can load (limits XSS impact),
`X-Content-Type-Options: nosniff` stops MIME sniffing, `Strict-Transport-Security`
forces HTTPS, `X-Frame-Options` / `frame-ancestors` blocks clickjacking, and it
removes the `X-Powered-By` fingerprint. It doesn't fix bugs in our code — it shrinks
the blast radius of client-side attacks.

## Why rate limiting matters
Without it, one client can hammer an endpoint: credential stuffing on login,
password-reset/OTP abuse, scraping, or a cheap DoS that exhausts DB and CPU.
Capping requests per IP/identity per time window makes these attacks slow and
expensive. Auth endpoints should have a much lower limit than normal reads.

## Protecting sensitive config in production
- Keep secrets out of the repo: `.env` gitignored, only `.env.example` committed.
- Validate config at startup (Joi schema in `ConfigModule`) so misconfig fails fast.
- Access values through `ConfigService`, never scattered `process.env`.
- Inject secrets at runtime from a secrets manager (AWS SSM/Secrets Manager, Vault,
  Doppler, or the host platform), not a file baked into the image.
- Redact secrets from logs, use least-privilege keys, and rotate them regularly.