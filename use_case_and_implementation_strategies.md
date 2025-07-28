# Use Cases and Implementation Strategies for Stablecoin Transfers with EUDI Compliant Crypto Wallet

- **Version**: 1.0
- **Date**: 28th July 2025
- **Status**: Draft
- **Maintainer**: Altme Identity & Compliance Team

## Table of Contents

1. [Introduction](#introduction)
2. [Use Cases](#use-cases)
   1. [E-Commerce Payments (Retail)](#1-e-commerce-payments-retail)
   2. [Banking & Institutional Services](#2-banking--institutional-services)
   3. [Digital Identity-Linked Payments](#3-digital-identity-linked-payments)
   4. [Cross-Border Remittances](#4-cross-border-remittances)
   5. [Tokenized Financial Products (Flagship Use Case)](#5-tokenized-financial-products-flagship-use-case)
3. [Verifier Implementation Strategies](#verifier-implementation-strategies)
   1. [Key Roles](#1-key-roles)
   2. [Wallet Models](#2-wallet-models)
   3. [Compliance Delegation](#3-compliance-delegation)
   4. [Implementation Scenarios](#4-implementation-scenarios)
      - [Scenario 1 – Verifier = Beneficiary (Self-Custody Model)](#scenario-1--verifier--beneficiary-self-custody-model)
      - [Scenario 2 – Verifier = Vendor (Vendor as Beneficiary Wallet)](#scenario-2--verifier--vendor-vendor-as-beneficiary-wallet)
      - [Scenario 3 – Split Role (Verifier = Vendor + Beneficiary)](#scenario-3--split-role-verifier--vendor--beneficiary)
      - [Scenario 4 – Peer-to-Peer Wallet (Fully Decentralized, No VASP)](#scenario-4--peer-to-peer-wallet-fully-decentralized-no-vasp)
      - [Scenario 5 – Wallet as Endpoint of Notabene Network](#scenario-5--wallet-as-endpoint-of-notabene-network)
      - [Scenario 6 – Wallet via VASP Proxy (Compliance Bridge)](#scenario-6--wallet-via-vasp-proxy-compliance-bridge)
   5. [Comparison Table](#comparison-table)
   6. [Regulatory Recommendations](#regulatory-recommendations)

## Introduction

This document provides guidelines on how **stablecoin transfers** (e.g., **USDC**, **DAI**, **USDT**) can be executed in a **compliant and privacy-preserving manner** using an **EUDI-compatible crypto wallet**.

By combining **EUDI identity credentials** with **self-custodial blockchain transactions**, these guidelines define secure and interoperable payment flows that meet **European regulations** (MiCA, TFR, AMLD6) while enabling **user consent, selective disclosure of identity attributes, and verifiable proofs** of transaction integrity.

The document focuses on two main aspects:

1. **Use Cases** – Practical applications of stablecoin transfers across different industries, with the best-fit verifier models.
2. **Verifier Implementation Strategies** – How verifiers, vendors, and beneficiaries can be structured to ensure compliance, privacy, and operational flexibility.

## Use Cases

## Use Cases

### **1. E-Commerce Payments (Retail)**

**Example Scenario:**
A user buys a new laptop from an online electronics store. At checkout, they scan a QR code with their **EUDI-compliant crypto wallet**, which simultaneously verifies their identity (e.g., age or name) and initiates a **100 USDC stablecoin payment** directly to the merchant’s wallet. The merchant instantly receives the payment along with **cryptographic proof of the user’s identity attributes**—all without exposing sensitive data.

**Key Benefits:**

- **Seamless Checkout:** A single QR code action handles both **payment and identity verification**.
- **Privacy-Preserving Compliance:** Only essential attributes (e.g., “age > 18”) are shared using **SD-JWT selective disclosure**.
- **Lower Costs:** Stablecoin payments **avoid chargebacks and card fees**.
- **Built-In Compliance:** Merchants can connect with **Notabene APIs** for automated Travel Rule compliance.

**Implementation Strategy:**

- **Scenario 1:** Large merchants managing self-custody wallets and compliance directly.
- **Scenario 3:** Merchants outsourcing OIDC4VP flows to a vendor while keeping custody of funds.
- **Scenario 6:** Merchants using a **VASP proxy** for compliance automation.

### **2. Banking & Institutional Services**

**Example Scenario:**
A private bank enables clients to invest in **tokenized bonds** or deposit stablecoins. Clients send funds from their **self-custodial wallet**, along with **verifiable KYC credentials**, to the bank’s smart contract address. The bank validates identity proofs and processes transactions under **MiCA and AMLD6 compliance**.

**Key Benefits:**

- **Full Compliance:** The bank receives **KYC/AML proofs** directly from the wallet.
- **Non-Custodial User Experience:** Funds remain in user control until settlement.
- **Audit-Ready Transactions:** Every payment is **linked to `tx_hash` and KYC data** for regulatory checks.

**Implementation Strategy:**

- **Scenario 1:** Bank acts as both verifier and beneficiary with complete compliance control.
- **Scenario 5:** Banks integrate directly with **Notabene as a wallet endpoint** for cross-bank settlements.

### **3. Digital Identity-Linked Payments**

**Example Scenario:**
A user pays for age-restricted goods (e.g., wine delivery) or a **government service requiring strong ID verification**. The wallet confirms the user’s **age or nationality** and processes the stablecoin payment, sharing **only the required attribute (e.g., “age > 18”)** while keeping sensitive data private.

**Key Benefits:**

- **Frictionless Flow:** Payment and ID verification are completed in a **single step**.
- **Selective Disclosure:** Minimal data is exposed through **SD-JWT proofs**.
- **Regulatory Traceability:** Transactions are linked to verifiable identity claims.

**Implementation Strategy:**

- **Scenario 1:** For agencies or merchants with in-house compliance.
- **Scenario 3:** For vendor-managed OIDC4VP flows.
- **Scenario 6:** When **VASP-based Travel Rule reporting** is needed.

### **4. Cross-Border Remittances**

**Example Scenario:**
A worker in Germany sends **500 USDC** to family in the Philippines. The sender’s wallet attaches **encrypted identity attributes** for **TFR compliance**, and the recipient’s self-custodial wallet receives funds instantly.

**Key Benefits:**

- **No Intermediary Banks:** Payments avoid delays and high SWIFT fees.
- **Travel Rule Compliance:** **Originator and beneficiary data** is securely exchanged.
- **Instant Global Transfers:** Stablecoin rails provide **real-time settlement**.

**Implementation Strategy:**

- **Scenario 5:** Wallet integrates directly with Notabene as a **Travel Rule endpoint**.
- **Scenario 6:** Wallet routes through a **VASP proxy** for regulatory messaging.
- **Scenario 3:** Hybrid approach where a vendor validates identity while funds remain self-custodied.

### **5. Tokenized Financial Products (Flagship Use Case)**

**Example Scenario:**
A bank issues **tokenized bonds or real-world assets (RWA)**. An investor pays **€10,000 USDC** via an EUDI wallet while presenting **verifiable KYC credentials**. Upon payment confirmation, the bank **automatically issues the tokenized asset** to the investor’s wallet.

**Key Benefits:**

- **KYC + Payment Binding:** The payment is **cryptographically linked to the investor’s verified identity**.
- **Instant Token Delivery:** **Stablecoin transfer triggers RWA issuance**.
- **Regulatory Compliance:** Built-in **MiCA and AMLD6 proofs**.

**Implementation Strategy:**

- **Scenario 1:** Bank manages verification and custody directly.
- **Scenario 5:** Bank integrates with Notabene for **cross-border asset issuance**.

## Verifier Implementation Strategies

This EUDI-compliant wallet supports multiple integration models for **identity verification, compliance, and stablecoin transfers**, depending on who manages compliance (beneficiary, vendor, or a VASP network).

### **1. Key Roles**

- **Verifier:** Validates identity proofs (OIDC4VP, SD-JWT, VP tokens) before accepting payment.
  *Example:* A bank verifying the sender’s KYC credentials.
- **Beneficiary:** The recipient of funds (e.g., merchant, corporate, or bank).
  *Example:* A retailer receiving 100 USDC in a self-custodial wallet.
- **Vendor:** A third-party provider managing identity verification or custodial wallets for beneficiaries.
- **VASP (Virtual Asset Service Provider):** A regulated entity (e.g., exchange or custodian) ensuring AML and Travel Rule compliance. Can connect directly to teh wallet or act as a proxy.
- **Compliance Layer (e.g., Notabene):** A Travel Rule network linking VASPs.

  - The wallet can integrate **directly as an endpoint (Scenario 5)** or
  - Use a **VASP proxy for compliance routing (Scenario 6)**.

### **2. Wallet Models**

The **beneficiary wallet** may be:

- **Self-custodial** (owned by the beneficiary),
- **Custodial** (hosted by a vendor),
- **VASP-linked** (connected via Notabene).

### **3. Compliance Delegation**

The verifier role can be:

- **Beneficiary-managed** (Scenario 1),
- **Vendor-managed** (Scenario 2),
- **Split between vendor and beneficiary** (Scenario 3), or
- **Delegated to a VASP network/Notabene** (Scenarios 5 & 6).

### **4. Implementation Scenarios**

The following sections describe **the six main implementation scenarios**, with details on:

- **Who acts as the verifier,**
- **Who controls the wallet,**
- **How Travel Rule and AML compliance are ensured.**

### **Scenario 1 – Verifier = Beneficiary (Self-Custody Model)**

**Roles and Wallet Ownership:**

- The **beneficiary acts as the verifier** and controls the beneficiary wallet.
- All OIDC4VP requests are generated by the beneficiary.

**How It Works:**

- The beneficiary generates the `authorization_request` JWT (OIDC4VP).
- The user’s EUDI wallet provides verifiable presentations (VP tokens and SD-JWT VCs).
- The beneficiary validates the responses and directly receives stablecoins on its self-custody wallet.
- Optionally, the beneficiary may integrate **Notabene as a direct API endpoint** to exchange Travel Rule data if cross-VASP compliance is needed.

**Compliance (TFR & AML):**

- The beneficiary must log:
  - **Payer KYC attributes** (e.g., `given_name`, `family_name`, `birth_date` from the VP token).
  - **Transaction metadata** (`amount`, `currency`, `tx_hash`, and timestamp).
- Logs must be retained in compliance with **TFR** and **AMLD6** requirements.
- **Not a CASP**, since the beneficiary only receives funds on its own wallet.

**Use Case:**

- Large merchants, financial institutions, or regulated businesses with internal compliance teams.


### **Scenario 2 – Verifier = Vendor (Vendor as Beneficiary Wallet)**

**Roles and Wallet Ownership:**

- A **vendor acts as both verifier and beneficiary wallet owner**.
- The vendor controls the wallet receiving the funds and manages OIDC4VP flows.

**How It Works:**

- Vendor issues the OIDC4VP request and validates the VP tokens.
- Stablecoins are transferred from the user to the **vendor’s custodial wallet**.
- Vendor later settles with the beneficiary (off-chain or by transferring stablecoins).
- Vendor can connect to **Notabene** to automate Travel Rule data exchange with other VASPs.

**Compliance (TFR & AML):**

- Vendor is responsible for:
  - Collecting **payer KYC data** via VP tokens.
  - Recording all transaction details (`amount`, `currency`, `tx_hash`, and timestamp).
  - Reporting under **TFR** and AML regulations.
- **Vendor acts as a CASP/VASP**, since it holds custody of user funds.

**Use Case:**

- Smaller or non-technical businesses that outsource crypto handling and compliance.


### **Scenario 3 – Split Role (Verifier = Vendor + Beneficiary)**

**Roles and Wallet Ownership:**

- The **verifier role is shared**:
  - Vendor handles OIDC4VP request creation and session orchestration.
  - Beneficiary owns the wallet receiving stablecoins and performs final data validation.

**How It Works:**

- Vendor issues the `authorization_request` JWT.
- User’s wallet sends stablecoins **directly to the beneficiary wallet** (self-custody).
- The OIDC4VP response (VP token and SD-JWT) is encrypted (JWE) so **only the beneficiary can access sensitive identity data**.
- Vendor may log session metadata but not personal data.
- If required, the vendor or beneficiary can connect to **Notabene as a VASP endpoint** for TFR compliance.

**Compliance (TFR & AML):**

- Beneficiary is responsible for logging:
  - **Payer KYC attributes** (from VP token).
  - **Transaction data** (`tx_hash`, `amount`, etc.).
- Vendor may log **non-sensitive metadata** (e.g., `nonce`, `state`) to provide audit traceability.
- **Not a CASP**, since the vendor never holds funds.

**Use Case:**

- Businesses wanting vendor support for OIDC4VP integration while maintaining custody of funds and privacy.


### **Scenario 4 – Peer-to-Peer Wallet (Fully Decentralized, No VASP)**

**Roles and Wallet Ownership:**

- Both **user and beneficiary have self-custodial wallets**.
- A verifier (beneficiary or a third-party vendor) only **validates compliance and identity proofs**, without holding funds.

**How It Works:**

- OIDC4VP flow is used to exchange identity data (VP tokens, SD-JWT VCs) and link it with the `tx_hash`.
- Stablecoins are transferred **directly from user to beneficiary**.
- **No Notabene or VASP** is involved unless manually added for compliance.

**Compliance (TFR & AML):**

- Beneficiary logs:
  - **Payer identity data** (from VP).
  - Transaction data (`tx_hash`, `amount`, timestamp).
- **No CASP** involved.

**Use Case:**

- DeFi protocols, on-chain services, or **Web3-native flows** prioritizing self-custody and privacy.


### **Scenario 5 – Wallet as Endpoint of Notabene Network**

**Roles and Wallet Ownership:**

- **The EUDI wallet itself is a direct participant in the Notabene network.**
- The wallet integrates with **Notabene APIs** to handle Travel Rule data exchange.

**How It Works:**

1. The wallet initiates a payment and prepares **Travel Rule metadata** (e.g., originator data from SD-JWT).
2. This data is **sent directly to Notabene**, which routes it to the receiving VASP or endpoint.
3. Funds are transferred **directly wallet-to-wallet**, but compliance data flows via Notabene.

**Compliance (TFR & AML):**

- The wallet acts like a **"light VASP node"** and must implement AML/TFR data exchange logic.
- PII is encrypted and transmitted via **Notabene’s SafePII** system.

**Use Case:**

- Advanced EUDI wallets or institutional crypto wallets that need **direct regulatory compliance** without intermediaries.


### **Scenario 6 – Wallet via VASP Proxy (Compliance Bridge)**

**Roles and Wallet Ownership:**

- **The EUDI wallet remains self-custodial** for funds.
- A **VASP acts as a compliance middleware**, relaying Travel Rule data to Notabene but **does not hold or manage the funds**.

**How It Works:**

1. The EUDI wallet executes the payment and shares SD-JWT credentials.
2. The wallet calls the **VASP Proxy API**, which:
   - Validates OIDC4VP proofs,
   - Packages Travel Rule data,
   - Sends it to the **Notabene network**.
3. Funds are transferred **directly wallet-to-wallet**, while the **VASP proxy logs compliance metadata**.

**Compliance (TFR & AML):**

- The VASP ensures Travel Rule data exchange and logging.
- The wallet stays **non-custodial** but gains **compliance interoperability** through the proxy.

**Use Case:**

- Wallets that want to remain **non-custodial** but need **compliance automation** for cross-border or regulated flows.



### **Comparison Table**


| Scenario                                 | Verifier Role              | Beneficiary Wallet Owner | CASP/VASP Risk   | TFR Compliance Responsibility  |
| ------------------------------------------ | ---------------------------- | -------------------------- | ------------------ | -------------------------------- |
| **1. Verifier = Beneficiary**            | Beneficiary                | Beneficiary              | Low              | Beneficiary                    |
| **2. Verifier = Vendor**                 | Vendor                     | Vendor                   | Vendor = CASP    | Vendor                         |
| **3. Split Role (Vendor + Beneficiary)** | Vendor + Beneficiary       | Beneficiary              | Low              | Beneficiary (Vendor logs meta) |
| **4. Peer-to-Peer Wallet**               | Beneficiary or Third-party | Beneficiary              | None             | Beneficiary                    |
| **5. Wallet as Endpoint (Notabene)**     | Wallet + Notabene          | Beneficiary              | Medium (as node) | Wallet (via Notabene APIs)     |
| **6. Wallet via VASP Proxy**             | VASP (Compliance API)      | Beneficiary              | Low (no custody) | VASP Proxy                     |



### **Regulatory Recommendations**

- **For advanced wallets with full compliance needs:**
  Use **Scenario 5 (Wallet as Endpoint)** for direct Notabene integration.
- **For self-custody wallets preferring simplicity:**
  Use **Scenario 6 (VASP Proxy)** to delegate Travel Rule message handling.
- **For decentralized Web3 flows:**
  **Scenario 4 (Pure P2P)** is suitable but may not meet TFR obligations.
- **Scenarios 1, 2, and 3** remain useful for **merchants, banks, and regulated institutions** with varying levels of vendor or self-hosted compliance.
