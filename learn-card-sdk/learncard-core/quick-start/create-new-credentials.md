---
description: Quick start for creating new credentials
---

# Create New Credentials

What's the point of issuing, sending, and verifying credentials if there's nothing important inside of them?

### Test Credential

One of the easiest—and fastest—ways to create a credential is to generate a test credential:

```typescript
// Returns an unsigned, test credential in the OBv3 spec.
const unsignedVc = learnCard.invoke.getTestVc();
```

### Basic Boost Credential

In it's most basic form, you can create a Boost credential using the following schema:

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://purl.imsglobal.org/spec/ob/v3p0/context-3.0.1.json",
    "https://ctx.learncard.com/boosts/1.0.0.json",
  ],
  "credentialSubject": {
    "achievement": {
      "achievementType": "ext:LCA_CUSTOM:Social Badge:Adventurer",
      "criteria": {
        "narrative": "This badge is awarded for being a adventurer."
      },
      "description": "An adventure badge.",
      "id": "urn:uuid:123",
      "image": "https://i.postimg.cc/s2xdx5Ss/erik-jan-leusink-Ib-Px-GLg-Ji-MI-unsplash.jpg",
      "name": "Adventurer",
      "type": [
        "Achievement"
      ]
    },
    "id": "did:web:network.learncard.com:users:example",
    "type": [
      "AchievementSubject"
    ]
  },
  "display": {
    "backgroundColor": "",
    "backgroundImage": "",
    "displayType": "badge"
  },
  "image": "https://i.postimg.cc/s2xdx5Ss/erik-jan-leusink-Ib-Px-GLg-Ji-MI-unsplash.jpg",
  "skills": [],
  "issuanceDate": "2025-04-01T16:56:00.667Z",
  "issuer": "did:web:network.learncard.com:users:issuer-example",
  "name": "Tabby Cat",
  "type": [
    "VerifiableCredential",
    "OpenBadgeCredential",
    "BoostCredential"
  ]
}
```

### Credentials from Template

But sometimes the test credential is too basic for most use cases. That's why LearnCard has out-of-the-box support for some basic types of credentials, and a simple function to create new credentials:

```typescript
// Returns an unsigned, basic credential
const basicCredential = learnCard.invoke.newCredential({ type: 'basic' });
// Returns an unsigned, achievement credential. 
const achievementCredential = learnCard.invoke.newCredential({ type: 'achievement' });
```

For more info on Credential Templates, checkout the [VC-Templates Plugin](../plugins/official-plugins/vc-templates.md):

{% content-ref url="../plugins/official-plugins/vc-templates.md" %}
[vc-templates.md](../plugins/official-plugins/vc-templates.md)
{% endcontent-ref %}
