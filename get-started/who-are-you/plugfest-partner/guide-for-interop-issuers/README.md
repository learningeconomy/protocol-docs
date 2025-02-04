---
description: How to issue from your issuing platform into our LearnCard app.
---

# Guide for Interop Issuers

{% hint style="info" %}
This guide is tailored for **Issuer** participants in the [**JFF Interoperability Plugfest 2**](https://w3c-ccg.github.io/vc-ed/plugfest-2-2022/)**.** If you are a participant in Plugfest, but not sure you are in the right place, make sure you've read our [Plugfest Partner guide](../). If you're not sure what Plugfest is, or how you got here, you should start [here](../../../../). 🚀
{% endhint %}

This guide will walk you through everything you need to **Issue credentials from your issuing platform into the LearnCard app for the purposes of JFF Plugfest 2.** This guide is divided between the two core protocols aligned with Plugfest that LearnCard supports: [VC-API](https://w3c-ccg.github.io/vc-api/)/[CHAPI](https://w3c-ccg.github.io/credential-handler-api/) & [OIDC](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html)—follow the guide for the protocol(s) your issuing platform supports.&#x20;

### VC-API/CHAPI

1. If your issuing platform **already supports VC-API/CHAPI**, then we should already be interoperable! Open up the [LearnCard app](../../../../learn-card-examples/learncard.md), register it as a wallet, then try issuing from your platform and verify you can claim the Verifiable Credential in the LearnCard app. The[ CHAPI Playground](https://playground.chapi.io/issuer) is a great place to test as well (Contact [Digital Bazaar/Veres ](https://veres.io/contact/)to add yourself as an issuer).&#x20;
2. If your issuing platform supports VC-API, **but does not yet support CHAPI.** Start [here](../../../../learn-card-sdk/learncard-core/chapi/using-learncard-to-interact-with-a-chapi-wallet.md)—then replace the test VC with the signed credential from your VC-API. Reference the[ Issuer cheatsheet for CHAPI.](../../../../learn-card-sdk/learncard-core/chapi/cheat-sheets/issuers.md)
3. If your issuing platform supports CHAPI, **but does not yet support VC-API.** You will need to [setup a VC-API endpoint](../../../../learn-card-sdk/learncard-core/learncard-bridge.md) to sign the Credential before passing it to CHAPI _(🚧 coming soon)._&#x20;
4. If your issuing platform **does not yet support VC-API or CHAPI**. You will need to do #2 & #3. For a zero to sixty guide on this—start [here](creating-an-interop-issuer.md).

{% hint style="success" %}
Need extra help, or have a question? Engage in our [Github Discussions](https://github.com/learningeconomy/LearnCard/discussions)!&#x20;

* [Post a Feature or Documentation Request ](https://github.com/learningeconomy/LearnCard/discussions/categories/feature-requests)💡
* [Ask for Help](https://github.com/learningeconomy/LearnCard/discussions/categories/help) 💖
* [Show off your project to the community!](https://github.com/learningeconomy/LearnCard/discussions/categories/show-and-tell) 🙌

Don't have access to the Github Discussions yet? Click [here](broken-reference).
{% endhint %}

### OIDC

> 🚧 Guide coming soon

{% hint style="warning" %}
We are currently part of a working group (organized by Spruce & Crossword) amongst a subset of the Plugfest participants to finalize key collaboration logistics for demonstrating interop through OIDC. The working group is focused on the [OIDC4VCI Issuing Profile](https://docs.google.com/document/d/1d6KH9UOqc5vbliPt-WTqv3qS2ssVTRERPH7oNzfu_3k/edit) and [NGI Resources](https://ngiatlantic.info/). Reach out to us at[ sdk@learningeconomy.io](mailto:sdk@learningeconomy.io) if you would like to be involved!&#x20;
{% endhint %}
