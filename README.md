# PF-GOS

**Persistent Federated Governance Operating System**  
多層的永続型分散統合ガバナンス・オペレーティングシステム

PF-GOS is an experimental governance infrastructure for independently governed actors—individuals, families/foundations, voluntary clusters, enterprises, municipalities, states, and eventually cross-border networks—to interoperate through verifiable rules while minimizing unnecessary disclosure.

## Core idea

> Subjects remain autonomous. Power is distributed. Private information is minimally disclosed. Public acts are verifiable. Rights, assets, responsibilities, and governance can survive organizational and generational transitions without creating permanently unaccountable power.

PF-GOS explores a transition from **trust-only governance** toward **trust-minimized, privacy-preserving, verifiable governance**.

## Layers

1. **Individual** — identity, credentials, rights, consent, personal agency
2. **Family / Foundation** — kinship, stewardship, succession, intergenerational assets
3. **Voluntary Cluster** — communities, cooperatives, DAOs, professional networks
4. **Enterprise** — employment, transactions, compliance, audit
5. **Municipality** — public services, eligibility, local participation
6. **State** — law, courts, standards, minimum guarantees
7. **Inter-network** — interoperability between jurisdictions and governance systems

## Privacy model

PF-GOS separates governance information into three layers:

- **Public layer** — outcomes and facts that require public accountability
- **Proof layer** — cryptographic/verifiable evidence that rules were satisfied
- **Private layer** — personal, familial, commercial, medical, financial, and other information that need not be disclosed

ZK proofs, selective disclosure, verifiable credentials, signatures, and auditable protocols are candidate mechanisms—not ideological requirements. Technology is subordinate to rights and governance.

## MVP

The first MVP demonstrates a minimal cross-cluster eligibility flow:

`Issuer -> Credential Holder -> Privacy-preserving proof -> Independent Verifier -> Right/Benefit -> Auditable result`

The verifier should be able to establish that a rule was satisfied without receiving the underlying sensitive attributes when disclosure is unnecessary.

A parallel sandbox will model **intergenerational stewardship**: succession events, kinship eligibility, governed access to shared assets, key recovery, and institutional continuity. It will use simulated assets until legal/tax structures are independently reviewed.

## Non-goals

PF-GOS is **not**:

- a cryptocurrency project by default;
- an attempt to put all social data on-chain;
- a replacement for courts, democratic institutions, or human judgment;
- a social-credit or universal scoring system;
- a mechanism for avoiding tax, inheritance law, regulation, or accountability;
- an assumption that everything valuable about human life can or should be formally proven.

## Project principles

See [CONSTITUTION.md](CONSTITUTION.md). The constitutional layer takes precedence over implementation convenience.

## Execution

See [ROADMAP.md](ROADMAP.md) for the initial 90-day plan and [reviews/WEEKLY_REVIEW_TEMPLATE.md](reviews/WEEKLY_REVIEW_TEMPLATE.md) for the operating cadence.

The project context that led to this repository is summarized in [docs/CONVERSATION_HANDOFF.md](docs/CONVERSATION_HANDOFF.md).

## Status

**Phase 0 — project initialization.** Specifications are provisional and intended for critique, forkability, and iterative improvement.

## License

License selection is intentionally left open for the first governance review. The project should favor forkability while separately considering defensive protections for specifications, trademarks, and reference implementations.