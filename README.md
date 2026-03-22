# Secure Crypto Payments with the EUDI Wallet

Last update: March 2026

This repository provides a **reference architecture and specification** describing how the **European Digital Identity Wallet (EUDI Wallet)** enables **secure, identity-verified crypto-asset payments** while preserving the decentralized nature of blockchain settlement.

The primary scenario described is a **person-to-merchant (P2M) crypto payment**, where a natural person pays a merchant using a **self-custodial crypto wallet or smart contract wallet**, while the **EUDI Wallet provides identity, authentication, and transaction authorization**.

The architecture demonstrates how **identity-assured crypto payments** can be implemented in alignment with European regulatory frameworks including:

- **eIDAS 2.0**
- **MiCA**
- **GDPR**
- **EUDI ARF TS12 Strong Customer Authentication**

while ensuring that intermediaries **do not act as Payment Initiation Service Providers (PISPs)**.

# 📄 Specification Document

The complete specification is available here:

- **[Secure Crypto P2M Payments Using the EUDI Wallet](Secure_Crypto_P2M_EUDI_Use_Case.md)**

# Overview

The growth of **digital assets, stablecoins, and decentralized finance** is transforming digital commerce. However, large-scale adoption in Europe requires solutions that combine:

- regulatory compliance
- strong authentication
- privacy-preserving identity verification
- interoperability with the **European Digital Identity framework**

This project shows how **EUDI Wallets and crypto wallets** interact to enable **secure, user-controlled blockchain payments**.

# Supported Execution Models

Two execution models are supported:

### 1. Direct Wallet Model (EOA)

- The user signs and submits the transaction directly
- No intermediary relays or submits transactions
- Fully user-driven execution

### 2. Smart Contract Wallet Model

- The user generates a **transaction authorization in the EUDI Wallet**
- A **smart contract wallet enforces execution**
- A relay (optionally the gateway) may broadcast the transaction

> In both models, no intermediary initiates or controls the payment.

# Architecture Principles

The architecture strictly separates:

- **identity verification**
- **payment authorization**
- **transaction execution**

This ensures:

- user sovereignty
- non-custodial design
- regulatory clarity

# Identity and Authentication

The **EUDI Wallet** acts as the **identity and consent layer**.

It enables the user to:

- authenticate using **PID or equivalent credentials**
- present **Proof of Crypto Account Ownership**
- review transaction details (merchant, amount, address)
- provide **explicit consent**
- generate **cryptographically bound authorization**

Authentication follows **Strong Customer Authentication (SCA)** under **EUDI ARF TS12**.

# Payment Execution

Execution is always **user-driven and deterministic**:

- via a **self-custodial wallet (EOA)**, or
- via a **smart contract wallet**

This guarantees:

- no custody by intermediaries
- no delegated execution control
- full user ownership of funds

# Payment Gateway Role (Non-PISP)

The payment gateway acts strictly as a **verification and orchestration layer**.

Its responsibilities include:

- generating payment requests
- acting as a **Relying Party (OpenID4VP)**
- verifying identity and authorization
- optionally relaying transactions
- monitoring blockchain settlement

The gateway:

- **does not hold funds**
- **does not sign transactions**
- **does not initiate payments**
- **does not control execution**

Where it relays transactions, this is a **technical broadcast function only**.

# Architecture — Dual Wallet Model

In this model, the user directly signs and submits the blockchain transaction.

The gateway verifies identity and orchestrates the flow but is **not involved in transaction submission**.

![Direct Wallet Architecture](dual_wallet.png)

# Architecture — Smart Contract Wallet Model

In this model:

- the user generates a **signed transaction authorization in the EUDI Wallet**
- the **smart contract wallet verifies and executes**
- a relay may broadcast the transaction

The gateway may act as a relay, but:

- it does not initiate the transaction
- it does not control execution
- it only transmits a **user-authorized transaction package**

![Smart Contract Wallet Architecture](smart_contract_wallet.png)

# Roles and Actors

## Payer (Natural Person)

The payer:

- holds an **EUDI Wallet**
- holds a **self-custodial or smart contract wallet**
- possesses identity credentials (PID)
- holds a **Proof of Crypto Account Ownership credential**

The payer:

- authenticates via the EUDI Wallet
- authorizes the transaction
- executes or triggers execution

## Merchant (Legal Person)

The merchant:

- provides goods or services
- exposes a receiving wallet address
- may provide verifiable identity credentials

## Payment Gateway

The gateway:

- orchestrates payment flows
- verifies identity and authorization
- optionally relays transactions
- monitors settlement

It **never acts on behalf of the user to initiate payment**.

## Blockchain Network

The blockchain acts as a **neutral settlement layer**.

Supported networks may include:

- Ethereum and EVM-compatible chains
- Tezos
- other DLTs

# Strong Customer Authentication (TS12)

Strong Customer Authentication is achieved using:

- **Proof of Crypto Account Ownership credentials**
- issued as **Qualified Electronic Attestations of Attributes (QEAA)**
- by a **Qualified Trust Service Provider (QTSP)**

During authentication, the user presents:

- identity credential (PID)
- crypto account ownership credential

The EUDI Wallet binds these to the transaction and produces a **verifiable presentation**.

# Trust Model

Trust is established through:

### Identity Layer

- EUDI Wallet authentication

### Authorization Layer

- cryptographic binding of user consent

### Settlement Layer

- blockchain execution

# Regulatory Alignment

The architecture aligns with:

### eIDAS 2.0

- EUDI Wallet
- QEAA
- advanced signatures

### MiCA

- compliant crypto-asset payments

### TFR

- selective disclosure

### GDPR

- privacy-by-design
- no personal data on-chain

# PSD2 / PSD3 Interpretation

This architecture is designed to **avoid qualification as a Payment Initiation Service Provider (PISP)**.

Specifically:

- no third-party initiation of payments
- no access to user credentials
- no control over execution
- no discretionary role in transaction processing

Transaction submission (when performed by a relay) is a **purely technical function** and does not constitute payment initiation.

# Future Extensions

Possible extensions include:

- person-to-person payments
- merchant-to-merchant flows
- legal entity wallets
- Digital Euro integration

# Contributing

Contributions are welcome to improve:

- architecture
- regulatory alignment
- interoperability
