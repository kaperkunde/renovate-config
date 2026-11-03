# renovate-config

Kaperkunde's organization-wide Renovate settings. Mend's hosted Renovate reads
`org-inherited-config.json` from this repository and applies it to every
repository in the organization that the Renovate app is installed on.

## What it says

- **Rules:** everything comes from the shared preset,
  [`github>kaperkunde/common-public//renovate/default`](https://github.com/kaperkunde/common-public/blob/main/renovate/default.json).
  - `@kaperkunde/*` updates are grouped and merge themselves once the app's checks pass.
  - Third-party minors and patches arrive as one pull request a week, and patches merge themselves.
  - Majors wait for a person.
- **No onboarding pull requests.** A repository needs no `renovate.json` of its own
  (`onboarding: false`, `requireConfig: "optional"`). Renovate reads a repository's config
  from its default branch, which is production in most of these repositories, so nothing is
  ever written there.
- **Updates land on the non-production branch.** That is `dev` or `develop` (`baseBranchPatterns`).
  A repository whose integration branch is `main` (lorespawner, studyguild, common-public)
  carries a `renovate.json` on `main` saying so. A repository's own config wins over this one.

## Changing it

- **The rules every repository shares:** change the preset in common-public.
- **Which repositories Renovate reaches, and where its pull requests land:** change this file.

This repository is public on purpose. Nothing here names a host or holds a secret. Credentials
Renovate might need, such as for a private registry, go in Mend's settings, encrypted, never in
this file.
