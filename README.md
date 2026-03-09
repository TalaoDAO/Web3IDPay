# Secure Crypto Payments with the EUDI Wallet

Last update: March 2026

## Introduction

The rapid growth of **digital assets, stablecoins, and decentralized finance** is transforming payments and digital commerce. However, the adoption of these technologies in Europe requires solutions that combine:

- regulatory compliance
- user privacy
- secure identity verification
- interoperability with EU digital identity frameworks

This repository provides a **reference architecture and specification** for enabling **secure crypto and stablecoin payments using the European Digital Identity Wallet (EUDI Wallet)**.

The approach combines:

- Self-custodial crypto wallets
- Verifiable Credentials (VCs)
- OIDC4VP / OIDC4VCI protocols
- Selective disclosure with SD-JWT
- Strong Customer Authentication (SCA) aligned with the **EUDI ARF TS12 specifications**

The goal is to demonstrate how **identity-assured crypto payments** can be performed while preserving the decentralized nature of blockchain transactions.

---

# Main Use Case

## Secure Crypto Person-to-Merchant Payments (P2M)

The main use case described in this repository demonstrates how a **natural person can pay a merchant using a non-custodial crypto wallet**, while the **EUDI Wallet provides the trusted identity and authentication layer**.

In this architecture:

- the **EUDI Wallet performs identity authentication and Strong Customer Authentication (SCA)**
- the **crypto wallet performs the blockchain transaction**
- the **payment gateway verifies the payment and the identity proof**
- **no intermediary executes the on-chain transaction**

This separation allows the system to combine:

- self-custodial blockchain payments
- EU-compliant identity authentication
- privacy-preserving disclosure

---

# Key Concepts

## EUDI Wallet as Identity Layer

The **EUDI Wallet** acts as the **trusted identity and consent layer** for crypto payments.

It enables users to:

- authenticate using **PID or other identity credentials**
- present **Proof of Crypto Account Ownership credentials**
- sign transaction consent using **advanced electronic signatures**
- provide **selective disclosure of identity attributes**

---

## Proof of Crypto Account Ownership (SCA Credential)

Strong Customer Authentication is implemented through a **Proof of Crypto Account Ownership credential**, issued as a **Qualified Electronic Attestation of Attributes (QEAA)** by a **QTSP**.

This credential proves that the user controls a specific blockchain account without exposing private keys.

Example claims include:

- blockchain network
- chain identifier
- blockchain account address

The credential is used during the **OpenID4VP authentication flow** to satisfy the **SCA requirements defined in ARF TS12**.

---

## Decentralized Payment Execution

The blockchain transaction is **executed directly by the user** using their **non-custodial crypto wallet**.

Key properties:

- no custody by the payment gateway
- no intermediary executes the blockchain transaction
- the blockchain is used purely as a **settlement layer**

The payment gateway verifies the payment by:

1. receiving the authenticated payment request
2. monitoring the blockchain
3. matching the executed transaction using the shared `transaction_id`

---

# Standards and Protocols

The architecture relies on open standards and EU frameworks including:

### Identity and Wallet Standards

- EUDI Wallet ARF
- OpenID4VP
- OpenID4VCI
- SD-JWT VC

### Payment Authentication

- ARF TS12 – Strong Customer Authentication

TS12 relies on **VC Type Metadata** to render transaction data in the wallet UI.  
Implementations should therefore support **retrieving VC metadata from the `vct` URL**, as wallet rendering may depend on the latest version of the metadata definition.

### Blockchain Standards

- CAIP-2 chain identifiers
- EVM compatible chains
- Tezos
- other compatible DLTs

---

# Regulatory Alignment

The specification is designed to align with European regulatory frameworks including:

### eIDAS 2.0

- EUDI Wallet identity authentication
- Qualified Electronic Attestations of Attributes (QEAA)
- advanced electronic signatures

### MiCA

- identity-assured crypto payments
- compliant merchant acceptance of crypto assets

### TFR (Travel Rule)

- selective disclosure of originator information
- risk-based compliance

### GDPR

- privacy by design
- no personal data written on-chain
- selective disclosure of attributes

---

# Repository Structure

```
Secure_Crypto_P2M_EUDI_Use_Case.md
README.md
```

### Main Documents

**Secure Crypto P2M Use Case**

Detailed architecture and technical specification:

```
Secure_Crypto_P2M_EUDI_Use_Case.md
```

This document describes:

- the payment architecture
- the trust model
- transaction flows
- regulatory positioning
- technical annex with credential examples

---

# Implementation Example

An example implementation of EUDI-compatible crypto wallet integration is available through:

https://altme.io

This implementation demonstrates:

- proof of crypto wallet ownership
- issuance of SCA credentials
- integration with EUDI-compatible wallets
- identity-assured crypto payment flows

---

# Future Extensions

The architecture will continue evolving with support for:

- EVM wallets
- additional blockchain networks
- Digital Euro integration
- expanded merchant credential frameworks

---

# License

This repository provides a **reference specification and implementation guidance** for research and interoperability purposes.

Please refer to individual document headers for detailed licensing information.
