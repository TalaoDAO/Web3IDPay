
# Stablecoin Payments with EUDI compliant Wallet

This repository contains the specification for enabling **stablecoin payments** (e.g., USDC, DAI, Tezos-based stable assets) using an **EUDI Wallet** or equivalent **non-custodial data wallet**.  
The specification focuses on combining **OIDC4VP**, **Verifiable Credentials (VCs)**, and **digital asset transfers** while ensuring **compliance with EU regulations** (e.g., MiCA, TFR, AMLD6) and **data privacy (GDPR)**.

---

## 📄 Specification Document

The complete specification is detailed in the following document:

- [**Stablecoin Payments with EUDI compliant wallet**](stablecoin_oidc4vp.md)

---

## Key Highlights

- **Privacy-preserving payments**: Uses **SD-JWT** for selective disclosure and **OIDC4VP** for verifiable presentations.
- **Multi-chain support**: Ethereum, EVM-compatible chains, Tezos, and others.
- **Regulatory compliance**: Aligns with MiCA, AMLD6, DAC8, and eIDAS 2.0.
- **Merchant-Wallet interoperability**: Uses open standards like **JWS**, **JWE**, and **DIF Presentation Exchange**.
- **Auditability and user consent**: Supports verifiable proofs, consent receipts, and auditable logs.

---

## Repository Structure

- `stablecoin_oidc4vp.md` – Full technical specification.
- `error_handling_and_recovery.md` – Error handling and recovery strategies for the platform.
- Other supporting documents and examples.

---

## Getting Started

1. Read the main [specification document](stablecoin_oidc4vp.md).
2. Use this as a foundation for developing compliant stablecoin payment solutions with EUDI-compatible wallets.

---

## License

This repository is provided for **research and implementation guidance**.  
Please review the individual document headers for licensing terms.

---
