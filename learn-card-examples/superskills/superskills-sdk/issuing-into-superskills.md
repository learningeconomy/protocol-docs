---
description: How to issue from your issuing platform into our SuperSkills! app.
---

# Issuing into SuperSkills!

This guide will walk you through everything you need to **Issue credentials from your issuing platform into the SuperSkills! app.**&#x20;

{% hint style="warning" %}
**SuperSkills! App & SDK are in early beta** - for the SuperSkills! App to be able to receive credentials from your issuer, you will need to be in a trusted issuer registry to prevent malicious issuers. Additionally, at this time, your user will need to be granted special priveleges to see the "Enable 3rd Party Credentials" button. Send us an email at [sdk@learningeconomy.io](mailto:sdk@learningeconomy.io) to get verified and start issuing!
{% endhint %}

### The Credential Handler API—"CHAPI"&#x20;

The easiest way to sign and send credentials from your platform into the SuperSkills app is to take advantage of the[ "Credential Handler API", or CHAPI](https://chapi.io/).&#x20;

* If your issuing platform **already supports CHAPI**, then you're platform is already enabled to send credentials!
  1. Open up the [SuperSkills! App ](../)
     * If you are on web, you will need to open up your profile, and click "Enable 3rd Party Credentials."
     * The Web application will walk you through registering SuperSkills! as a recognized digital wallet in your browser.
  2. Then, try issuing from your platform and verify you can claim the Verifiable Credential in the SuperSkills! app. The[ CHAPI Playground](https://playground.chapi.io/issuer) is a great place to test as well.
* If your issuing platform **does not yet support CHAPI, or you have no idea what we are talking about.** [Start here](creating-a-superskills-issuer.md).

{% content-ref url="creating-a-superskills-issuer.md" %}
[creating-a-superskills-issuer.md](creating-a-superskills-issuer.md)
{% endcontent-ref %}

{% hint style="success" %}
Need extra help, or have a question? Engage in our [Github Discussions](https://github.com/learningeconomy/LearnCard/discussions)!&#x20;

* [Post a Feature or Documentation Request ](https://github.com/learningeconomy/LearnCard/discussions/categories/feature-requests)💡
* [Ask for Help](https://github.com/learningeconomy/LearnCard/discussions/categories/help) 💖
* [Show off your project to the community!](https://github.com/learningeconomy/LearnCard/discussions/categories/show-and-tell) 🙌

Don't have access to the Github Discussions yet? Click [here](broken-reference).
{% endhint %}
