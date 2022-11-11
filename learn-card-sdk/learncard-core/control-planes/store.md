---
description: Create URIs
---

# Store

## Description

The Store Control Plane is the interface responsible for storing a Verifiable Credential and returning a [URI](../uris.md) that resolves to it.

{% hint style="info" %}
If the LearnCard also implements the [Cache Plane](cache.md), then this Plane will automatically be cached!
{% endhint %}

{% hint style="info" %}
**Note:** In order to use this plane, you will have to choose _where_ to store the Verifiable Credential!

You can get a list of available storage providers using the `providers` field:

```typescript
console.log(learnCard.store.providers);
// {
//     Ceramic: {
//       name: 'Ceramic',
//       displayName: 'Ceramic',
//       description: 'Uploads/resolves credentials using the Ceramic Network (https://ceramic.network/)'
//     }
// }
```
{% endhint %}

The Store Plane implements two methods: `upload`, and (optionally) `uploadMany`

### store.upload

The `upload` method takes in a Verifiable Credential, stores the credential, and converts it into a resolvable [URI](../uris.md).

### store.uploadMany

{% hint style="info" %}
Note: This method is optional
{% endhint %}

The `uploadMany` method takes in an array of Verifiable Credentials, stores the credentials, and converts them into an array of resolvable [URIs](../uris.md).

## Example plugins that implement the Store Plane

{% content-ref url="../plugins/official-plugins/ceramic.md" %}
[ceramic.md](../plugins/official-plugins/ceramic.md)
{% endcontent-ref %}
