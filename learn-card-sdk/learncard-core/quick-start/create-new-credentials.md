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
