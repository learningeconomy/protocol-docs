---
description: What is a control plane?
---

# Control Planes

Control Planes are a primary way for consumers to interact with a LearnCard. A Control Plane provides an abstraction for a higher-order wallet object to initiate complex workflows while being agnostic to the means of accomplishing the workflow.&#x20;

### Control Planes:

* Align plugins based on **primary action categories**: Identity, Signing, Verification, Storage, Caching, and Communication.
* Specify **interfaces** for conforming plugins to implement.&#x20;
* Provide execution environments that support more complex workflows.&#x20;
* Allows for utilizing multiple plugins to support a particular request.
* Streamline functionality for high-quality UX requirements, such as caching and querying capabilities.
* Incentivizes plugin convergence, rather than divergence.
* Enables plugin discovery, both internal and external.

{% hint style="info" %}
**For Example:** when a user stores a credential, they may have a preference over _where_ the credential is stored. Leveraging Controls Planes, a consumer of LearnCard may query for available storage options (IPFS, LocalStorage, DWN, Device Storage, etc.), ask the user which option they would like to use, and then initiate the storage workflow for the user's selection from a **generic** **store** function.&#x20;
{% endhint %}

To help better understand what Control Planes are, it may be easiest for you to take a look at the available Control Planes within LearnCard:

{% content-ref url="id.md" %}
[id.md](id.md)
{% endcontent-ref %}

{% content-ref url="read.md" %}
[read.md](read.md)
{% endcontent-ref %}

{% content-ref url="store.md" %}
[store.md](store.md)
{% endcontent-ref %}

{% content-ref url="index.md" %}
[index.md](index.md)
{% endcontent-ref %}

{% content-ref url="cache.md" %}
[cache.md](cache.md)
{% endcontent-ref %}

{% hint style="warning" %}
You may have noticed, but not all Control Planes have been released yet! We are hard at work implementing the remaining Control Planes on our roadmap 🛠
{% endhint %}
