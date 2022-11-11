# Share & Present Credentials

{% hint style="warning" %}
🚧 This section is under construction to make a more comprehensive guide for implementing share & present flows in your applications. Thank you for being patient while our community gets another cup of coffee to finish these docs! ☕️I
{% endhint %}

## Issue/Verify Presentations

Similar to Verifiable Credentials, Verifiable Presentations also have methods that can be used to issue and verify:

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
