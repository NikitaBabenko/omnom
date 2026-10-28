# Omnom on VibeNest: static pilot, blocked

Checked 28 October 2026. This fork retains the upstream source and AGPL license.
Upstream base: `asciimoo/omnom@5abef24e0ce66bec9c04e1dc84822b82b130bd50`.
The only build change is `golang:1.24` -> `golang:1.26`, matching `go.mod`.
It has not been built or tested. The base tag is not an immutable release recipe.
Fork Actions are disabled; no application code has been run for this pilot.

## Current result

**Not ready for deployment or Free-tier acceptance.** The button records the fork
and explicit `master` branch for a future gated deployment. It is not evidence of
a working launch. No demo exists.

The upstream Docker publication for the October session fix
[failed](https://github.com/asciimoo/omnom/actions/runs/37103531792): `go.mod`
requires Go >=1.26, while that builder used Go 1.24.13 with `GOTOOLCHAIN=local`.
Changing the Dockerfile version is only a proposed build compatibility correction.

The [documented upstream image](https://github.com/asciimoo/omnom/wiki/Docker),
`ghcr.io/asciimoo/omnom:master`, currently resolves to:

| Item | Observed value |
| --- | --- |
| Index | `sha256:25e3f824e7b25b6fd1422b38c4b8582aef27beb2863fc8019cd955a684d3d1d5` |
| Linux amd64 manifest | `sha256:238a1f28ddbe003159b23dea819fccd2f7ecdefc0d2b0adc7034e76f05e82715` |
| OCI/provenance source revision | `673919d2130ce2d7fdc930d89850bf7c39917f4f` |
| Build date | 22 June 2026 |
| Binary build info | Go 1.24.13, linux/amd64, CGO enabled |

This is before [the session signing fix](https://github.com/asciimoo/omnom/commit/5abef24e0ce66bec9c04e1dc84822b82b130bd50).
The latest binary release, v0.9.0 from January, also predates it. Neither is an
acceptable shortcut for this pilot. Do not substitute an old binary under the
current source tree. A new exact-source build and image provenance are required.

The currently assigned VibeNest target has a known source-build networking
blocker. No compiler, CI run, or runtime slot is assigned to this pilot. This is
a blocker for this candidate, not a reason to pause other pilots or change the
platform's security, capacity, or host networking policy.

## Minimal setup requirements, not an accepted recipe

Omnom can create an owner and login tokens through its own CLI, without SMTP or
OAuth. A future guided setup could use `omnom create-user OWNER EMAIL` and
`omnom create-token OWNER login`, with the actual values chosen by the owner.
These commands print credentials: capture their output privately, never into
deployment logs, reports, shell history, or a repository. CLI access through an
authorized setup mechanism still needs to be established. This is not unattended
one-click onboarding.

Required configuration for that investigation:

- SQLite plus persistent `/omnom/config` for database and ActivityPub keys;
  persistent `/omnom/static/data` for archived content. `VOLUME` declarations
  alone do not prove persistent mounts are applied by the platform.
- `app.disable_signup: true`, `app.create_snapshot_from_webapp: false`,
  `server.secure_cookie: true`, and an exact HTTPS `server.base_url`.
- No SMTP, OAuth, or Chromium. Keep `remote_user_header` unset unless a separately
  reviewed authenticating proxy exclusively owns the backend network path and
  replaces incoming identity headers.
- These settings alone do **not** establish a private instance. Signup behavior,
  direct archive access, uploads, cookies and outbound ActivityPub/feed fetching
  require additional containment and review before exposure. No such proxy or
  security adaptation is included or claimed to work in this fork.

## Resources and remaining acceptance

Free target: 256 MiB RAM, 0.5 platform CPU, 4096 MiB storage; coordinator must
recheck limits and effective host CPU before any assignment. Go/SQLite without
Chromium is a candidate for a small workload, but RAM, startup, idle/peak CPU,
disk growth, OOM/restarts and build costs are **unmeasured**. Archives and feeds
have variable size; no capacity or performance guarantee is made.

After a safe current runtime exists, an explicitly assigned test must follow the
README button through registration/existing login with repo and branch retained,
then the normal gated launch. Test clean configuration separately from reused
ENV and volumes. Confirm actual limits, HTTPS/auth/cookies, a small private
bookmark and harmless synthetic HTML archive via the native API, and one small
owner-selected feed. Verify database, archive and key persistence after normal
gated restart/redeploy. Exercise access restrictions without exploit or load
tests. Stop and clean up only the assigned pilot after recording evidence.

No runtime attempt, production safety clearance, persistence test or useful
workflow acceptance has occurred. This current variant is closed as blocked.
