# `did:web:ishtar.numetal.xyz` — the HeartPrefs issuer identity (GOK-166)

Ishtar needs a stable, self-controlled **issuer identity** for two things in a HeartPrefs document:

- `identity.subject` = `did:web:<host>` when a **venue/issuer** (not an end-user wallet) is the controller;
- `attestation.credential` = a W3C **Verifiable Credential** proving `ageOver18`, **issued by this DID** after an out-of-band age check.

`did:web` resolves a DID to a document over plain HTTPS: **`did:web:ishtar.numetal.xyz` → `https://ishtar.numetal.xyz/.well-known/did.json`** (host root; no path segment in the DID → `/.well-known/`). Verified against the did:web method spec (2026-07-04).

## Before you serve it — REQUIRED fill-in

[`did.json`](did.json) is a template. Replace the placeholder before serving:

- **`blockchainAccountId`** — the zero address `0x0000…0000` is a placeholder. Set it to **Ishtar's VC-signing wallet** (the key that will sign age credentials), in CAIP-10 form `eip155:<chainId>:<address>`. `chainId` is set to **8453 (Base)** to match Ishtar's settlement chain; the same secp256k1 key works regardless of chain, so keep 8453 unless you deliberately anchor elsewhere.
  - Using a secp256k1 / Ethereum key (`EcdsaSecp256k1RecoveryMethod2020`) is deliberate: it lets the **same wallet** both sign EIP-191 document proofs (`proof.type = "EIP191"`, see `spec/0.1/SPEC.md §2`) and issue VCs — one key, whole stack. If you prefer a dedicated Ed25519 issuer key, swap the verification method to `Ed25519VerificationKey2020` + a `publicKeyMultibase` and drop the secp256k1 context.
- **`serviceEndpoint`** — points at `api.ishtar.numetal.xyz`; adjust if the issuer service lives elsewhere.

## Where to serve it

At the **site** (`ishtar-website`), NOT the venue — as a static asset at `/.well-known/did.json`, `Content-Type: application/did+json` (or `application/json`), served over HTTPS with a valid cert (did:web requires TLS). This is a founder deploy; it touches the site, not `numetal-datebook`.

## The 18+ Verifiable Credential (the `attestation` block)

Per `spec/0.1/SPEC.md §3` + VC Data Model 2.0 (verified 2026-07-04):

- After an out-of-band age check (Didit / Persona), Ishtar (as `did:web:ishtar.numetal.xyz`) **issues a VC** whose `credentialSubject` discloses **only** a boolean `ageOver18: true` — **never a date of birth** (VC 2.0 defines no normative age field, so v0.1 pins the property name `ageOver18`).
- The HeartPrefs doc carries a **Verifiable Presentation** of that VC in `attestation.credential`; `attestation.ageOver18` is a fast-filter summary, the credential is the source of truth.
- Use **selective disclosure** so nothing but the predicate leaks — SD-JWT-VC or a BBS-2023 cryptosuite. Pin the exact cryptosuite against its first-party spec before locking (the SPEC's §9 re-verify rule applies).

## Verification (for consumers)

Resolve `did:web:ishtar.numetal.xyz` → fetch `/.well-known/did.json` → read `assertionMethod` → check the VC's proof recovers to that key. For the document's own `proof` (EIP-191), recover the signer from the JCS canonicalization and assert it equals `identity.subject` (SPEC §2).
