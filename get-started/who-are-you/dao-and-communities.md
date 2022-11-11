---
description: Using LearnCard to supercharge your DAO or community!
---

# DAO & Communities

If you participate in a DAO, and are interested in understanding how LearnCard can augment your community—you've come to the right place! :tada:

This guide will walk you through everything you need to get started. No prior experience required.

First things first: you need to identify your use case. **Why are you interested in using LearnCard in the first place?**&#x20;

### **Some common use cases:**

* ****:trophy: **Achievements:** you want to recognize your members when they do cool or significant stuff in your community. _Start_ [_here_](dao-and-communities.md#1-issue-credentials-in-your-community)_._
* ****:mortar\_board: **Courses:** you want to issue skills, learning certificates, achievements, and more when members of your community progress through your curriculum. _Start_ [_here_](dao-and-communities.md#1-issue-credentials-in-your-community)_._
* ****:thumbsup: **Endorsements:** you want to enable or accept peer-to-peer endorsements within your community. _Start_ [_here_](dao-and-communities.md#1-issue-credentials-in-your-community)_._
* ****:unlock: **Gated Content:** you want to unlock content or channels in your community based on the achievement of specific credentials. _Start_ [_here_](dao-and-communities.md#2-verify-credentials-in-your-community)_._
* ****:white\_check\_mark: **Proof of Membership:** you want to issue proof of membership in your community. _Start_ [_here_](dao-and-communities.md#1-issue-credentials-in-your-community)_._
* ****:handshake: **Hiring:** you want to verify skills, endorsements, and reputation when hiring people in and outside of your community.  _Start_ [_here_](dao-and-communities.md#2-verify-credentials-in-your-community)_._
* ****:credit\_card: **Identity & KYC:** you want to verify identity of members or potential members. _Start_ [_here_](dao-and-communities.md#2-verify-credentials-in-your-community)_._

### **Are you using LearnCard?**

_We'd love to hear to hear from you! Share your story in our_[ _Github Discussions_](https://github.com/learningeconomy/LearnCard/discussions/categories/show-and-tell)_, or send us an email at_ [_community@learningeconomy.io_](mailto:community@learningeconomy.io)_—we'd love to feature your work 🙌._

## Quick Start

These are some of the most common and quickest ways to get started.&#x20;

### #1**—Issue Credentials in your Community**

Great! You've decided that you would like to issue credentials in your community—achievements, skills, learning certificates, endorsements, identities, etc.&#x20;

#### First, you need to **identify what service, bot, or app you will use to issue your credentials.**

Flip through the tabs to learn more about each option:&#x20;

{% tabs %}
{% tab title="Discord Bot" %}
If your community already lives in Discord, one of the easiest ways to get started is to use our Discord bot.&#x20;

If you haven't already, **follow the instructions to get the Discord bot setup in your community,** then come back here!

{% content-ref url="../../learncard-services/discord-bot.md" %}
[discord-bot.md](../../learncard-services/discord-bot.md)
{% endcontent-ref %}
{% endtab %}

{% tab title="LearnCard App" %}
For peer-to-peer credential issuing, it's often easy to use the LearnCard app itself!

If you haven't already, get setup with LearnCard, then return here!

{% content-ref url="../../learn-card-examples/learncard.md" %}
[learncard.md](../../learn-card-examples/learncard.md)
{% endcontent-ref %}
{% endtab %}

{% tab title="Metamask Snap" %}
If your community heavily uses Metamask, there are ways to enable issuance flows through Metamask.

{% hint style="warning" %}
**Experimental:** Metamask Snaps is in early beta with Consensys. Snaps, to date, can only be installed in the experimental [Metamask Flask ](https://metamask.io/flask/) - this is only required for _issuing_ credentials. Normal Metamask users may use regular Metamask to _claim_ credentials.&#x20;
{% endhint %}

If you haven't already, **follow the instructions to get Metamask setup in your community,** then come back here!

{% content-ref url="../../learncard-services/metamask-snap.md" %}
[metamask-snap.md](../../learncard-services/metamask-snap.md)
{% endcontent-ref %}
{% endtab %}
{% endtabs %}

#### Second, you need to _identify what credentials you will be issuing._

If you are using the VCTemplatesPlugin (enabled by default with LearnCard), there are a variety of default credential templates to help you get started quickly! **** Flip through the tabs to see some default options, and what information you will need to compile: ****&#x20;

{% tabs %}
{% tab title="Achievement" %}
There are 4 main fields you will want for each achievement:

1. **Title**: the main way of identifying your achievement e.g. "Achievement Unlocked"
2. **Description**: common description of what this achievement represents.
3. **Narrative**: description of how someone earns this achievement.
4. **Image**: a picture representation of this achievement.

```json
// JSON Representation of Achievement
{
    "title": "Achievement Unlocked",
    "description": "This is a description",
    "narrative": "Earned by completing a basic tutorial on our website.",
    "image": "https://www.example.com"
}
```
{% endtab %}

{% tab title="Learning Completion" %}
Coming soon.
{% endtab %}

{% tab title="Skill" %}
Coming soon.
{% endtab %}

{% tab title="ID" %}
Coming soon.
{% endtab %}

{% tab title="Custom" %}
Coming soon.
{% endtab %}
{% endtabs %}

Check out the VC-Templates plugin for more options:

{% content-ref url="../../learn-card-sdk/learncard-core/plugins/official-plugins/vc-templates.md" %}
[vc-templates.md](../../learn-card-sdk/learncard-core/plugins/official-plugins/vc-templates.md)
{% endcontent-ref %}

#### Third, you need to configure your issuing platform to use your credential templates.

{% tabs %}
{% tab title="Discord Bot" %}
Use the `/create-credential` command. It will open a modal and walk you through creating a credential template, with first-class support for achievements, learning completions, skills, and IDs.
{% endtab %}

{% tab title="LearnCard App" %}
Coming soon.
{% endtab %}

{% tab title="Metamask Snap" %}
Coming soon.
{% endtab %}
{% endtabs %}

#### Then, start issuing credentials!

{% tabs %}
{% tab title="Discord Bot" %}
Use the `/send-credential @<user>` command to start issuing credentials to your members.&#x20;

It will prompt you to select one of your credential templates from [Step 3](dao-and-communities.md#third-you-need-to-configure-your-issuing-platform-to-use-your-credential-templates.). Then, the LearnCard bot will send a direct message to your community member with steps on how they can claim their shiny new credential! :sparkles:
{% endtab %}

{% tab title="LearnCard App" %}
Coming soon.
{% endtab %}

{% tab title="Metamask Snap" %}
Coming soon.
{% endtab %}
{% endtabs %}

### **#2—Verify Credentials in your Community**

> 🚧 Coming soon

{% hint style="info" %}
**Did we miss your use case?** We'd love to chat and hear what you are working on to see how we can help. Post a question to our developer community, the Super Skills League, or shoot us an email at [sdk@learningeconomy.io](mailto:sdk@learningeconomy.io). &#x20;
{% endhint %}

## Advanced

Sometimes you need more than the basic, out-of-the-box flows because you have a complex community or use case. That's great! All of our tooling is fully pluggable and open-source, so with a little elbow grease and developer time, you should be able to accomplish your goals.

{% hint style="warning" %}
**Don't have your own developers?** We're here to [help](../../super-skills-league/custom-development.md).&#x20;
{% endhint %}

### **Build Your Own Bot**

Does your community use a platform not yet supported? Let's change that:

{% content-ref url="../../learncard-services/build-your-own-service.md" %}
[build-your-own-service.md](../../learncard-services/build-your-own-service.md)
{% endcontent-ref %}

### **Build Your Own Plugin**

Do you have a unique requirement, such as supporting a specific DID method, protocol, or system? You might need to build your own plugin:

{% content-ref url="../../learn-card-sdk/learncard-core/plugins/writing-plugins/" %}
[writing-plugins](../../learn-card-sdk/learncard-core/plugins/writing-plugins/)
{% endcontent-ref %}

## Coming Soon

These features aren't yet available, but they are coming soon on our roadmap—never to early too get excited!&#x20;

### LearnBank

* &#x20;**** :money\_with\_wings: **Earn-and-learn:** you want to incentivize learning in your community on a specific topic, or even incentivize people to learn _about_ your community.&#x20;
* :moneybag:**Gig Micropayments**: smart contract templates for issuing micropayments with proof of a verifiable credential, i.e. streaming payments and proof-of-work. Credential the actual tasks connected to a todo list; tracked with PVCs feeds reputation, ability to access things, ability to get paid autonomously.

