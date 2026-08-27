# PF-GOS — Initial 90-Day Roadmap

## Objective

Turn PF-GOS from a governance thesis into a falsifiable, executable MVP while preserving privacy, legal realism, institutional accountability, and forkability.

## Days 0–30 — Define and prove one narrow loop

### Governance
- Review Constitution v0.1 and record objections rather than prematurely seeking consensus.
- Define actor model: issuer, holder, verifier, auditor, adjudicator/reviewer.
- Produce threat model covering capture, collusion, coercion, identity theft, key loss, correlation, and governance abuse.

### Technical
- Specify one eligibility predicate using synthetic data.
- Define credential schema and disclosure boundaries.
- Implement a minimal issuer → holder → proof → verifier flow.
- Keep blockchain optional; justify any persistent public state.

### Legal/institutional
- Map which MVP statements are technical proofs versus legal facts.
- Document requirements for human appeal and correction.
- Do not use real inheritance assets or sensitive personal data in Phase 1.

### Exit criterion
A third party can run the demo locally and verify an eligibility result without receiving the protected source attribute.

## Days 31–60 — Federate two independent clusters

- Create two independently administered verifier/cluster configurations.
- Demonstrate credential/proof interoperability without sharing raw identity databases.
- Add revocation/status handling.
- Add recovery experiment for lost holder keys.
- Add audit output that demonstrates correct aggregate execution without publishing participant-level data.
- Document correlation and metadata leakage.

### Exit criterion
Two independently configured clusters can accept a shared proof/credential contract while retaining separate governance.

## Days 61–90 — Succession and stewardship sandbox

Using simulated assets only:

- Define a private kinship/eligibility graph model.
- Model death/incapacity/succession events.
- Demonstrate governed access rights rather than naive transfer of raw ownership.
- Model trustee/foundation/committee roles without claiming legal equivalence.
- Add amendment, dispute, emergency-stop, and institutional-failure scenarios.
- Produce legal questions for Japanese trust, foundation, inheritance, tax, privacy, and identity specialists.

### Exit criterion
A reproducible sandbox demonstrates that governance, access rights, auditability, and succession can continue across a simulated generational transition without requiring publication of the full kinship graph.

## Weekly operating cycle

Every week:

1. What became demonstrably true?
2. What assumption was falsified or weakened?
3. What new privacy/security risk appeared?
4. What governance power became too concentrated?
5. What legal assumption needs expert validation?
6. What should be deleted or simplified?
7. What are the next three highest-leverage actions?

Use `reviews/WEEKLY_REVIEW_TEMPLATE.md` and keep reviews in the repository.

## Success at Day 90

PF-GOS should have:

- a contestable constitutional layer;
- a runnable privacy-preserving eligibility MVP;
- two-cluster federation demonstration;
- a documented threat model;
- a recovery and revocation story;
- an intergenerational stewardship sandbox;
- an explicit legal-questions register;
- enough documentation for an independent team to fork and reproduce the work.

The goal is not token issuance, fundraising, or maximum adoption. The goal is to establish whether the architecture can produce **autonomy + interoperability + privacy + accountability + continuity** at the same time.