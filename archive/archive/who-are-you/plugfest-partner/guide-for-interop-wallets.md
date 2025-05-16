---
description: How LearnCard Bridge can issue into your wallet.
---

# Guide for Interop Wallets

{% hint style="info" %}
This guide is tailored for **Wallet** participants in the [**JFF Interoperability Plugfest 2**](https://w3c-ccg.github.io/vc-ed/plugfest-2-2022/)**.** If you are a participant in Plugfest, but not sure you are in the right place, make sure you've read our [Plugfest Partner guide](./). If you're not sure what Plugfest is, or how you got here, you should start [here](../../../../). 🚀
{% endhint %}

This guide will walk you through everything you need to claim a credential into your wallet application from the LearnCard Bridge issuer for the purposes of JFF Plugfest 2.&#x20;

This guide is divided between the two core protocols aligned with Plugfest that LearnCard supports: [VC-API](https://w3c-ccg.github.io/vc-api/)/[CHAPI](https://w3c-ccg.github.io/credential-handler-api/) & [OIDC](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html)—follow the guide for the protocol(s) your wallet application supports.&#x20;

### VC-API/CHAPI

1. If your wallet application **already supports VC-API/CHAPI**, then we should already be interoperable! After you've registered your wallet application in CHAPI, you can navigate to the[ CHAPI Playground](https://playground.chapi.io/issuer):&#x20;
   1. Click the "gear" icon: <img src="../../../../.gitbook/assets/Screen Shot 2022-09-29 at 11.07.25 AM.png" alt="" data-size="line">
   2. Select "LearnCard Bridge" as the Issuer Service, and enable DID Auth.&#x20;
   3. Click "Generate Verifiable Credential"&#x20;
   4. Click "Store in Wallet" and select your Wallet. Then, claim your credential.
   5. If all went well, you should be able to see the credential issued in your wallet application. Success! ✅ 🎉
2. If your wallet application **does not yet support CHAPI.** Start [here](../../../../tutorials/explore-advanced-topics/chapi/chapi-wallet-setup-guide.md). Reference the [Wallet cheatsheet for CHAPI.](../../../../tutorials/explore-advanced-topics/chapi/cheat-sheets/wallets.md) After you have implemented, return and do steps in #1 above.

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
