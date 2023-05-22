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
//     },
//     LearnCloud: {
//         name: 'LearnCloud',
//         displayName: 'LearnCloud',
//         description: 'LearnCloud Integration'
//     }
// }
```
{% endhint %}

The Store Plane implements three methods: `upload`, (optionally) `uploadEncrypted`, and (optionally) `uploadMany`

### store.upload

The `upload` method takes in a Verifiable Credential, stores the credential, and converts it into a resolvable [URI](../uris.md).

### store.uploadEncrypted

{% hint style="info" %}
Note: This method is optional
{% endhint %}

The `uploadEncrypted` method allows you to encrypt a credential before uploading it, optionally specifying recipients who are allowed to decrypt the resolved credential. This is generally going to be safer, and it is heavily encouraged for Providers to implement this method!

### store.uploadMany

{% hint style="info" %}
Note: This method is optional
{% endhint %}

The `uploadMany` method takes in an array of Verifiable Credentials, stores the credentials, and converts them into an array of resolvable [URIs](../uris.md).

## Example plugins that implement the Store Plane

{% content-ref url="../plugins/official-plugins/ceramic.md" %}
[ceramic.md](../plugins/official-plugins/ceramic.md)
{% endcontent-ref %}

{% content-ref url="../plugins/official-plugins/learncloud.md" %}
[learncloud.md](../plugins/official-plugins/learncloud.md)
{% endcontent-ref %}
