---
description: Storage Management
---

# Storage

### **1. Store a Credential/Presentation**

To store a credential or presentation, use the `store` method. This method accepts a `credential` or `presentation` object.

```javascript
const credential = your_credential;

await learnCard.store['LearnCard Network'].uploadEncrypted(credential);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/storage/store" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **2. Resolve a URI to a Credential/Presentation**

To resolve a URI to a credential or presentation, use the `learnCard.read` method. This method accepts a `uri` parameter.

```javascript
econst uri = 'your_credential_or_presentation_uri';

await learnCard.read.get(uri);
```

These are the storage-related API calls available in the LearnCard Network API. Use these methods to manage the storage and retrieval of credentials and presentations on the LearnCard Network.

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/storage/resolve/{uri}" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

