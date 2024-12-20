---
description: Using LearnCard to cultivate open, cross-border ecosystems!
---

# NGOs & Governments

If you're an NGO or a government, and are interested in understanding how LearnCard can help to minimize complexity and streamline your processes—you've come to the right place! :tada:

This guide will walk you through everything you need to get started. No prior experience required.

First things first: you need to identify your use case. **Why are you interested in using LearnCard in the first place?**&#x20;

### Some common use cases:

* &#x20;**🪪 IDs:** you want to issue a verifiable ID for your citizens. _Start_ [_here_](ngos-and-governments.md#1-issue-credentials-in-your-community)_._
* &#x20;**⛑ Professional Licenses:** you want to issue a verifiable licenses for professions. _Start_ [_here_](ngos-and-governments.md#1-issue-credentials-in-your-community)_._
* :white\_check\_mark: **Verification:** you want to verify IDs, licenses, skills, learning certificates, achievements, or another credential that a citizen presents to you. Start [here](ngos-and-governments.md#2-verify-credentials-from-your-agencies).
* **🕊 Cultivate an Ecosystem:** you want to solve equity, skills, and mobility gaps in your state or nation. Start [here](ngos-and-governments.md#3-support-open-interoperable-ecosystems-with-policy).

### **Are you using LearnCard?**

_We'd love to hear to hear from you! Share your story in our_[ _Github Discussions_](https://github.com/learningeconomy/LearnCard/discussions/categories/show-and-tell)_, or send us an email at_ [_community@learningeconomy.io_](mailto:community@learningeconomy.io)_—we'd love to feature your work 🙌._

## Quick Start

These are some of the most common and quickest ways to get started.&#x20;

### #&#x31;**—Issue IDs from your Agencies**

To **issue credentials to your citizens** this, you can either [setup your own, interoperable Issuer by following these steps](plugfest-partner/guide-for-interop-issuers/creating-an-interop-issuer.md), or you can [reach out to us for support and custom development to help connect your Agencies](../../resources/custom-development.md).

{% content-ref url="plugfest-partner/guide-for-interop-issuers/creating-an-interop-issuer.md" %}
[creating-an-interop-issuer.md](plugfest-partner/guide-for-interop-issuers/creating-an-interop-issuer.md)
{% endcontent-ref %}

{% content-ref url="../../resources/custom-development.md" %}
[custom-development.md](../../resources/custom-development.md)
{% endcontent-ref %}

### **#2—Verify Credentials from your Agencies**

In a government platform, you want to streamline the verification process of citizens' credentials for various use cases like IDs, professional licenses, verification of presented credentials, and cultivating an ecosystem to solve equity, skills, and mobility gaps. You can achieve this using the CHAPI (Credential Handler API) and the LearnCard SDK. The following steps outline how an App Developer can accept and verify credentials in their platform using CHAPI and LearnCard SDK.

### Accepting Credentials using CHAPI

1. Import the CHAPI Polyfill into your platform based on your development environment. You can either use the script tag method for vanilla JavaScript or import the polyfill library in Node.js.
2. Construct a Verifiable Presentation Request using the desired credential types (e.g., GovernmentIDCredential for issuing a verifiable ID to citizens).
3. Wrap the Verifiable Presentation Request in a Web Credential Query, allowing your platform to request credentials from a user's digital wallet.
4. Request a Web Credential using the `navigator.credentials.get(credentialQuery)` function. The user will be prompted to present the requested credentials from their digital wallet.
5. Handle null results, which can occur when the user denies the request or does not have a wallet installed. As a developer, decide how to handle these situations by offering fallback mechanisms, retry options, or alternate paths.

See the full CHAPI documentation for verifiers [here](https://chapi.io/developers/verifiers).

### Verifying Credentials using LearnCard SDK

1. After receiving the credentials from the user's wallet, use the LearnCard SDK's [`learnCard.invoke.verifyCredential(signedVc)`](../../learn-card-sdk/learncard-core/quick-start/accept-and-verify-credentials.md) function to verify the received credentials.
2. Check the results of the verification to ensure the validity of the credentials. The result will contain an array of objects with status, check, and message properties.
3. If the verification is successful, proceed with the next steps specific to the use case (e.g., granting professional licenses or verifying presented credentials). Otherwise, handle the failed verification case by either requesting the user to provide valid credentials or implementing any other suitable action.

By integrating CHAPI and LearnCard SDK into your government platform, you can create a seamless and secure process for accepting and verifying citizen credentials for various use cases. This will not only streamline the verification process but also provide added security and trust in the credentials presented by citizens, enhancing overall public services and facilitating the cultivation of a thriving ecosystem in your state or nation.

### #&#x33;**—Support Open, Interoperable Ecosystems with Policy**&#x20;

> 🚧 Coming soon
