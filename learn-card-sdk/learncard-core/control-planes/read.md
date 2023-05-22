---
description: Resolve URIs
---

# Read

## Description

The Read Control Plane is the interface responsible for resolving a [URI](../uris.md) to its Verifiable Credential.&#x20;

{% hint style="info" %}
If the LearnCard also implements the [Cache Plane](cache.md), then this Plane will automatically be cached!
{% endhint %}

The Read Plane implements one method: `get`

### read.get

The `get` method takes in a [URI](../uris.md) and resolves it to a Verifiable Credential.&#x20;

If a plugin implementing get is unable to resolve a URI, it should return undefined, allowing other plugins to take a crack at resolving that URI. If no plugins are able to resolve the URI, the LearnCard will return `undefined`.

## Example plugins that implement the Read Plane

{% content-ref url="../plugins/official-plugins/ceramic.md" %}
[ceramic.md](../plugins/official-plugins/ceramic.md)
{% endcontent-ref %}

{% content-ref url="../plugins/official-plugins/learncloud.md" %}
[learncloud.md](../plugins/official-plugins/learncloud.md)
{% endcontent-ref %}
