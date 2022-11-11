# Accept & Verify Credentials

{% hint style="warning" %}
🚧 This section is under construction to make a more comprehensive guide for implementing accept & verify flows in your applications. Thank you for being patient while our community gets another cup of coffee to finish these docs! ☕️I
{% endhint %}

## Verify Credentials

After being signed, a credential is then given out through an exchange mechanism, where the receiver should verify it! To do that, you can use `verifyCredential`

{% tabs %}
{% tab title="Valid Credential" %}
```typescript
const result = await learnCard.invoke.verifyCredential(signedVc);

console.log(result);
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
