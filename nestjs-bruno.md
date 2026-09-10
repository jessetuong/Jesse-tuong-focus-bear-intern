# API Debugging with Bruno — Reflection

## How does Bruno help with API testing compared to Postman or cURL?
Bruno gives you a UI for building, saving, and replaying requests without
retyping long cURL commands, and it shows the full response (status, headers,
body, timing) clearly for debugging. Unlike Postman, its collections are
plain-text files stored in the repo, so they're version-controlled, reviewable in
PRs, and don't require a cloud account or sync. It's lighter and fully offline.

## How do you send an authenticated request in Bruno?
Add an `Authorization` header of `Bearer {{token}}` (or use the Auth tab → Bearer
Token), where token is a variable defined in the active Environment. The
token can be set manually, or populated automatically by a pre-request script
that logs in and stores the returned JWT as an environment variable.

## What are the advantages of organizing API requests in collections?
Related requests live together and share a base URL and auth via environments, so
you switch between local/staging/prod by changing one dropdown. New team members
get a ready-made, runnable map of the API. Saved requests double as
lightweight documentation and quick regression checks.

## How would you structure a Bruno collection for a NestJS backend project?
One collection per service, folders per resource/controller (`users/`, `auth/`,
`queue/`), one `.bru` file per endpoint named by intent ("List users", "Create
user – invalid"). An `environments/` folder for `local` and `staging` holding
`baseUrl` and a secret `token`. A login request plus a pre-request script that
refreshes `token` so authenticated requests just work. Commit it all to the repo.