# How to submit the w3id.org permalink (GOK-163)

Registers `w3id.org/heartprefs` so the schema `$id` (`https://w3id.org/heartprefs/0.1/schema.json`) resolves permanently. Verified against `github.com/perma-id/w3id.org` (2026-07-04).

## Prerequisite

Decide the **canonical immutable host** that will actually serve the schema, and set `<CANONICAL_SCHEMA_HOST>` in [`heartprefs/.htaccess`](heartprefs/.htaccess).
- **Preferred:** a Cloudflare-hosted immutable asset (content-addressed / never-rewritten path).
- **Interim:** a pinned GitHub raw tag, e.g. `raw.githubusercontent.com/gokhan-vc/heartprefs/v0.1/spec` (immutable as long as the `v0.1` tag is never moved).

## Steps

1. Fork `github.com/perma-id/w3id.org`.
2. Copy the **`heartprefs/`** folder from this directory (`standards/w3id/heartprefs/` → the fork's repo root) — it contains `.htaccess` + `README.md`, the structure w3id requires.
3. Confirm `<CANONICAL_SCHEMA_HOST>` is filled in and the redirect resolves as intended.
4. Commit with a **descriptive** message naming the project (w3id rejects generic default messages), e.g. `Add heartprefs namespace (HeartPrefs matching-intent standard)`.
5. Open the PR against `perma-id/w3id.org`. Maintainers review and merge.

**Alternative (no PR):** email `public-perma-id@w3.org` with the desired URL (`w3id.org/heartprefs`), the redirect target, and the preferred HTTP code (302).

## After merge

Verify: `curl -sI https://w3id.org/heartprefs/0.1/schema.json` returns a `302` to the canonical host, and following it returns the schema JSON.
