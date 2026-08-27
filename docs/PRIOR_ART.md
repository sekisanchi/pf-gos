# PF-GOS Prior Art and Reuse Strategy

This document maps relevant projects, standards, and research directions to PF-GOS. The goal is not to claim uniqueness where mature work already exists, but to identify what should be reused, what should be integrated, and where PF-GOS may contribute a distinct governance layer.

## 1. Metagov

Metagov describes its mission as building a governance layer for the internet and works on community sovereignty, network governance, governance interoperability, standards, and governance tooling.

### Relevance to PF-GOS
- Strong conceptual overlap around governance as infrastructure rather than a single platform.
- Useful prior art for community sovereignty, polycentric governance, and interoperability between independently governed groups.
- Potential source of governance patterns, community design methods, and standards work.

### Reuse
- Governance interoperability concepts.
- Polycentric / federated governance patterns.
- Community-governance tooling ideas and research methods.

### PF-GOS extension
PF-GOS pushes beyond community governance into cross-layer continuity among individuals, families/foundations, voluntary clusters, enterprises, municipalities, states, and inter-network systems, with explicit attention to succession, legal-state reconciliation, privacy-preserving proofs, and intergenerational continuity.

Reference: https://metagov.org/

## 2. European Digital Identity Wallet (EUDI Wallet)

The EUDI Wallet ecosystem defines a common architecture, standards, protocols, and formats so independently implemented wallets can interoperate across EU Member States. The ecosystem includes issuers, wallets, and service providers, with open-source reference implementation components and large-scale pilots.

### Relevance to PF-GOS
- Mature real-world model for federated identity interoperability.
- Strong reference for issuer-holder-verifier role separation.
- Public-sector example of common specifications across independent jurisdictions.
- Important implementation precedent for privacy-preserving attribute presentation and cross-border acceptance.

### Reuse
- Role model: issuer / wallet-holder / relying party.
- Architecture and Reference Framework methodology.
- Interoperability and certification mindset.
- Reference-implementation approach rather than one mandatory implementation.

### PF-GOS extension
PF-GOS should not reinvent digital identity infrastructure. It should treat identity and credentials as one subsystem and focus on governance, rights, institutional accountability, continuity, dispute, amendment, succession, and cross-layer interactions.

References:
- https://commission.europa.eu/topics/digital-economy-and-society/european-digital-identity_en
- https://digital-strategy.ec.europa.eu/en/policies/eudi-wallet-toolbox

## 3. W3C Verifiable Credentials 2.0

W3C Verifiable Credentials 2.0 provides a standard model for issuing, holding, presenting, and verifying digital credentials. The standard family supports selective disclosure and can work with cryptographic methods including zero-knowledge techniques.

### Relevance to PF-GOS
- Strong candidate foundation for credential representation.
- Avoids creating a proprietary PF-GOS credential format.
- Supports the Public / Proof / Private separation central to PF-GOS.

### Reuse
- VC data model.
- Verifiable Presentation patterns.
- Selective disclosure where supported by the chosen proof suite.
- Standard issuer-holder-verifier semantics.

### PF-GOS extension
PF-GOS should specify governance semantics around credentials: who is authorized to issue which claims, how issuance authority is audited, how credentials are revoked, how decisions are appealed, and how credential ecosystems remain portable across independently governed clusters.

References:
- https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/
- https://www.w3.org/TR/vc-data-model-2.0/

## 4. Plurality / Plurality Institute

Plurality Institute focuses on technologies that improve democracy and support human cooperation at scale, connecting research, civil society, industry, and government.

### Relevance to PF-GOS
- Strong philosophical overlap with technology designed to increase cooperation without forcing homogenization.
- Relevant to deliberation, democratic participation, and institutional design beyond simple token voting.

### Reuse
- Participatory and deliberative governance principles.
- Anti-polarization and plural-value design thinking.
- Democratic-technology research methods.

### PF-GOS extension
PF-GOS should supply interoperable institutional primitives that can host pluralistic processes while preserving exit, contestability, privacy, and cross-cluster autonomy.

Reference: https://www.plurality.institute/about

## 5. Web3 / DAO governance

Web3 introduced practical building blocks for decentralized asset custody, programmable transactions, decentralized governance, and independently operated networks. DAO experiments have also exposed major weaknesses in governance based only on token-weighted voting, low participation, plutocracy risk, governance capture, and weak dispute processes.

### Relevance to PF-GOS
- Useful technical substrate for signatures, programmable rules, distributed state, and cryptographic proofs.
- Valuable negative prior art: transparent execution does not equal legitimate governance.

### Reuse
- Cryptographic signing and authorization patterns.
- Open protocol and forkability culture.
- Smart-contract execution only where its immutability and public state are justified.

### Do not inherit blindly
- Token voting as default governance.
- Permanent public disclosure.
- "Code is law" assumptions.
- Irreversible loss of rights after key loss.
- Confusion between technical consensus and political legitimacy.

## 6. PF-GOS differentiation hypothesis

PF-GOS should not compete with identity-wallet standards, ZK libraries, blockchains, or DAO frameworks. Its likely contribution is the integration and governance layer connecting existing primitives across both institutional layers and time.

### Vertical dimension
Individual → family/foundation → voluntary cluster → enterprise → municipality → state → inter-network.

### Horizontal dimension
Independent clusters and jurisdictions interoperate without sharing one administrator or one raw-data database.

### Temporal dimension
Governance continues across key loss, incapacity, death, succession, leadership turnover, institutional failure, and lawful rule change.

### Constitutional dimension
Privacy, accountability, contestability, portability, recovery, anti-scoring safeguards, and limits on permanent power are first-class constraints rather than afterthoughts.

## 7. Reuse-first architecture

PF-GOS should prefer mature standards and reference implementations whenever possible.

| Layer | Prefer to reuse | PF-GOS work |
|---|---|---|
| Identity / credentials | W3C VC, EUDI-compatible patterns | Authority, appeal, portability, governance semantics |
| Selective disclosure / ZK | Existing proof systems and VC-compatible suites | Predicate policy, privacy boundaries, audit semantics |
| Wallet | Existing wallet/reference patterns | Governance-specific UX and recovery requirements |
| Distributed execution | Existing chains / databases / transparency logs where justified | Decision of what must not be on-chain |
| Governance | Metagov / Plurality / institutional-governance prior art | Cross-layer governance protocol and constitutional constraints |
| Succession | Existing legal trust/foundation/inheritance mechanisms | Technical/legal interface and privacy-preserving eligibility |
| Audit | Existing cryptographic audit and conventional institutional audit | Privacy-preserving institutional accountability model |

## 8. MVP implications

The first MVP should therefore avoid building a custom blockchain, custom wallet, custom identity standard, or token.

Priority should be:

1. Select a standards-compatible credential representation.
2. Select the smallest proof mechanism capable of demonstrating one private eligibility predicate.
3. Model two independently governed verifiers/clusters.
4. Define status/revocation/recovery.
5. Explicitly document metadata leakage and correlation risk.
6. Add a human appeal path at the governance specification level.
7. Only introduce distributed ledgers where a clear threat model requires shared, independently verifiable persistent state.

## 9. Open prior-art research

Future research should include:
- identity systems beyond EUDI, including decentralized and national digital-ID approaches;
- ZK credential systems and unlinkable presentations;
- key recovery and social recovery;
- privacy-preserving compliance/audit;
- digital succession and estate planning;
- legal-person / trust / foundation governance;
- public-sector algorithmic accountability;
- federated constitutional governance;
- polycentric governance and Ostrom-inspired institutional design;
- digital public infrastructure (DPI) and digital public goods.

## 10. Working conclusion

PF-GOS should position itself as a **governance interoperability and continuity layer**, not as another base-layer protocol.

The core question is whether mature identity, proof, wallet, and distributed-system technologies can be composed under a constitutional governance model that preserves:

**autonomy + interoperability + privacy + accountability + continuity + corrigibility.**
