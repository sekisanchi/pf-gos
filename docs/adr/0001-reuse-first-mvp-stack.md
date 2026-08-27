# ADR 0001 — Reuse-first MVP stack

- Status: Accepted for MVP
- Date: 2026-08-28
- Related: #2, #4

## Context

PF-GOS must demonstrate a privacy-preserving eligibility decision across independently governed actors without inventing a new identity protocol, wallet ecosystem, blockchain, or credential format.

The MVP must distinguish three concerns that are often conflated:

1. **Credential semantics** — how an issuer expresses and signs claims.
2. **Issuance/presentation transport** — how holder, issuer, and verifier exchange credentials and proofs.
3. **Predicate privacy** — how a holder proves a computation such as `income < threshold` without revealing the private value.

A selective-disclosure credential can hide undisclosed attributes, but selective disclosure alone does not generally prove arbitrary predicates over hidden values. PF-GOS therefore treats predicate proofs as a separate cryptographic component.

## Decision

### 1. Credential data model

Use **W3C Verifiable Credentials Data Model 2.0-compatible semantics** for issued claims.

Rationale:
- W3C VC 2.0 is a Recommendation.
- It gives PF-GOS a standards-aligned issuer / holder / verifier vocabulary.
- PF-GOS does not need to define a new credential data model.

For MVP, keep the credential schema deliberately small and synthetic.

### 2. Issuance protocol

Use **OpenID for Verifiable Credential Issuance (OpenID4VCI) 1.0** as the target issuance protocol.

Rationale:
- It is an OpenID Final Specification.
- It separates issuer behavior from holder implementation.
- It provides a realistic path toward interoperability with existing wallet ecosystems.

The first local proof-of-concept MAY use a simplified adapter that preserves the same actor boundaries if implementing the entire protocol would delay the first runnable loop. Any simplification must be documented and isolated behind an interface.

### 3. Presentation protocol

Use **OpenID for Verifiable Presentations (OpenID4VP)** as the target presentation boundary.

Rationale:
- OpenID4VP / OpenID4VCI conformance tooling is now available.
- The verifier interface should be compatible with independently governed implementations rather than a PF-GOS-only API.

Again, the first local demo MAY implement a minimal adapter while preserving the protocol boundary.

### 4. Predicate proof

Use a **small dedicated zero-knowledge circuit** for the first hidden predicate.

Initial predicate:

`private_income < public_threshold`

Preferred MVP circuit language: **Noir**, with a local proving backend.

Rationale:
- The project requires an actual predicate/range-style proof, not merely claim redaction.
- Noir gives a compact way to express the first privacy predicate and can keep the proof engine separate from credential transport.
- The proof interface can later be replaced without redesigning the governance model.

Important caveat:
- Noir/tooling must be treated as experimental cryptographic software for the MVP, not production-grade public infrastructure.
- No real financial, identity, or inheritance data will be used.

Fallback:
- If reproducibility or toolchain stability is poor, use **Circom + snarkjs** for the predicate proof. This alternative is mature enough for a local demonstrator but introduces trusted-setup considerations depending on proof system choice.

### 5. Binding credential to predicate proof

The MVP must not prove only that "some secret number is below the threshold."

The ZK circuit/proof construction must bind the private value to an issuer-authenticated commitment or credential-derived value so that a holder cannot choose an arbitrary lower number.

MVP design target:

1. Issuer authenticates a claim or commitment representing the synthetic income value.
2. Holder proves knowledge of the authenticated private value.
3. Holder proves the predicate against the verifier-provided public threshold.
4. Verifier checks issuer authenticity, proof validity, freshness/challenge, and status.

The exact commitment/signature-to-circuit binding is a required design task under Issue #2 and must be threat-modeled before calling the demo complete.

### 6. Selective disclosure

PF-GOS supports selective disclosure as a complementary capability, not as a substitute for predicate proofs.

**BBS-based Data Integrity proofs are not a hard MVP dependency.** As of this ADR, the W3C BBS cryptosuite remains on the Candidate Recommendation track. It may be tested in a later interoperability branch for unlinkable selective disclosure.

### 7. Status / revocation

Use a minimal status abstraction compatible in spirit with **W3C Bitstring Status List v1.0**, but do not implement a global registry.

The verifier must be able to determine whether the synthetic credential is currently acceptable without learning unnecessary holder activity.

Status checks must be included in the privacy threat model because naive per-verification issuer callbacks can create correlation.

### 8. Federation

Do not build a PF-GOS-specific PKI.

For the first two-cluster demonstration:
- each cluster owns its own verifier configuration;
- trust roots/configuration are explicit and separate;
- both accept the same credential/proof contract;
- raw holder databases are not shared.

**OpenID Federation 1.1** is the preferred future standards direction for larger trust networks, but it is not required for the first local two-cluster MVP.

### 9. Holder implementation

Do **not** build a production wallet in MVP.

Implement a minimal holder agent that can:
- receive/store the synthetic credential locally;
- keep private attributes local;
- generate the predicate proof;
- respond to verifier challenge/presentation requests.

Wallet interoperability becomes a later integration objective.

### 10. Blockchain / public ledger

**No blockchain is required for MVP.**

Reasons:
- issuance can be authenticated with ordinary public-key cryptography;
- ZK verification can occur locally/off-chain;
- federation does not require globally shared mutable state;
- placing holder events or identifiers on a public ledger creates correlation and permanence risks;
- PF-GOS should add persistent public state only when a concrete governance property cannot be achieved more simply.

Any future blockchain dependency requires a separate ADR answering:
- what state must be globally shared;
- why conventional signed logs/transparency mechanisms are insufficient;
- privacy/metadata implications;
- governance of upgrades/forks;
- cost and operational dependency.

### 11. Recovery

For MVP, holder keys are disposable synthetic keys. Key loss means re-issuance in the demo environment.

Production recovery is intentionally deferred because it is a governance problem as much as a cryptographic problem. Later designs must consider multi-party/social recovery, issuer re-binding, compromised-device revocation, death/incapacity, and appeal.

### 12. Human appeal / correction

A cryptographically valid proof is not equivalent to a legitimate institutional decision.

The verifier result must expose at least:
- rule identifier/version;
- pass/fail result;
- cryptographic verification outcome;
- credential/status outcome;
- a non-cryptographic path for correction or appeal.

No irreversible denial of a legal or social right may be inferred from the MVP.

## MVP architecture

```text
Synthetic Issuer
  |
  | VC-compatible credential / authenticated claim
  v
Minimal Holder Agent
  |  private attribute remains local
  |  ZK predicate proof
  v
Verifier A ------------------+
                             | shared proof contract
Verifier B ------------------+

Each verifier is independently configured.
No shared raw identity database.
No blockchain required.
```

## Public / proof / private split

### Public
- issuer identifier/key material needed for verification
- rule ID and version
- threshold used for a given verification request
- verifier challenge/nonce
- proof verification result
- aggregate/non-personal audit data where appropriate

### Proof
- issuer authenticity
- holder possession/knowledge as required by the construction
- predicate proof
- freshness/challenge binding
- credential status evidence

### Private
- exact income value
- unrelated credential claims
- holder local secret keys
- unnecessary identity/kinship/financial data

## Rejected alternatives

### Build a new blockchain
Rejected: no demonstrated need and introduces unnecessary governance, privacy, and operational complexity.

### Build a PF-GOS-specific DID/identity method
Rejected: identity-method innovation is not the project’s differentiator.

### Use plain signed JSON only
Rejected as the target architecture because it does not test interoperability standards or selective/minimal disclosure boundaries, though a signed fixture may be used internally for early unit tests.

### Use BBS selective disclosure as the only privacy mechanism
Rejected for MVP predicate requirement: selective disclosure and unlinkable derived proofs are useful, but they do not by themselves implement arbitrary hidden inequality predicates.

### Put exact income in the credential presentation
Rejected: defeats the MVP privacy requirement.

### Build a full wallet before proving the core loop
Rejected: high complexity with little architectural learning.

## Consequences

### Positive
- standards-first and replaceable components;
- no protocol/token/blockchain invention before need;
- clear separation between credentials and computation proofs;
- compatible with future EUDI-style wallet integrations;
- supports two independently governed verifier clusters;
- preserves the PF-GOS principle that technology is subordinate to governance.

### Negative / risks
- binding an issuer-authenticated private claim into a general ZK circuit is the hardest technical part;
- OpenID protocol conformance may add complexity beyond the first demo;
- metadata correlation can survive even perfect claim privacy;
- current ZK developer tooling is not equivalent to audited public-sector infrastructure;
- revocation/status privacy remains a design problem.

## Implementation sequence

1. Threat model and exact trust assumptions (#1).
2. Define synthetic credential schema.
3. Implement issuer signing/authentication fixture.
4. Implement Noir predicate circuit and tests.
5. Bind proof to issuer-authenticated claim/commitment.
6. Add nonce/challenge replay protection.
7. Implement Verifier A.
8. Clone independent Verifier B configuration.
9. Add minimal issuance/presentation adapters aligned with OpenID4VCI/OpenID4VP.
10. Add status/revocation test.
11. Document appeal/correction path.
12. Run external reproducibility test.

## Exit criteria for revisiting this ADR

Revisit if:
- the ZK toolchain cannot reproducibly bind authenticated credential claims;
- a more mature standards-based predicate-proof credential mechanism becomes suitable;
- EUDI/OpenID profiles impose a materially better format choice;
- interoperability testing shows the selected boundaries are wrong;
- the threat model identifies unacceptable correlation or coercion risk.
