---
description: One of the two hardest problems in computer science
---

# Cache

## Description

The Cache Control Plane is responsible for speeding up and making a LearnCard more efficient through the use of Caching.

To better encourage and allow separation of the caching between different planes, Cache plugins are required to implement separate caching methods for each plane. In general, when consuming a LearnCard object, you should rarely, if ever, need to interact with the cache directly_—_it should just work underneath each of the other Planes 🚀!

The Cache Plane implements six methods: `getIndex`, `setIndex`, `flushIndex`, `getVc`, `setVc`, `flushVc`

### cache.getIndex

The `getIndex` method takes in a query returns a list of `CredentialRecords`, similar to the Index Plane's `get` method.

### cache.setIndex

The `setIndex` method takes in a query and a list of `CredentialRecords` and caches the records against the query, returning `true` if successful and `false` if not.

### cache.flushIndex

The `flushIndex` method empties out everything in the cache that can be returned by `getIndex.`

### cache.getVc

The `getVc` method takes in a URI and returns a Verifiable Credential, similar to the Read Plane's `get` method.

### cache.setVc

The `setVc` method takes in a URI and a Verifiable Credential and caches the Verifiable Credential against the URI, returning `true` if successful and `false` if not.

### cache.flushVc

The `flushVc` method empties out everything in the cache that can be returned by `getVc.`

## Example plugins that implement the Cache Plane

{% hint style="warning" %}
🚧 This section is under construction. Thank you for being patient while our community gets another cup of coffee to finish these docs! ☕️I
{% endhint %}
