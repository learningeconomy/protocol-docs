---
description: Manage the holder's list of credentials
---

# Index

## Description

The Index Control Plane is the interface responsible for managing [CRUD](https://en.wikipedia.org/wiki/Create,\_read,\_update\_and\_delete) operations on the holder's personal index.

{% hint style="info" %}
If the LearnCard also implements the [Cache Plane](cache.md), then this Plane will automatically be cached!
{% endhint %}

{% hint style="info" %}
**Note:** In order to use some of the methods of this plane, you will have to choose _where_ to store the index!

You can get a list of available index providers using the `providers` field:

```typescript
console.log(learnCard.index.providers);
// {
//     IDX: {
//       name: 'IDX',
//       displayName: 'IDX',
//       description: 'Stores a bespoke index of credentials for an individual based on their did'
//     }
// }
```
{% endhint %}

The Index Plane implements four methods: `get`, `add`, `update`, and `remove`

### index.get

{% hint style="info" %}
**Hint:** You may use the "all" provider to combine the `CredentialRecord`s of _all_ providers with this method:

```typescript
console.log(await learnCard.index.all.get());
// []
```
{% endhint %}

The `get` method takes in a query and returns a list of `CredentialRecords`, which are primarily an ID, a [URI](../uris.md), and some metadata.

### index.add

The `add` method takes in a `CredentialRecord` and adds it to the holder's personal index.

### index.update

The `update` method takes in an ID and an update object and updates a `CredentialRecord` in the holder's personal index.

### index.remove

The `remove` method takes in an ID and removes the `CredentialRecord` with the corresponding ID from the holder's personal index.

## Example plugins that implement the Index Plane

{% content-ref url="../plugins/official-plugins/idx.md" %}
[idx.md](../plugins/official-plugins/idx.md)
{% endcontent-ref %}
