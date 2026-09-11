# How does Auth0 handle authentication vs. traditional username/password?
With a traditional setup, your own server stores password hashes, handles
login forms, resets, and MFA, and is the thing an attacker targets. Auth0 takes
all of that off your server: it hosts the login page, verifies credentials (or
social/SSO login), and hands your app back a signed JWT. Your API never sees a
password - it only ever verifies a token's signature.

## What is the role of JWT in API authentication?
The JWT is proof of identity the client attaches to every request
(such as: Authorization: Bearer <token>). It's a self-contained, signed claim - your
API can verify it's genuine and unexpired using only a public key, with no
database lookup or session store, which is why JWT auth scales well across
stateless API instances.

## How do jwks-rsa and public/private key verification work in Auth0?
Auth0 signs tokens with a private key it keeps secret, using RS256 (asymmetric).
`jwks-rsa` fetches Auth0's matching *public* keys from its JWKS endpoint
(`/.well-known/jwks.json`), caches them, and hands the right one to
`passport-jwt` based on the token's `kid` header, so your API can verify the
signature without ever holding Auth0's private key.

## How would you protect an API route so only authenticated users can access it?
Register a Passport JWT strategy that validates the token against Auth0's JWKS
and the expected `audience`/`issuer`, then apply `@UseGuards(AuthGuard('jwt'))`
to the route (or the whole controller). Any request without a valid, unexpired,
correctly-signed token gets a 401 before the handler runs.