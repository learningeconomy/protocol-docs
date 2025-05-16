# Table of contents

## 🚀 Introduction

* [What is LearnCard?](README.md)
* [Use Cases & Possibilities](introduction/use-cases-and-possibilities.md)
* [Ecosystem Architecture](introduction/ecosystem-architecture.md)

## ⚡ Quick Start

* [Setup & Prerequisites](quick-start/setup-and-prerequisites.md)
* [Your First Integration](quick-start/your-first-integration.md)

## 🧠 Core Concepts

* [Identities & Keys](core-concepts/identities-and-keys/README.md)
  * [Decentralized Identifiers (DIDs)](core-concepts/identities-and-keys/decentralized-identifiers-dids.md)
  * [Seed Phrases](core-concepts/identities-and-keys/seed-phrases.md)
  * [Network Profiles](core-concepts/identities-and-keys/network-profiles.md)
* [Credentials & Data](core-concepts/credentials-and-data/README.md)
  * [Verifiable Credentials (VCs)](core-concepts/credentials-and-data/verifiable-credentials-vcs.md)
  * [Credential Lifecycle](core-concepts/credentials-and-data/credential-lifecycle.md)
  * [Schemas, Types, & Categories](core-concepts/credentials-and-data/achievement-types-and-categories.md)
  * [Building Verifiable Credentials](core-concepts/credentials-and-data/building-verifiable-credentials.md)
  * [Boost Credentials](core-concepts/credentials-and-data/boost-credentials.md)
  * [Getting Started with Boosts](core-concepts/credentials-and-data/getting-started-with-boosts.md)
  * [Credential URIs](core-concepts/credentials-and-data/uris.md)
  * [xAPI Data](core-concepts/credentials-and-data/xapi-data.md)
  * [General Best Practices & Troubleshooting](core-concepts/credentials-and-data/general-best-practices-and-troubleshooting.md)
* [Consent & Permissions](core-concepts/consent-and-permissions/README.md)
  * [ConsentFlow Overview](core-concepts/consent-and-permissions/consentflow-overview.md)
  * [Consent Contracts](core-concepts/consent-and-permissions/consent-contracts.md)
  * [User Consent & Terms](core-concepts/consent-and-permissions/user-consent-and-terms.md)
  * [Consent Transactions](core-concepts/consent-and-permissions/consent-transactions.md)
  * [Auto-Boosts](core-concepts/consent-and-permissions/auto-boosts.md)
  * [Writing Consented Data](core-concepts/consent-and-permissions/writing-consented-data.md)
  * [Accessing Consented Data](core-concepts/consent-and-permissions/accessing-consented-data.md)
* [Network & Interactions](core-concepts/network-and-interactions/README.md)
  * [Network Vision & Principles](core-concepts/network-and-interactions/network-vision-and-principles.md)
  * [Key Network Procedures](core-concepts/network-and-interactions/key-network-procedures.md)
  * [Core Interaction Workflows](core-concepts/network-and-interactions/core-interaction-workflows.md)
  * [Signing Authorities](core-concepts/network-and-interactions/signing-authorities.md)
* [Architecture & Principles](core-concepts/architecture-and-principles/README.md)
  * [Control Planes](core-concepts/architecture-and-principles/control-planes.md)
  * [Plugin System](core-concepts/architecture-and-principles/plugins.md)
  * [Auth Grants and API Tokens](core-concepts/architecture-and-principles/auth-grants-and-api-tokens.md)

## 📚 Tutorials

* [Use Core Features](tutorials/use-core-features/README.md)
  * [Create a Credential](tutorials/use-core-features/create-a-credential.md)
  * [Create a Boost](tutorials/use-core-features/create-a-boost.md)
  * [Create a Verified Issuer](tutorials/use-core-features/create-a-verified-issuer.md)
  * [Create a ConsentFlow](tutorials/use-core-features/create-a-consentflow.md)
  * [Use xAPI Statements](tutorials/use-core-features/sending-xapi-statements.md)
  * [Listen to Webhooks](tutorials/use-core-features/listen-to-webhooks.md)
  * [Connect a Game](tutorials/use-core-features/gameflow.md)
* [Build Examples](tutorials/build-examples/README.md)
  * [Issue Badges from a Website](tutorials/build-examples/issue-badges-from-a-website.md)
  * [Connect an LMS](tutorials/build-examples/connect-an-lms.md)
  * [Connect a Bot](tutorials/build-examples/connect-a-bot.md)
  * [Connect AI Tutor](tutorials/build-examples/connect-ai-tutor.md)
  * [Connect AI Agent](tutorials/build-examples/connect-ai-agent.md)
  * [Login with LearnCard](tutorials/build-examples/login-with-learncard.md)
  * [Access Wallet Data](tutorials/build-examples/access-wallet-data.md)
  * [Embed a Wallet](tutorials/build-examples/embed-a-wallet.md)
* [Explore Advanced Topics](tutorials/explore-advanced-topics/README.md)
  * [Implement Remote Key Management](tutorials/explore-advanced-topics/managing-seed-phrases.md)
  * [Build a Plugin](tutorials/explore-advanced-topics/the-simplest-plugin.md)
  * [Generate API Tokens](tutorials/explore-advanced-topics/generate-api-tokens.md)
  * [Claim Data after Guardian Consent](tutorials/explore-advanced-topics/claim-data-after-guardian-consent.md)
  * [Use CHAPI](tutorials/explore-advanced-topics/chapi/README.md)
    * [⭐ CHAPI Wallet Setup Guide](tutorials/explore-advanced-topics/chapi/chapi-wallet-setup-guide.md)
    * [↔️ Translating to CHAPI documentation](tutorials/explore-advanced-topics/chapi/translating-to-chapi-documentation.md)
    * [🖥️ Demo Application](tutorials/explore-advanced-topics/chapi/demo-application.md)
    * [🔰 Using LearnCard to Interact with a CHAPI Wallet](tutorials/explore-advanced-topics/chapi/using-learncard-to-interact-with-a-chapi-wallet.md)
    * [📝 Cheat Sheets](tutorials/explore-advanced-topics/chapi/cheat-sheets/README.md)
      * [Issuers](tutorials/explore-advanced-topics/chapi/cheat-sheets/issuers.md)
      * [Wallets](tutorials/explore-advanced-topics/chapi/cheat-sheets/wallets.md)
  * [Deploy Your Own Network](tutorials/explore-advanced-topics/deploy-your-own-network.md)
  * [Connect a Website to Independent Network](tutorials/explore-advanced-topics/connect-a-website-to-independent-network.md)
  * [Delegate Credential Issuance](tutorials/explore-advanced-topics/delegate-credential-issuance.md)

## 🛠️ SDKs & API Reference <a href="#sdks" id="sdks"></a>

* [LearnCloud Network API](sdks/learncard-network/README.md)
  * [Authentication](sdks/learncard-network/authentication.md)
  * [Usage Examples](sdks/learncard-network/usage-examples.md)
  * [Architecture](sdks/learncard-network/architecture.md)
  * [Notifications & Webhooks](sdks/learncard-network/notifications.md)
  * ```yaml
    type: builtin:openapi
    props:
      models: true
    dependencies:
      spec:
        ref:
          kind: openapi
          spec: learn-card-network-api
    ```
  * [OpenAPI](https://network.learncard.com/docs#/)
* [LearnCloud Storage API](sdks/learncloud-storage-api/README.md)
  * [Authentication](sdks/learncloud-storage-api/authentication.md)
  * [Usage Examples](sdks/learncloud-storage-api/usage-examples.md)
  * [Architecture](sdks/learncloud-storage-api/architecture.md)
  * ```yaml
    type: builtin:openapi
    props:
      models: true
    dependencies:
      spec:
        ref:
          kind: openapi
          spec: learn-cloud-storage-openapi
    ```
  * [xAPI Reference](sdks/learncloud-storage-api/xapi-reference.md)
* [LearnCloud AI API](sdks/learncloud-ai-api/README.md)
  * [Authentication](sdks/learncloud-ai-api/authentication.md)
  * [Core Concepts](sdks/learncloud-ai-api/core-concepts.md)
  * [Usage Examples](sdks/learncloud-ai-api/usage-examples.md)
  * [API Reference](sdks/learncloud-ai-api/api-reference.md)
* [LearnCard App API](sdks/learncard-app-api.md)
* [LearnCard Wallet SDK](sdks/learncard-core/README.md)
  * [Usage Examples](sdks/learncard-core/construction.md)
  * [Architecture](sdks/learncard-core/architecture.md)
  * [SDK Reference](https://api.docs.learncard.com/docs/core/modules)
  * [Plugin API Reference](sdks/learncard-core/writing-plugins.md)
  * [Integration Strategies](sdks/learncard-core/architectural-patterns.md)
  * [Deployment](sdks/learncard-core/production-deployment-guide.md)
  * [Troubleshooting](sdks/learncard-core/troubleshooting-guide.md)
  * [Changelog](sdks/learncard-core/migration-guide.md)
* [Plugins](sdks/official-plugins/README.md)
  * [Crypto](sdks/official-plugins/crypto.md)
  * [DIDKit](sdks/official-plugins/didkit.md)
  * [DID Key](sdks/official-plugins/did-key.md)
  * [Dynamic Loader](sdks/official-plugins/dynamic-loader.md)
  * [VC](sdks/official-plugins/vc/README.md)
    * [Expiration Sub-Plugin](sdks/official-plugins/vc/expiration-sub-plugin.md)
  * [VC-Templates](sdks/official-plugins/vc-templates.md)
  * [VC-API](sdks/official-plugins/vc-api.md)
  * [Ceramic](sdks/official-plugins/ceramic.md)
  * [IDX](sdks/official-plugins/idx.md)
  * [VPQR](sdks/official-plugins/vpqr.md)
  * [Ethereum](sdks/official-plugins/ethereum.md)
  * [CHAPI](sdks/official-plugins/chapi.md)
  * [LearnCard Network](sdks/official-plugins/learncard-network.md)
  * [LearnCloud](sdks/official-plugins/learncloud.md)
  * [LearnCard](sdks/official-plugins/learncard.md)
  * [Claimable Boosts](sdks/official-plugins/claimable-boosts.md)
* [LearnCard CLI](sdks/learncard-cli.md)

## 🔗 Development

* [Github](https://github.com/learningeconomy/LearnCard)
* [Service Status](https://status.learncloud.ai/)
* [Roadmap](development/roadmap.md)
* [Support](development/custom-development.md)
* [Contributing](development/contributing.md)

## 💀 ARCHIVE

* [Archive](archive/archive/README.md)
  * [⭐ Who are you?](archive/archive/who-are-you/README.md)
    * [Learners & Employees](archive/archive/who-are-you/learners-and-employees.md)
    * [Traditional Educator](archive/archive/who-are-you/traditional-educator.md)
    * [Non-Traditional Educator](archive/archive/who-are-you/non-traditional-educator.md)
    * [Assessment Provider](archive/archive/who-are-you/assessment-provider.md)
    * [Employer](archive/archive/who-are-you/employer.md)
    * [App Developer & EdTech](archive/archive/who-are-you/app-developer-and-edtech.md)
    * [DAO & Communities](archive/archive/who-are-you/dao-and-communities.md)
    * [Content Creators](archive/archive/who-are-you/content-creators.md)
    * [Research Institutions](archive/archive/who-are-you/research-institutions.md)
    * [NGOs & Governments](archive/archive/who-are-you/ngos-and-governments.md)
    * [Plugfest Partner](archive/archive/who-are-you/plugfest-partner/README.md)
      * [Guide for Interop Issuers](archive/archive/who-are-you/plugfest-partner/guide-for-interop-issuers/README.md)
        * [🤽 Creating an Interop Issuer](archive/archive/who-are-you/plugfest-partner/guide-for-interop-issuers/creating-an-interop-issuer.md)
      * [Guide for Interop Wallets](archive/archive/who-are-you/plugfest-partner/guide-for-interop-wallets.md)
  * [Protocol Overview](archive/archive/protocol-overview/README.md)
    * [The Internet of Education](archive/archive/protocol-overview/the-internet-of-education.md)
    * [The Learning Economy](archive/archive/protocol-overview/the-learning-economy.md)
    * [Learner & Employee Privacy](archive/archive/protocol-overview/learner-and-employee-privacy.md)
    * [22nd Century Education](archive/archive/protocol-overview/22nd-century-education.md)
    * [PVCs](archive/archive/protocol-overview/pvcs.md)
  * [🔌 Connect Your Application](archive/archive/connect-your-application.md)
  * [Discord Bot](archive/archive/discord-bot.md)
  * [LearnCard Bridge](archive/archive/learncard-bridge.md)
  * [Boost Credentials](archive/archive/understanding-boosts.md)
  * [Create New Credentials](archive/archive/create-new-credentials.md)
  * [Sign & Send Credentials](archive/archive/sign-and-send-credentials.md)
  * [VC Resolution](archive/archive/vc-resolution.md)
  * [UX SDK Reference](archive/archive/learncard-ux/README.md)
    * [Quick Start](archive/archive/learncard-ux/quick-start.md)
    * [Components](archive/archive/learncard-ux/components/README.md)
      * [Verifiable Credentials](archive/archive/learncard-ux/components/verifiable-credentials/README.md)
        * [VC Thumbnail](archive/archive/learncard-ux/components/verifiable-credentials/vc-thumbnail.md)
        * [VC Thumbnail, Mini](archive/archive/learncard-ux/components/verifiable-credentials/vc-thumbnail-mini.md)
      * [LearnCards](archive/archive/learncard-ux/components/learncards/README.md)
        * [LearnCard Front](archive/archive/learncard-ux/components/learncards/learncard-front.md)
        * [LearnCard Back](archive/archive/learncard-ux/components/learncards/learncard-back.md)
    * [API](https://api.docs.learncard.com/docs/react/modules)
  * [Credential Networks](archive/archive/the-open-credential-network.md)
  * [Core Concepts](archive/archive/core-concepts.md)
  * [ConsentFlow OLD](archive/archive/consentflow.md)
  * [IDX Config](archive/archive/idx-config.md)
