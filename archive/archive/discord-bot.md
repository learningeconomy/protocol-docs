---
description: A bot for sending verifiable credentials in your Discord community
---

# Discord Bot

## Installing the Discord Bot in your Community

#### Prior to Adding the Bot:

* [ ] Create your [Discord server](https://support.discord.com/hc/en-us/articles/204849977-How-do-I-create-a-server-)(s).

#### Adding the Bot:

* [ ] Sign-in to Discord
*   [ ] [Click here](https://discord.com/oauth2/authorize?client_id=998981137173061805\&scope=bot\&perms=380104854592) to add the LearnCard bot and add a server to manage.



    <img src="../../.gitbook/assets/Screen Shot 2022-10-25 at 8.34.19 PM (1).png" alt="" data-size="original">

#### **That's it!** :tada:

You should see LearnCard Discord bot on your Discord server:

<figure><img src="../../.gitbook/assets/Screen Shot 2022-10-25 at 8.37.40 PM.png" alt=""><figcaption></figcaption></figure>

## Setting Up Your Discord Bot

Now that you've gotten your Discord Bot installed in your community, let's get you setup to start issuing your first credentials.

### **1️⃣** —**Configure Your first Issuer!**

![](<../../.gitbook/assets/Screen Shot 2022-10-25 at 8.42.15 PM.png>)

In any channel, type `/configure-issuer`, which will prompt you to fill out information about your community's issuer.&#x20;

<img src="../../.gitbook/assets/Screen Shot 2022-10-25 at 8.46.44 PM.png" alt="" data-size="original">

{% hint style="info" %}
When users receive a credential from you, it will be associated with the issuer profile you configure here. You may create more than one issuer profile.&#x20;
{% endhint %}

Hit `Submit` and, if all went well, you should see a success message:

<img src="../../.gitbook/assets/Screen Shot 2022-10-25 at 8.49.53 PM.png" alt="" data-size="original">

### **2️⃣**—**Create Your First Credential Template**

![](<../../.gitbook/assets/Screen Shot 2022-10-25 at 8.51.51 PM.png>)

In any channel, type the `/add-credential` command, which will allow you to setup a credential you would like to issue in your community.

First, it will prompt you to select a credential type, choosing among different **achievement, skills, learning history, work history** categories:

{% tabs %}
{% tab title="Achievements" %}
* Generic Achievement
* Formal Award
* Badge
* Community Service
{% endtab %}

{% tab title="IDs" %}
* License
* Membership
{% endtab %}

{% tab title="Skills" %}
* Assessment
* Certificate
* Certification
* Competency
* MicroCredential
{% endtab %}

{% tab title="Learning History" %}
* Assignment
* Course
* Degree
* Diploma
* Learning Program
{% endtab %}

{% tab title="Work History" %}
* Apprenticeship Certificate
* Fieldwork
* Journeyman Certificate
* Master Certificate
{% endtab %}
{% endtabs %}

<img src="../../.gitbook/assets/Screen Shot 2022-10-25 at 8.52.53 PM.png" alt="" data-size="original">

Then, you can fill out the content of your credential template:

![](<../../.gitbook/assets/Screen Shot 2022-10-25 at 8.56.04 PM.png>)

If all goes well, you should see your new credential template! ✅

<img src="../../.gitbook/assets/Screen Shot 2022-10-25 at 8.56.51 PM.png" alt="" data-size="original">

{% hint style="info" %}
Right now the Bot doesn't natively support hosting an image for your credential. Although you can host your image anywhere you would like, a great option is [NFT.Storage](https://nft.storage/files/)&#x20;

Upload the image into [NFT.Storage](https://nft.storage/files/), then click “Actions” on your uploaded image and click “View URL”—that’s the URL you want! It should look like: `https://<cid>.ipfs.nftstorage.link/`&#x20;
{% endhint %}

### **3️⃣**—**Send Your First Credential**&#x20;

![](<../../.gitbook/assets/Screen Shot 2022-10-25 at 8.58.18 PM.png>)

In any channel, type the `/send-credential @<user>` command, and @tag someone, which will allow you to send a credential to a user in your community.&#x20;

![](<../../.gitbook/assets/Screen Shot 2022-10-25 at 8.59.13 PM.png>)

The LearnCard bot will ask you which credential you would like to send to the user, and which issuer you would like to send the credential from:

![](<../../.gitbook/assets/Screen Shot 2022-10-25 at 8.59.45 PM.png>)

✅ Then, the LearnCard bot will send a direct message to your community member with steps on how they can claim their shiny new credential! :sparkles:&#x20;

<figure><img src="../../.gitbook/assets/Screen Shot 2022-10-25 at 9.05.51 PM.png" alt=""><figcaption><p>Private DM between the LearnCard bot &#x26; Jacksón</p></figcaption></figure>

## Using your Discord Bot

The discord bot enables the following `/`commands on your server:

<figure><img src="../../.gitbook/assets/Screen Shot 2022-10-25 at 8.40.11 PM.png" alt=""><figcaption><p><code>/</code>  commands for LearnCard Discord bot on your server </p></figcaption></figure>

{% hint style="warning" %}
🚧 More Guides for Discord Bot Coming soon
{% endhint %}

### Comments, Questions, or Palpitations of the Heart?

The best way to start engaging in the community is to participate in our [Github Discussions](https://github.com/learningeconomy/LearnCard/discussions):&#x20;

* [Post a Feature Request ](https://github.com/learningeconomy/LearnCard/discussions/categories/feature-requests)💡
* [Ask for Help](https://github.com/learningeconomy/LearnCard/discussions/categories/help) 💖
* [Show off your project to the community!](https://github.com/learningeconomy/LearnCard/discussions/categories/show-and-tell) 🙌

Do you need custom development or technical support? Click [here](custom-development.md), or send us an email at [sdk@learningeconomy.io](mailto:sdk@learningeconomy.io).
