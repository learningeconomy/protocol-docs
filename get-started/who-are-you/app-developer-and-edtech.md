---
description: How to add LearnCard to your existing apps, services, and platforms!
---

# App Developer & EdTech

If you are an app developer, ed-tech provider, or systems architect and are interested in understanding how LearnCard can augment your existing platform—you've come to the right place! :wrench:

This guide will walk you through everything you need to get started. Baseline experience and familiarity with software development tooling and processes is expected. No prior knowledge of decentralized identity or verifiable credentials necessary.

First things first: you need to identify your use case. **Why are you interested in using LearnCard in the first place?**

### Some common use cases:

* :mortar\_board:**Courses**: users complete courses and curriculum in your platform or app, and you are interested in issuing achievements, skills, learning certificates, IDs, and more that can be recognized in the broader ecosystem. _Start_ [_here_](app-developer-and-edtech.md#1-sign-and-send-credentials-in-your-platform)_._
* :handshake: **Hiring:** candidates search for work opportunities and/or hiring managers validate job applications in your platform, and you are interested in streamlining the verification process of credentials from many different sources inside an ecosystem. _Start_ [_here_](app-developer-and-edtech.md#2-accept-and-verify-credentials-in-your-platform)_._
* :unlock:**Gated Content:** you want to enable your users to gate content based on the validation of specific credentials—community membership, skills, achievements, accomplishments, endorsements, etc. _Start_ [_here_](app-developer-and-edtech.md#2-accept-and-verify-credentials-in-your-platform)_._
* :ballot\_box\_with\_check: **Proof-of-progress:** you want to integrate verifiable progress within your platform, such as credentials issues for completing a task [list](app-developer-and-edtech.md#1-sign-and-send-credentials-in-your-platform). &#x20;
* :credit\_card: **Identity:** you want to enable your users to anchor verifiable, decentralized identities with your platform. _Start_ [_here_](app-developer-and-edtech.md#1-sign-and-send-credentials-in-your-platform)_._
* :video\_game: **Metaverse & Games:** you want to integrate LearnCard into your digital experiences and games, enabling issuing, recognition, and/or validation of credentials within your ecosystem. Start [here](app-developer-and-edtech.md#1-sign-and-send-credentials-in-your-platform).

### **Are you using LearnCard?**

_We'd love to hear to hear from you! Share your story in our_[ _Github Discussions_](https://github.com/learningeconomy/LearnCard/discussions/categories/show-and-tell)_, or send us an email at_ [_community@learningeconomy.io_](mailto:community@learningeconomy.io)_—we'd love to feature your work 🙌._

## Quick Start

These are some of the most common and quickest ways to get started.

### #1—Sign & Send Credentials in Your Platform

The easiest way to sign and send credentials from your platform, is to leverage the **LearnCard Network.**

As an App Developer, if you want to sign and send credentials using the LearnCard Network Plugin, follow the steps below. This guide assumes you have already set up the LearnCard SDK and the LearnCard Network Plugin in your platform.

{% content-ref url="../../learncard-services/learncard-network/" %}
[learncard-network](../../learncard-services/learncard-network/)
{% endcontent-ref %}

### Step 1: Create Your Service Profile in the LearnCard Network

&#x20;Follow the instructions in "Connect Your Application" to setup your platform's DID, register your service profile, and connect to the LearnCard Network.

{% content-ref url="../../learncard-services/learncard-network/connect-your-application.md" %}
[connect-your-application.md](../../learncard-services/learncard-network/connect-your-application.md)
{% endcontent-ref %}

Then, ensure you have initialized the [LearnCard Network Plugin ](../../learncard-services/learncard-network/)with your platform's configuration.

```javascript
import { initNetworkLearnCard } from '@learncard/network-plugin';
import didkit from '@learncard/core/dist/didkit/didkit_wasm_bg.wasm?url';

const networkLearnCard = await initNetworkLearnCard({
    seed,
    didkit,
});
```

### Step 2: Set up the Credential Template

Create a credential template that specifies the type of credential you want to issue. In this example, we'll use `UniversityDegreeCredential`.

```javascript
const credentialTemplate = {
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  type: ["VerifiableCredential", "UniversityDegreeCredential"],
  issuer: "did:example:12345", // Your platform's DID
  credentialSubject: {
    id: "did:example:abcde", // Recipient's DID
    degree: {
      type: "BachelorDegree",
      name: "Bachelor of Science and Arts"
    }
  }
};
```

For more info on [creating credential templates, click here](../../learn-card-sdk/learncard-core/quick-start/create-new-credentials.md).

### Step 3: Sign & Issue the Credential

First, determine who you are sending your credential to. If you followed the flow for connecting your application, you can retrieve users who have granted you permission to send them credentials:

```typescript
const connections = await networkLearnCard.invoke.getConnections();

// This is just an example to get a user you are connected with. 
const recipient = connections[0];

// Make sure you insert the recipients DID as the credentialSubject.id
credentialTemplate.credentialSubject.id = recipient.did;
```

To sign the credential, use the LearnCard SDK's [`learnCard.invoke.issueCredential()`](../../learn-card-sdk/learncard-core/quick-start/sign-and-send-credentials.md) function, passing the credential template and your platform's DID as parameters.

```javascript
const signedCredential = await networkLearnCard.invoke.issueCredential(credentialTemplate);
```

This will return a signed credential object that includes a proof generated by your platform's DID.

### Step 4: Send the Credential

Next, use the `sendCredential()` method provided by the LearnCard Network Plugin to send the signed credential to the recipient.

```javascript
const sendResult = await networkLearnCard.invoke.sendCredential(signedCredential, recipient.profileId);
```

By following these steps, you can sign and send credentials to users within your platform using the LearnCard Network Plugin.

Alternatively, given your specific use case, you may not want to leverage the LearnCard Network for sending credentials from your platform. In that case, you have several options!&#x20;

* [Deploy your own federated LearnCard Network node](../../learncard-services/learncard-network/learncard-network-api/launch-your-own-network.md)**:** have full control over the exchange network while remaining fully interoperable with the total ecosystem!
* &#x20;[Setup your own VC-API Issuer by following these steps](plugfest-partner/guide-for-interop-issuers/creating-an-interop-issuer.md).&#x20;
* Or, you can [reach out to us for support and custom development to help connect your Institution](../../community/custom-development.md).

{% hint style="info" %}
Note: these options are not mutually exclusive! For example, you can use your existing or new VC-API compliant issuer within the LearnCard Network to send and sign VCs and handle key material. Or, you could launch your own Network node and use your own VC-API.
{% endhint %}

{% content-ref url="../../community/custom-development.md" %}
[custom-development.md](../../community/custom-development.md)
{% endcontent-ref %}

### #2—Accept & Verify Credentials in Your Platform&#x20;

### Accepting and Verifying Credentials in a Hiring Platform

In a hiring platform, you want to streamline the verification process of candidates' credentials from various sources within an ecosystem. You can achieve this using the CHAPI (Credential Handler API) and the LearnCard SDK. The following steps outline how an App Developer can accept and verify credentials in their platform using CHAPI and LearnCard SDK.

### Accepting Credentials using CHAPI

1. Import the CHAPI Polyfill into your platform based on your development environment. You can either use the script tag method for vanilla JavaScript or import the polyfill library in Node.js.
2. Construct a Verifiable Presentation Request using the desired credential types (e.g., `UniversityDegreeCredential` for a job application).
3. Wrap the Verifiable Presentation Request in a Web Credential Query, allowing your platform to request credentials from a user's digital wallet.
4. Request a Web Credential using the `navigator.credentials.get(credentialQuery)` function. The user will be prompted to present the requested credentials from their digital wallet.
5. Handle null results, which can occur when the user denies the request or does not have a wallet installed. As a developer, decide how to handle these situations by offering fallback mechanisms, retry options, or alternate paths.

See the [full CHAPI documentation for verifiers here](https://chapi.io/developers/verifiers).

### Verifying Credentials using LearnCard SDK

1. After receiving the credentials from the user's wallet, use the LearnCard SDK's [`learnCard.invoke.verifyCredential(signedVc)`](../../learn-card-sdk/learncard-core/quick-start/accept-and-verify-credentials.md) function to verify the received credentials.
2. Check the results of the verification to ensure the validity of the credentials. The result will contain an array of objects with status, check, and message properties.
3. If the verification is successful, proceed with the next steps in the hiring process. Otherwise, handle the failed verification case by either requesting the user to provide valid credentials or implementing any other suitable action.

By integrating CHAPI and LearnCard SDK into your hiring platform, you can create a seamless and secure process for accepting and verifying candidate credentials from various sources within the ecosystem. This will not only streamline the verification process but also provide added security and trust in the credentials presented by the candidates.

{% content-ref url="../../learn-card-sdk/learncard-core/quick-start/accept-and-verify-credentials.md" %}
[accept-and-verify-credentials.md](../../learn-card-sdk/learncard-core/quick-start/accept-and-verify-credentials.md)
{% endcontent-ref %}

### #3—Display Credentials in Your Platform&#x20;

{% content-ref url="../../learn-card-sdk/learncard-ux/" %}
[learncard-ux](../../learn-card-sdk/learncard-ux/)
{% endcontent-ref %}

### #4—Build a Plugin to Connect Your Platform

{% content-ref url="../../learn-card-sdk/learncard-core/plugins/writing-plugins/" %}
[writing-plugins](../../learn-card-sdk/learncard-core/plugins/writing-plugins/)
{% endcontent-ref %}

### #5—Build a Bot or Service for Your Platform

{% content-ref url="../../learncard-services/build-your-own-service.md" %}
[build-your-own-service.md](../../learncard-services/build-your-own-service.md)
{% endcontent-ref %}

## Advanced

Sometimes you need more than the basic, out-of-the-box flows because you have a complex community or use case. That's great! All of our tooling is fully pluggable and open-source, so with a little elbow grease and developer time, you should be able to accomplish your goals.

{% hint style="warning" %}
**Need additional development assistance?** We're here to [help](../../community/custom-development.md).&#x20;
{% endhint %}

## Coming Soon

These features aren't yet available, but they are coming soon on our roadmap—never too early to get excited!&#x20;

### LearnBank

* :money\_with\_wings: **Earn-and-learn:** you want to enable incentivized learning within your platform on a specific topic, or even incentivize people to learn _about_ your platform.&#x20;
* :moneybag: **Skill Bounties:** you want to enable users on your platform to fund and claim micro-scholarships for demonstrating specific skills. &#x20;
* :tools: **Work Bounties:** you want to enable users on your platform to fund and claim payments for demonstrating completed work.

### LearnGraph

* :bar\_chart: **Skills Dashboards:** add support in your platform for visualizing skills, achievements, and opportunities data to enhance learning outcomes.&#x20;
