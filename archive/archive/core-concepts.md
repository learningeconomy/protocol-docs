# Core Concepts

## 🧠 Core Concepts

LearnCard is a developer-first, modular wallet that handles **verifiable credentials**, **identity**, and **consent**. To use it effectively, it helps to understand a few foundational ideas. You don’t need to be a blockchain or cryptography expert—we’ve done the heavy lifting for you.

This page gives you the key concepts you’ll see across this documentation.

***

### 🎓 Verifiable Credentials (VCs)

Verifiable Credentials are portable digital statements—like a diploma, badge, or license—that anyone can issue and anyone can verify.

* **Issuer**: The party who creates the credential (e.g. a school, platform, employer).
* **Holder**: The person or agent who owns the credential.
* **Verifier**: Anyone who needs to check that the credential is legit.

LearnCard uses the [W3C VC standard](https://www.w3.org/TR/vc-data-model/) to ensure global interoperability and verification.

***

### 🪪 Decentralized Identifiers (DIDs)

DIDs are unique, cryptographically-verifiable identifiers that aren’t tied to centralized registries.

* They let users prove ownership without relying on usernames or emails.
* LearnCard generates and manages DIDs under the hood.

DIDs are what make trust portable—and private.

***

### 🧰 Wallets

A **wallet** is where credentials live. It:

* Stores verifiable credentials
* Signs and verifies credentials
* Manages identity (via DIDs)
* Handles selective sharing and consent

LearnCard gives you an in-app wallet that can be embedded in your own app, bot, or backend.

***

### 🧾 Consent & Selective Disclosure

Learners and workers own their data. LearnCard supports:

* **Granular consent**: Share only the parts of a record that are needed.
* **ZKPs (Zero-Knowledge Proofs)**: Prove something without revealing everything.
* **BBS+ Signatures**: Enable selective disclosure of credential fields.

This ensures privacy, security, and compliance with data protection best practices.

***

### 🧠 Semantic Memory & Context

LearnCard can integrate with embeddings and vector databases (like Qdrant) to:

* Build persistent memory across interactions
* Improve AI suggestions based on real learning context
* Enable adaptive bots and copilots

This powers personalization at the infrastructure level.

***

### 🛠️ SDK & API Model

Choose your stack:

* `@learncard/core` SDK for programmatic control
* LearnCloud Network API for backend integrations
* LearnCloud Storage API for encrypted storage
* LearnCloud AI API for AI-enabled credential flows
* LearnCard CLI for automation and scripting

LearnCard’s SDK is modular: bring only what you need, scale as you go.

***

### 🔓 Open Standards

Interoperability is built-in. LearnCard supports:

* **Open Badges v3 (OBv3)**
* **Comprehensive Learner Record (CLR)**
* **Learning Tools Interoperability (LTI)**
* **Learning and Employment Records (LER)**
* **Learner Information Framework (LIF)**

***

### ⚡ Boosts

A **Boost** is a superpowered VC. It follows OBv3 and W3C standards but adds:

* **Display metadata**: Control how credentials appear in wallets
* **Governance rules**: Enforce who can issue what
* **Network validation**: Confirm issuance rules were followed
* **Attachments**: Include files, PDFs, or resources

Think of Boosts as **VC+**—fully standards-compliant but better for real-world apps.

***

### 🔐 ConsentFlows

**ConsentFlows** define how data can be read from or written to a user’s wallet—with their explicit permission.

Use ConsentFlow contracts to:

* Request only specific fields from credentials
* Enforce write permissions with fine-grained rules
* Respect data ownership at every step

ConsentFlows power integrations like GameFlow and are especially useful in educational or family contexts.

***

### 🖊️ Signing Authorities

**Signing Authorities** are remote services that sign credentials on behalf of users. They're ideal for:

* Offline flows (e.g. scanning a QR code at an event)
* Headless or delegated signing
* Shared infrastructure for large orgs

You can host your own Signing Authority or use LearnCard’s managed infrastructure.

***

### 📦 Verifiable Presentations

A **Verifiable Presentation (VP)** is a bundle of one or more credentials that a user shares with another party.

* Think of it as a "credential folder" you can pass around
* Can be generated dynamically with selective fields
* Fully verifiable using DIDs and cryptographic proofs

***

### 🔁 DID Authentication

**DID Authentication** lets users prove ownership of their DID to log in or access services.

* Works like OAuth, but self-sovereign
* No passwords or emails needed
* Used across LearnCard to authorize actions

***

### 🌐 LearnCloud Network

The **LearnCloud Network API** lets developers:

* Send and receive credentials, boosts, and presentations
* Create and claim credentials through peer-to-peer or QR flows
* Register and manage Signing Authorities
* Trigger and validate ConsentFlows
* Monitor health and fetch metadata (like DIDs or challenge keys)

It’s the backbone of interaction between LearnCard users and applications.

***

### ☁️ LearnCloud Storage

**LearnCloud** is LearnCard’s end-to-end encrypted storage system:

* Store credentials and presentations securely
* Sync across devices
* Swap in your own storage backend if desired

Data is encrypted client-side. LearnCard never sees private data unless explicitly shared through a consent contract.

***

### ✅ Next Steps

Now that you understand the big ideas:

* 🔗 Jump into [Your First Integration](../../quick-start/your-first-integration.md)
* 🧪 Try a live flow using the [LearnCard CLI](broken-reference)
* 📚 Browse the API Reference
