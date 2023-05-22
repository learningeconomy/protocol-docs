---
description: Get up and running with Learn Card!
---

# Quick Start

## Install the library

Install using the package manager of your choice:

{% tabs %}
{% tab title="pnpm" %}
```bash
pnpm i @learncard/init
```
{% endtab %}

{% tab title="yarn" %}
```bash
yarn add @learncard/init
```
{% endtab %}

{% tab title="npm" %}
```bash
npm i @learncard/init
```
{% endtab %}
{% endtabs %}

## Make your LearnCard

To make your first wallet, import and call `initLearnCard` with a unique string that is 64 characters or less:

{% hint style="warning" %}
**Good to know:** If you do not pass in a string that is 64 characters long. It will be prefixed with zeroes until it is 64 characters. This means that '1' and '001' are identical keys in the eyes of `initLearnCard`.
{% endhint %}

{% hint style="danger" %}
**Warning:** Key input should be a hexadecimal string. If you pass a string that is not valid hex, an error will be thrown!
{% endhint %}

```typescript
import { initLearnCard } from '@learncard/init';

const learnCard = await initLearnCard({ seed: '8f476ba148360c7d1830beb2520e6bf883e934a7d16159ce0930e3cc53799fd9' });
```

## Issue Credentials

First, make an unsigned [Verifiable Credential](https://www.w3.org/TR/vc-data-model/). You can do this yourself if you already have that set up for your app, or, if you just need to test out working with this library, you can use the `newCredential` method to easily create a test VC.

```typescript
const unsignedVc = learnCard.invoke.newCredential();
```

To sign (or "issue") that VC, simply call `issueCredential`

```typescript
const signedVc = await learnCard.invoke.issueCredential(unsignedVc);
```

## Verify Credentials

After a credential is signed, the credential may be transferred via an exchange mechanism, where a receiving party can verify it! To verify a signed Verifiable Credential, you can use `verifyCredential`

{% tabs %}
{% tab title="Valid Credential" %}
```typescript
const result = await learnCard.invoke.verifyCredential(signedVc);

console.log(result);
// { checks: ['proof', 'expiration'], warnings: [], errors: [] }

// OR, for a more human readable output:

const result = await learnCard.invoke.verifyCredential(signedVc, {}, true);
// [
//     { status: "Success", check: "proof", message: "Valid" },
//     {
//         status: "Success",
//         check: "expiration",
//         message: "Valid • Does Not Expire"
//     }
// ]
```
{% endtab %}

{% tab title="Invalid Credential" %}
```typescript
signedVc.expirationDate = '2022-06-10T18:26:57.687Z';

const result = await learnCard.invoke.verifyCredential(signedVc);

console.log(result);
// {
//   checks: ['proof'],
//   warnings: [],
//   errors: [
//     'signature error: Verification equation was not satisfied',
//     'expiration error: Credential is expired'
//   ]
// }

// OR, for a more human readable output:

const result = await learnCard.invoke.verifyCredential(signedVc, {}, true);

console.log(result); 
// [
//     { 
//         status: "Failed",
//         check: "signature",
//         details: "signature error: Verification equation was not satisfied"
//     },
//     {
//         status: "Failed",
//         check: "expiration",
//         details: "Invalid • Expired 10 JUN 2022"
//     },
//     { status: "Success", check: "proof", message: "Valid" }
// ]
```
{% endtab %}
{% endtabs %}

## Issue/Verify Presentations

Similar to Verifiable Credentials, LearnCard has methods for verifying and issuing Verifiable Presentations:

{% tabs %}
{% tab title="Valid Presentation" %}
```typescript
const unsignedVp = await learnCard.invoke.getTestVp();

//Package signed Verifiable Credential into the presentation
unsignedVp.verifiableCredential = signedVc;

const vp = await learnCard.invoke.issuePresentation(unsignedVp);

const result = await learnCard.invoke.verifyPresentation(vp);

console.log(result);
// {
//   checks: ['proof'],
//   warnings: [],
//   errors: [],
// }
```
{% endtab %}

{% tab title="Invalid Presentation" %}
```typescript
const unsignedVp = await learnCard.invoke.getTestVp();
const vp = await learnCard.invoke.issuePresentation(unsignedVp);

vp.holder = 'did:key:nope';

const result = await learnCard.invoke.verifyPresentation(vp);

console.log(result);
// {
//     checks: [],
//     warnings: [],
//     errors: ['Unable to filter proofs: Unable to resolve: invalidDid'],
// }
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**What is a** [**Verifiable Presentation**](https://www.w3.org/TR/vc-data-model/#dfn-presentations)**, and why would I use one?**&#x20;

Verifiable Presentations enable trusted sharing of one or more claims in a single, verifiable package. Claims may be bundled from one or multiple issuers, and they may consist of the original Verifiable Credential, or a derived "zero-knowledge proof."

**As a general principle,** you should use Verifiable Presentations when _presenting_ Verifiable Credentials to a verifying party because it proves the relationship between the user or entity presenting the credential, and the credential itself.&#x20;
{% endhint %}

## Storing/Retrieving Credentials

Credentials can be converted back and forth to [URIs](../uris.md), which can be stored per holder using [Control Planes](../control-planes/). [URIs](../uris.md) simplify complex processes, such as indexing and caching, over credentials stored in many different locations, such as in IPFS, device storage, or a Decentralized Web Node.

{% code title="Issuer" %}
```typescript
const holderDid = 'did:key:z6MknqnHBn4Rx64gH4Dy1qjmaHjxFjaNG1WioKvQuXKhEKL5'
const uvc = learnCard.invoke.newCredential({ subject: holderDid });
const vc = await learnCard.invoke.issueCredential(uvc);
const uri = await learnCard.store.Ceramic.upload(vc);

// *** Send URI to Holder ***
```
{% endcode %}

{% code title="Holder" %}
```typescript
// *** Receive URI from Issuer ***

const credential = await learnCard.read.get(uri);
const result = await learnCard.invoke.verifyCredential(credential);

if (result.errors.length == 0) {
    await learnCard.index.IDX.add({ uri, id: 'test' });
}

// Later, when the Holder would like to see the credential again
const records = await learnCard.index.all.get();
const record = records.find(({ id }) => id === 'test');
const storedCredential = await learnCard.read.get(record.uri);

// _.isEqual(credential, storedCredential) = true 
```
{% endcode %}

{% hint style="info" %}
The above example uses Ceramic storage, but there are many ways to store and retrieve a credential! Check out the[ **Store control plane**](../control-planes/store.md) for more info and options.
{% endhint %}

## Further Reading

{% content-ref url="../construction/" %}
[construction](../construction/)
{% endcontent-ref %}

{% content-ref url="../control-planes/" %}
[control-planes](../control-planes/)
{% endcontent-ref %}

{% content-ref url="../plugins/" %}
[plugins](../plugins/)
{% endcontent-ref %}

{% content-ref url="../chapi/" %}
[chapi](../chapi/)
{% endcontent-ref %}
