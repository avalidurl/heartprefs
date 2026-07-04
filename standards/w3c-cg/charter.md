# HeartPrefs Community Group — Charter (draft)

> A charter is **optional** to launch a W3C Community Group (verified against the W3C CG FAQ, 2026-07-04) but is included here for clarity and to signal neutral governance. The group can begin work immediately after launch.

## Mission

Develop and maintain **HeartPrefs** — an open, portable, signed **matching-intent document** for agent-mediated matching: one JSON object that says who someone is, who and what they seek, and on what terms an agent may act for them, that any agent at any venue can read, verify, and act on.

## Scope

HeartPrefs invents only the **matching vocabulary** (`self` / `seek` / `free`) and delegates trust, portability, and payment to existing rails via thin binding blocks. In scope:

- The HeartPrefs document model + JSON Schema (draft 2020-12) and its versioning.
- Bilateral, constraint-checked **matching semantics** (dealbreakers, hard filters, soft ranking).
- The **binding blocks** and how they compose existing standards:
  - `identity` — W3C **DID** (`did:pkh` / `did:web`) + a detached **EIP-191** signature over RFC 8785 (JCS) canonical bytes;
  - `attestation` — a W3C **Verifiable Credential** (VC 2.0) proving `ageOver18` by **selective disclosure**;
  - `consent` — an **AP2** Intent Mandate or a signed allowance for standing/delegated access;
  - `payment` — an **x402** quote (HTTP 402 + USDC) to read / submit / subscribe.
- Carriage over **x402** bodies, **A2A** Agent-Card extensions, **MCP** resources, and **ERC-8004** service entries — the same canonical bytes, no transformation.
- The **`application/vnd.heartprefs+json`** media type (→ standards tree on adoption) and the `w3id.org/heartprefs` permalink.
- Conformance: a hosted validator, a conformance badge, and a test suite.

### Out of scope

- The matching/inference engine of any particular venue (implementation detail).
- Identity, payment, credential, or consent standards themselves — HeartPrefs **profiles** and composes them; it does not redefine them.
- Custody of funds or any settlement mechanism beyond advertising an x402 quote.

## Deliverables

1. **HeartPrefs Core** (Community Group Report) — the document model, schema, and matching semantics.
2. **Binding profiles** — DID/VC/AP2/x402 and the A2A/MCP/ERC-8004 carriage profiles.
3. **Conformance suite** + hosted validator + badge.
4. **Registrations** — IANA media type; `w3id.org/heartprefs`.

## Success criteria

At least **three independent implementations** (venues or agents) reading and writing conformant documents, and one cross-venue match completed on portable documents.

## Decision policy

Consensus of participants; the Chair(s) call consensus and record dissent. Anyone may raise an issue in the group's repository. Substantive changes are announced with a comment period before adoption.

## Chairs

Gökhan Turhan (Numetal), initial Chair; additional co-Chairs welcome.

## Participation

Free and open to anyone with a W3C account who joins the group and agrees to the **W3C Community Contributor License Agreement (CLA)**. Contributions to a published specification are made under the CLA; participants voluntarily sign the **Final Specification Agreement (FSA)** when the group publishes a final report.

## Communication

The group's GitHub repository (issues + PRs) is the primary venue; a public mailing list is provided by W3C on launch. All work is public.
