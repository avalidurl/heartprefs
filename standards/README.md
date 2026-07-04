# HeartPrefs — standards submissions

Ready-to-submit artifacts for making HeartPrefs an official, portable, permanent standard. Each item here is **prepared** so the founder only has to submit it — the actual external submissions (IANA, W3C, the `perma-id/w3id.org` PR, and serving `did.json`) are **founder actions**, because they are outward-facing and irreversible.

> Authored 2026-07-04, each verified against its first-party spec (links below). Nothing here has been submitted yet.

## Status

| Artifact | Standard | This folder | External submission (founder) | Issue |
|---|---|---|---|---|
| DID issuer document | W3C DID Core / `did:web` | [`did/did.json`](did/did.json) + [`did/README.md`](did/README.md) | serve at `https://ishtar.numetal.xyz/.well-known/did.json` (via **ishtar-website**, not the venue) | GOK-166 |
| Permanent schema URL | w3id.org | [`w3id/`](w3id/) | PR to `github.com/perma-id/w3id.org` | GOK-163 |
| Media type | IANA / RFC 6838 | [`iana/vnd.heartprefs+json.txt`](iana/vnd.heartprefs+json.txt) | email `iana@iana.org` or the IANA web form | GOK-164 |
| Community Group | W3C CG | [`w3c-cg/charter.md`](w3c-cg/charter.md) + [`w3c-cg/README.md`](w3c-cg/README.md) | "Create a Community Group" on w3.org + gather 5 supporters | GOK-172 |

## ⚠ One decision to make first (media-type tree)

RFC 6838 restricts the **standards tree** (`application/heartprefs+json`) to formats recognized by a standards body. HeartPrefs is not there yet, so the **registrable name today is the vendor tree: `application/vnd.heartprefs+json`** (RFC 6838 §3.2 — "vendor" explicitly includes consortia and non-commercial entities). Once the **W3C Community Group** (GOK-172) adopts the spec, it can **graduate** to the standards-tree `application/heartprefs+json`.

- The IANA application here uses **`application/vnd.heartprefs+json`** accordingly.
- `spec/0.1/SPEC.md §10` still advertises `application/heartprefs+json` "(registration pending; use provisionally)". **Recommended follow-up (not done in this PR — it's a normative spec change for you to bless):** reconcile the SPEC to state `application/vnd.heartprefs+json` as the *registered* type and `application/heartprefs+json` as the *target* after CG adoption.

## Suggested submission order

1. **Launch the W3C CG** (free; gives you a standards body → unlocks the standards-tree media type + a neutral governance home).
2. **Register the IANA media type** (`vnd.` now; the CG can graduate it later).
3. **File the w3id PR** *(optional)* — a permanent, host-independent schema URL. The schema `$id` now resolves via GitHub raw (`…/main/spec/0.1/heartprefs.schema.json`); registering `w3id.org/heartprefs` lets you switch the `$id` to the permalink later.
4. **Serve `did.json`** once the issuer signing key is chosen (see `did/README.md`) — needed before the 18+ VC path (GOK-166) goes live.

## First-party sources (verified 2026-07-04)

- did:web — <https://w3c-ccg.github.io/did-method-web/> ; DID Core — <https://www.w3.org/TR/did-core/>
- IANA media types — RFC 6838 <https://www.rfc-editor.org/rfc/rfc6838> ; `+json` suffix — RFC 6839
- w3id — <https://github.com/perma-id/w3id.org>
- W3C Community Groups — <https://www.w3.org/community/about/faq/>
- VC Data Model 2.0 — <https://www.w3.org/TR/vc-data-model-2.0/>
