---
description: Manage the holder's list of credentials
---

# Index

## Description

The Index Control Plane is the interface responsible for managing [CRUD](https://en.wikipedia.org/wiki/Create,\_read,\_update\_and\_delete) operations on the holder's personal index.

{% hint style="info" %}
If the LearnCard also implements the [Cache Plane](cache.md), then this method will automatically be cached!
{% endhint %}

{% hint style="info" %}
**Note:** In order to use some of the methods of this plane, you will have to choose _where_ to store the index!

You can get a list of available index providers using the `providers` field:

```typescript
console.log(learnCard.index.providers);
// {
//     LearnCloud: {
//         name: 'LearnCloud',
//         displayName: 'LearnCloud',
//         description: 'LearnCloud Integration'
//     },
//     IDX: {
//       name: 'IDX',
//       displayName: 'IDX',
//       description: 'Stores a bespoke index of credentials for an individual based on their did'
//     }
// }
```
{% endhint %}

The Index Plane implements six methods: `get`, (optionally) `getPage`, (optionally) `getCount`, `add`, `update`, and `remove`

### index.get

{% hint style="info" %}
**Hint:** You may use the "all" provider to combine the `CredentialRecord`s of _all_ providers with this method:

```typescript
console.log(await learnCard.index.all.get());
// []
```
{% endhint %}

The `get` method takes in a Mongo-style query and returns a list of `CredentialRecords`, which are primarily an ID, a [URI](../uris.md), and some metadata.

### index.getPage

{% hint style="info" %}
Note: This method is optional
{% endhint %}

{% hint style="info" %}
If the LearnCard also implements the [Cache Plane](cache.md), then this method will automatically be cached!
{% endhint %}

When there are a lot of credentials stored in the index for a given query, it can be useful to paginate your queries rather than request all of them at once. That is what `getPage` is for! This call will return an object of the following shape:

```typescript
type GetPageResult<Metadata extends Record<string, any>> = {
    cursor?: string;
    hasMore: boolean;
    records: CredentialRecord<Metadata>[];
};
```

Using the `hasMore` and `cursor` fields, you can determine if you should request the next page, as well as how to request the next page. The below example shows a simple way to request all available pages:

```typescript
const records: CredentialRecord[] = [];

let result = await learnCard.index.LearnCloud.getPage();
records.push(result.records);

while (result.hasMore) {
    result = await learnCard.index.LearnCloud.getPage(undefined, { cursor: result.cursor });
    records.push(result.records);
}
```

### index.getCount

{% hint style="info" %}
Note: This method is optional
{% endhint %}

{% hint style="info" %}
If the LearnCard also implements the [Cache Plane](cache.md), then this Plane will automatically be cached!
{% endhint %}

Sometimes, it can be useful for an app to display the total number of records for a given query without wanting to actual grab every credential for that query. This is where `getCount` comes in handy!

```typescript
const totalRecords = await learnCard.index.LearnCloud.getCount();
const totalAchievementRecords = await learnCard.index.LearnCloud.getCount({ type: 'Achievement' });
```

### index.add

The `add` method takes in a `CredentialRecord` and adds it to the holder's personal index.

### index.addMany

The optional `addMany` method takes in an array of `CredentialRecord`s and adds them to the holder's personal index.

### index.update

The `update` method takes in an ID and an update object and updates a `CredentialRecord` in the holder's personal index.

### index.remove

The `remove` method takes in an ID and removes the `CredentialRecord` with the corresponding ID from the holder's personal index.

### index.removeAll

The optional `removeAll` method flushes all `CredentialRecord`s from the holder's personal index.

## Example plugins that implement the Index Plane

{% content-ref url="../plugins/official-plugins/idx.md" %}
[idx.md](../plugins/official-plugins/idx.md)
{% endcontent-ref %}

{% content-ref url="../plugins/official-plugins/learncloud.md" %}
[learncloud.md](../plugins/official-plugins/learncloud.md)
{% endcontent-ref %}
