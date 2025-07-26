# Use Cases and Implementation Strategies for Stablecoin Transfer with EUDI Compliant Wallet

- **Version**: 1.0
- **Date**: 26th July 2025
- **Status**: Draft
- **Maintainer**: Altme Identity & Compliance Team

## Table of Contents

1. [Introduction](#introduction)
2. [Use Cases and Implementation Strategies](#use-cases-and-implementation-strategies)
   - [E-Commerce Payments (Retail)](#1-e-commerce-payments-retail)
   - [Banking & Institutional Services](#2-banking--institutional-services)
   - [Digital Identity-Linked Payments](#3-digital-identity-linked-payments)
   - [DeFi & Web3 Services](#4-defi--web3-services)
   - [Cross-Border Remittances](#5-cross-border-remittances)
   - [Loyalty and Reward Programs](#6-loyalty-and-reward-programs)
   - [B2B Settlements & Supply Chain Payments](#7-b2b-settlements--supply-chain-payments)
   - [Tokenized Financial Products (Flagship Use Case)](#8-tokenized-financial-products-flagship-use-case)
   - [Use Case and Verifier Strategy Mapping](#use-case--verifier-strategy-matrix)
3. [Verifier Implementation Strategies](#verifier-implementation-strategies)
   - [Scenario 1 – Verifier = Beneficiary (Self-Custody Model)](#scenario-1--verifier--beneficiary-self-custody-model)
   - [Scenario 2 – Verifier = Vendor (Vendor as Beneficiary Wallet)](#scenario-2--verifier--vendor-vendor-as-beneficiary-wallet)
   - [Scenario 3 – Split Role (Verifier = Vendor + Beneficiary)](#scenario-3--split-role-verifier--vendor--beneficiary)
   - [Scenario 4 – Vendor Gateway (Verifier and Wallet Fully Outsourced)](#scenario-4--vendor-gateway-verifier-and-wallet-fully-outsourced)
   - [Scenario 5 – Peer-to-Peer Wallet (Verifier Separate, Wallets User-Controlled)](#scenario-5--peer-to-peer-wallet-verifier-separate-wallets-user-controlled)
   - [Comparison Table](#comparison-table)
   - [Regulatory Recommendations](#regulatory-recommendations)

---

## Introduction

This document provides guidelines on how **stablecoin transfers** (e.g., **USDC**, **DAI**, **USDT**) can be executed in a **compliant and privacy-preserving manner** using an **EUDI-compatible wallet**.

By combining **EUDI identity credentials** with **self-custodial blockchain transactions**, these guidelines define secure and interoperable payment flows that meet **European regulations** (MiCA, TFR, AMLD6) while enabling **user consent, selective disclosure of identity attributes, and verifiable proofs** of transaction integrity.

The document focuses on two main aspects:

1. **Use Cases and Implementation Strategies** – Practical applications of stablecoin transfers across different industries, with the best-fit verifier models.
2. **Verifier Implementation Strategies** – How verifiers, vendors, and beneficiaries can be structured to ensure compliance, privacy, and operational flexibility.

---

## Use Cases

### **1. E-Commerce Payments (Retail)**

**Example Scenario:**
A user buys a new laptop from an online electronics store. During checkout, they scan a QR code with their **EUDI-compatible wallet**, which simultaneously verifies their identity (e.g., age or name) and initiates a **100 USDC** stablecoin payment directly to the merchant’s wallet.
The entire flow happens in seconds without requiring the user to enter sensitive payment details on the merchant’s website.

**Key Benefits:**

- **Seamless Checkout:** The QR code triggers the **EUDI wallet** for both payment and identity verification.
- **AML/KYC Compliance:** Only essential data (e.g., name or age) is disclosed via **SD-JWT**.
- **Fast Settlement:** Stablecoin transfers eliminate chargebacks and high card fees.

**Implementation Strategy:**

- **Scenario 1**: For large merchants managing their own compliance and self-custody wallet.
- **Scenario 3**: For merchants relying on a **vendor** to handle OIDC4VP flows but keeping direct custody of funds.

---

### **2. Banking & Institutional Services**

**Example Scenario:**
A private bank offers high-net-worth clients the ability to invest in **tokenized bonds** or **deposit stablecoins**. A user initiates a payment from their self-custodial wallet, presenting **verifiable KYC credentials** during the process.
The bank, acting as both verifier and beneficiary, receives the funds directly while ensuring all transactions are compliant with **MiCA and AMLD6** regulations.

**Key Benefits:**

- **Regulatory Compliance:** The bank acts as verifier, receiving **KYC/AML proofs** directly from the wallet.
- **Non-Custodial Transfers:** Users retain control of funds until payment settlement.
- **Audit-Ready:** Every payment is linked to a verifiable proof (`tx_hash` + KB JWT).

**Implementation Strategy:**

- **Scenario 1**: Bank acts as both verifier and beneficiary, fully controlling compliance.

---

### **3. Digital Identity-Linked Payments**

**Example Scenario:**
A user wants to purchase age-restricted goods, such as wine delivery, or pay for a government service requiring strong identity verification.
The EUDI wallet verifies the user’s **age or citizenship** and processes the stablecoin payment in a single flow, disclosing only the required attributes (e.g., “age > 18”) without revealing sensitive personal information.

**Key Benefits:**

- **Single Flow:** Payment and age verification happen in one step.
- **Selective Disclosure:** Only “age over 18” is shared, **not full DOB**.
- **Regulatory Traceability:** Payments are linked to disclosed attributes and `tx_hash`.

**Implementation Strategy:**

- **Scenario 1**: For in-house verifier setups (retailers or government).
- **Scenario 3**: For vendor-assisted OIDC4VP with beneficiary self-custody.

---

### **4. DeFi & Web3 Services**

**Example Scenario:**
A decentralized autonomous organization (DAO) wants only verified users to participate in staking or voting.
Members use their EUDI wallet to provide **selective KYC credentials** while proving ownership of their blockchain accounts, ensuring that only trusted, compliant participants can interact with the protocol.

**Key Benefits:**

- **Decentralized Verification:** The DAO acts as verifier but never touches user funds.
- **Compliance Layer:** On-chain identity proofs (SD-JWT for account ownership) allow regulatory access control.
- **Self-Custody:** Users sign payments and staking transactions themselves.

**Implementation Strategy:**

- **Scenario 5**: DAO or Web3 app operates as a verifier without holding funds.

---

### **5. Cross-Border Remittances**

**Example Scenario:**
A worker in Germany wants to send **500 USDC** to family in the Philippines without waiting days for a bank transfer.
The sender uses their EUDI wallet to share identity details and authorize the payment, while the recipient instantly receives the funds in their self-custodial wallet, all in full compliance with EU TFR rules.

**Key Benefits:**

- **No Intermediary Custody:** Stablecoins move **P2P from sender to receiver**.
- **Compliance by Design:** AML and TFR compliance ensured via SD-JWT & KB JWT proofs.
- **Low Fees & Instant Settlement:** Avoids SWIFT delays and remittance fees.

**Implementation Strategy:**

- **Scenario 5**: For direct wallet-to-wallet transfers.
- **Scenario 3**: For hybrid services using vendor verification.

---

### **6. Loyalty and Reward Programs**

**Example Scenario:**
A retail chain issues **USDC-based loyalty points** that can be redeemed across all partner stores.
When a customer redeems points, their EUDI wallet verifies their identity, ensuring the rewards are tied to legitimate accounts and cannot be fraudulently reused.

**Key Benefits:**

- **Fraud Prevention:** Rewards are bound to verified user identity (e.g., EUDI credentials).
- **Instant Redemption:** Users can spend or transfer tokens without intermediaries.
- **Turnkey Setup:** Vendor manages compliance and payments if merchants lack technical expertise.

**Implementation Strategy:**

- **Scenario 2 or 4**: Vendor manages verification, custody, and redemption.

---

### **7. B2B Settlements & Supply Chain Payments**

**Example Scenario:**
A European manufacturer pays **€50,000 USDC** to an Asian supplier.
The supplier’s corporate identity is verified via SD-JWT, and the payment is settled instantly on-chain, replacing the lengthy, expensive process of cross-border bank transfers.

**Key Benefits:**

- **Instant Cross-Border Settlement:** No intermediary banks needed.
- **Legal Entity Verification:** Supplier’s corporate identity verified via SD-JWT.
- **Full Audit Compliance:** Transaction logs are tied to corporate KYC.

**Implementation Strategy:**

- **Scenario 1**: Both parties manage compliance and use self-custody wallets.

---

### **8. Tokenized Financial Products (Flagship Use Case)**

**Example Scenario:**
A bank offers tokenized bonds or real-world assets (RWA) to retail investors.
A customer pays **€10,000 USDC** through their EUDI wallet, simultaneously presenting KYC credentials. Once the payment is confirmed, the bank issues the tokenized asset directly to the customer’s blockchain address.

**Key Benefits:**

- **Payment + KYC Binding:** The EUDI wallet shares KYC claims and links them to the payment `tx_hash`.
- **Real-Time Settlement:** Stablecoin payment triggers instant token issuance.
- **Regulatory-Grade Proof:** All actions are logged per MiCA and AMLD6.

**Implementation Strategy:**

- **Scenario 1**: Bank acts as verifier and beneficiary with full control.

---

### **Use Case and Verifier Strategy Mapping**


| Use Case                                | Recommended Verifier Strategy |
| ----------------------------------------- | ------------------------------- |
| **1. E-Commerce Payments**              | Scenario 1 or Scenario 3      |
| **2. Banking & Institutional Services** | Scenario 1                    |
| **3. Digital Identity-Linked Payments** | Scenario 1 or Scenario 3      |
| **4. DeFi & Web3 Services**             | Scenario 5                    |
| **5. Cross-Border Remittances**         | Scenario 5 or Scenario 3      |
| **6. Loyalty & Reward Programs**        | Scenario 2 or Scenario 4      |
| **7. B2B Settlements & Supply Chain**   | Scenario 1                    |
| **8. Tokenized Financial Products**     | Scenario 1                    |

---

## Verifier Roles and Implementation Models

In the payment architecture, three roles can exist:

- **Verifier** – The entity initiating and validating the OIDC4VP request and verifying SD-JWT and VP tokens.
- **Beneficiary** – The final recipient of the funds (e.g., a merchant).
- **Vendor** – A third-party service provider that can act as a verifier, hold the beneficiary’s wallet, or provide compliance and verification as a service.

The **beneficiary wallet** is the blockchain wallet that receives the stablecoin transfer.This wallet can be:

- **Owned by the beneficiary** (self-custody), or
- **Owned by a vendor** (custodial model).

The verifier role may be:

- Performed **entirely by the beneficiary**,
- Delegated to the **vendor**, or
- **Split between both**.

Below are the **main implementation scenarios**.

### **Scenario 1 – Verifier = Beneficiary (Self-Custody Model)**

**Roles and Wallet Ownership:**

- The **beneficiary acts as the verifier** and controls the beneficiary wallet.
- All OIDC4VP requests are generated by the beneficiary.

**How It Works:**

- The beneficiary generates the `authorization_request` JWT (OIDC4VP).
- The user’s wallet provides verifiable presentations (VP tokens and SD-JWT VCs).
- The beneficiary validates the responses and directly receives stablecoins on its self-custody wallet.

**Compliance (TFR & AML):**

- The beneficiary must log:
  - **Payer KYC attributes** (e.g., `given_name`, `family_name`, `birth_date` from the VP token).
  - **Transaction metadata** (`amount`, `currency`, `tx_hash`, and timestamp).
- Logs must be retained in compliance with **TFR** and **AMLD6** requirements.
- **Not a CASP**, since the beneficiary only receives funds on its own wallet.

**Use Case:**

- Large merchants, financial institutions, or regulated businesses with their own compliance teams.

### **Scenario 2 – Verifier = Vendor (Vendor as Beneficiary Wallet)**

**Roles and Wallet Ownership:**

- A **vendor acts as both verifier and beneficiary wallet owner**.
- The vendor controls the wallet receiving the funds and manages OIDC4VP flows.

**How It Works:**

- Vendor issues the OIDC4VP request and validates the VP tokens.
- Stablecoins are transferred from the user to the **vendor’s custodial wallet**.
- Vendor later settles with the beneficiary (off-chain or by transferring stablecoins).

**Compliance (TFR & AML):**

- Vendor is responsible for:
  - Collecting **payer KYC data** via VP tokens.
  - Recording all transaction details (`amount`, `currency`, `tx_hash`, and timestamp).
  - Reporting under **TFR** and AML regulations.
- **Vendor acts as a CASP/VASP**, since it holds custody of user funds.

**Use Case:**

- Smaller or non-technical businesses that outsource both crypto handling and compliance.

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

**Compliance (TFR & AML):**

- Beneficiary is responsible for logging:
  - **Payer KYC attributes** (from VP token).
  - **Transaction data** (`tx_hash`, `amount`, etc.).
- Vendor may log **non-sensitive metadata** (e.g., `nonce`, `state`) to provide audit traceability.
- **Not a CASP**, since the vendor never holds funds.

**Use Case:**

- Businesses wanting vendor support for OIDC4VP integration while maintaining custody of funds and privacy.

### **Scenario 4 – Vendor Gateway (Verifier and Wallet Fully Outsourced)**

**Roles and Wallet Ownership:**

- Vendor acts as both the **verifier and the beneficiary wallet owner**, managing the entire OIDC4VP and payment flow.

**How It Works:**

- Vendor generates the OIDC4VP request, verifies identity and blockchain proofs, and receives stablecoins on its custodial wallet.
- Vendor provides a **payment confirmation callback** or webhook to the beneficiary.
- Beneficiary does not directly interact with the blockchain.

**Compliance (TFR & AML):**

- Vendor logs and reports all **TFR-required data** and AML checks.
- Beneficiary relies entirely on vendor reports for audits.
- **Vendor is a CASP/VASP** (full custody).

**Use Case:**

- Businesses that require a "turnkey" crypto payment solution with fiat conversion.

### **Scenario 5 – Peer-to-Peer Wallet (Verifier Separate, Wallets User-Controlled)**

**Roles and Wallet Ownership:**

- Both **user and beneficiary have self-custodial wallets**.
- A verifier (beneficiary or a third-party vendor) only **validates compliance and identity proofs**, without holding funds.

**How It Works:**

- OIDC4VP flow is used to exchange identity data (VP tokens, SD-JWT VCs) and link it with the `tx_hash`.
- Stablecoins are transferred **directly from user to beneficiary**.

**Compliance (TFR & AML):**

- Beneficiary logs:
  - **Payer identity data** (from VP).
  - Transaction data (`tx_hash`, `amount`, timestamp).
- **No CASP** involved, since no third party holds funds.

**Use Case:**

- Decentralized, privacy-preserving payments with direct wallet-to-wallet transfers.

### **Comparison Table**


| Scenario                                 | Verifier Role              | Beneficiary Wallet Owner | CASP/VASP Risk | TFR Compliance Responsibility  |
| ------------------------------------------ | ---------------------------- | -------------------------- | ---------------- | -------------------------------- |
| **1. Verifier = Beneficiary**            | Beneficiary                | Beneficiary              | Low            | Beneficiary                    |
| **2. Verifier = Vendor**                 | Vendor                     | Vendor                   | Vendor = CASP  | Vendor                         |
| **3. Split Role (Vendor + Beneficiary)** | Vendor + Beneficiary       | Beneficiary              | Low            | Beneficiary (Vendor logs meta) |
| **4. Vendor Gateway**                    | Vendor                     | Vendor                   | Vendor = CASP  | Vendor                         |
| **5. Peer-to-Peer Wallet**               | Beneficiary or Third-party | Beneficiary              | None           | Beneficiary                    |

### **Regulatory Recommendations**

- **For full privacy and compliance control:**

  - Use **Scenario 1 (Verifier = Beneficiary)** or **Scenario 3 (Split Model)**.
  - Both ensure the beneficiary directly controls the wallet and TFR records.
- **For fast integration with minimal technical work:**

  - Use **Scenario 2 (Verifier = Vendor)** or **Scenario 4 (Vendor Gateway)**.
  - Ensure the vendor is **CASP-compliant** and AML reporting is contractually covered.
- **For decentralized, CASP-free flows:**

  - Use **Scenario 5 (Peer-to-Peer Wallet)** with direct wallet-to-wallet transfers and OIDC4VP proofs for TFR data exchange.
