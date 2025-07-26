# Stablecoin Transfers with EUDI Compliant Crypto Wallet

## Introduction

The rapid evolution of **digital assets** and **stablecoins** is transforming the landscape of payments, remittances, and digital commerce. However, the adoption of these technologies faces challenges such as **regulatory compliance**, **privacy protection**, and **cross-border interoperability**.

This repository defines a **reference specification** for **stablecoin transfers** that aligns with **European regulatory frameworks** like **MiCA**, **TFR**, and **AMLD6**, while preserving user privacy through technologies like **EUDI wallets**, **OIDC4VP**, and **SD-JWT**. It introduces a secure and auditable payment architecture where **verifiable identity data** is cryptographically tied to digital asset transfers, ensuring both **compliance** and **user sovereignty**.

For further background and industry insights, see the article:
[The Future of Compliant Crypto in Europe – EUDI Wallets and Stablecoin Transfers](https://medium.com/@thierry.thevenet/the-future-of-compliant-crypto-in-europe-eudi-wallets-and-stablecoin-transfers-9d4c6c799c82).

This repository contains the specification for enabling **stablecoin transfers** (e.g., USDC, DAI, EVM-based stable assets) using an **EUDI Wallet** or equivalent **non-custodial data wallet**.
The specification focuses on combining **OIDC4VP**, **Verifiable Credentials (VCs)**, and **digital asset transfers** while ensuring **compliance with EU regulations** (e.g., MiCA, TFR, AMLD6) and **data privacy (GDPR)**.

---

## 📄 Specification Documents

- [**Stablecoin Payments with EUDI compliant wallet**](stablecoin_oidc4vp.md) – Full technical specification.
- [**Use Cases and Implementation Strategies**](use_case_and_implementation_strategies_improved.md) – Practical scenarios and verifier strategy models.

---

## Key Highlights

- **Privacy-preserving payments** using **SD-JWT** for selective disclosure and **OIDC4VP** for verifiable presentations.
- **Multi-chain support**: Ethereum, Etherlink, EVM-compatible chains, and other networks.
- **Regulatory compliance** aligned with MiCA, AMLD6, DAC8, and eIDAS 2.0.
- **Interoperability** with open standards such as **JWS**, **JWE**, and **DIF Presentation Exchange**.
- **Auditability and user consent** with verifiable proofs, consent receipts, and traceable logs.

---

## Implementation

The first implementation of this specification is available through [**Altme.io**](https://altme.io), demonstrating real-world integration of **EUDI crypto Wallets** for stablecoin payments and compliance flows.

---

## Repository Structure

- `stablecoin_oidc4vp.md` – Core technical specification.
- `use_case_and_implementation_strategies_improved.md` – Use cases and verifier implementation strategies.
- Supporting documentation and images.

---

## Getting Started

1. Read the [main specification document](stablecoin_oidc4vp.md).
2. Explore [use cases and implementation strategies](use_case_and_implementation_strategies_improved.md).
3. Use this repository as a foundation for building **compliant stablecoin payment solutions** with **EUDI-compatible wallets**.

---

## License

This repository is provided for **research and implementation guidance**.
Please review the individual document headers for licensing terms.
