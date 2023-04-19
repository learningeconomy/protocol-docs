---
description: Credentials Management
---

# Credentials

### **1. Send a Credential**

To send a credential to another profile, use the `sendCredential` method. This method accepts a `profileId`, a `vc` object (which can be an `UnsignedVC` or `VC`), and an optional `encrypt` parameter.

```javascript
const profileId = 'janesmith';
const vc = await networkLearnCard.invoke.issueCredential(networkLearnCard.invoke.newCredential())
const encrypt = true;

learnCard.invoke.sendCredential(profileId, vc, encrypt);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/credential/send/{profileId}" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **2. Accept a Credential**

To accept a credential, use the `acceptCredential` method. This method accepts a `uri` parameter.

```javascript
const uri = 'your_credential_uri';

learnCard.invoke.acceptCredential(uri);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/credential/accept/{uri}" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **3. Get Received Credentials**

To retrieve all received credentials, use the `getReceivedCredentials` method. This method accepts an optional `from` parameter.

```javascript
const from = 'johnsmith';

learnCard.invoke.getReceivedCredentials(from);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/credentials/received" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **4. Get Sent Credentials**

To retrieve all sent credentials, use the `getSentCredentials` method. This method accepts an optional `to` parameter.

```javascript
const to = 'janesmith';

learnCard.invoke.getSentCredentials(to);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/credentials/sent" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **5. Get Incoming Credentials**

To retrieve all incoming credentials, use the `getIncomingCredentials` method. This method accepts an optional `from` parameter.

```javascript
const from = 'johnsmith';

learnCard.invoke.getIncomingCredentials(from);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/credentials/incoming" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **6. Delete a Credential**

To delete a credential, use the `deleteCredential` method. This method accepts a `uri` parameter.

```javascript
const uri = 'your_credential_uri';

learnCard.invoke.deleteCredential(uri);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/credential/{uri}" method="delete" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}
