---
description: A zero to sixty guide
---

# 🦸 Creating a SuperSkills! Issuer

**This guide assumes the following:**

* You have a web application, such as an online learning platform.
* You would like to issue Verifiable Credentials from your platform into [SuperSkills! App](../).
* You would like to follow the major, interoperable standards in the larger ecosystem for issuing credentials between applications!&#x20;

If that all sounds true, let's get started 🎉

### 1**—**Identify what credentials you want to issue.

While there are infinite ways you can customize your unique credential, these are the 4 main fields you will want to tweak for each achievement:

1. **Name**: the primary name for identifying your Verifiable Credential.
2. **Achievement Name**: the granular name for the particular achievement claim in your Verifiable Credential.
3. **Description**: common description of what this achievement represents.
4. **Narrative**: description of how someone earns this achievement.
5. **Image**: a picture representation of this achievement.

```json
// JSON Representation of Achievement
{
    "name": "Achievement Unlocked",
    "achievementName": "Teamwork Achievement",
    "description": "This is a description",
    "criteriaNarrative": "Earned by completing a basic tutorial on our website.",
    "image": "https://www.example.com"
}
```

Ideally, these credentials would be mapped to credential-able items in your platform i.e. for completing a course in your platform.

Once you've established what credentials you would like to issue, you can checkout the [guide for creating new credentials](../../../learn-card-sdk/learncard-core/quick-start/create-new-credentials.md), then return here.&#x20;

### 2**—**Sending credentials from your platform using CHAPI.

On the client side, you will need to prepare your web application for issuing credentials. An easy way to achieve interoperability is to use CHAPI.&#x20;

* [**Install**](../../../learn-card-sdk/learncard-core/quick-start/#install-the-library) [learn-card-core package](../../../learn-card-sdk/learncard-core/quick-start/#install-the-library) from pnpm, yarn, or npm into your project.
* [**Initialize** LearnCard in your web application with CHAPI enabled](../../../learn-card-sdk/learncard-core/chapi/using-learncard-to-interact-with-a-chapi-wallet.md). Reference the[ Issuer cheatsheet for CHAPI.](../../../learn-card-sdk/learncard-core/chapi/cheat-sheets/issuers.md)&#x20;
* **Replace the Test VC** with the `newCredential()` you defined in [step 1](creating-a-superskills-issuer.md#1-identify-what-credentials-you-want-to-issue.).

**You should be able to see the credential inside SuperSkills!** &#x20;

<img src="../../../.gitbook/assets/Screen Shot 2022-12-19 at 4.45.01 PM.png" alt="" data-size="original"><img src="../../../.gitbook/assets/Screen Shot 2022-12-19 at 4.50.04 PM.png" alt="" data-size="original">

### 3**—**Setting Up a Remote Issuer using VC-API (Optional)

At this point, it's up to you where and how you want to create the credential itself. A very common pattern is to host a remote issuer. Our current recommendation is to setup your own VC-API endpoints using the LearnBridge inside the LearnCard SDK for handling this:

* [**Deploy LearnCard Bridge**](../../../learn-card-sdk/learncard-bridge.md) as your VC-API endpoint.&#x20;
* **Configure** your [LearnCard to use your VC-API endpoint](../../../learn-card-sdk/learncard-core/plugins/official-plugins/vc-api.md) upon initialization.
* When you use `learnCard.invoke.storeCredentialViaChapiDidAuth(vc)` to send the signed credential to an interoperable wallet, your LearnCard will now use your VC-API endpoint for signing the Verifiable Credential! ✅

{% hint style="success" %}
Need extra help, or have a question? Engage in our [Github Discussions](https://github.com/learningeconomy/LearnCard/discussions)!&#x20;

* [Post a Feature or Documentation Request ](https://github.com/learningeconomy/LearnCard/discussions/categories/feature-requests)💡
* [Ask for Help](https://github.com/learningeconomy/LearnCard/discussions/categories/help) 💖
* [Show off your project to the community!](https://github.com/learningeconomy/LearnCard/discussions/categories/show-and-tell) 🙌

Don't have access to the Github Discussions yet? Click [here](broken-reference).
{% endhint %}
