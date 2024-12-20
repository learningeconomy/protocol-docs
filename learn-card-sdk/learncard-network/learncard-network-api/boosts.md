---
description: Boosts Management
---

# Boosts

### &#x31;**. Create a Boost**

To create a boost, use the `createBoost` method. This method accepts a `credential` object (which can be an `UnsignedVC` or `VC`) and an optional `metadata` object.

```javascript
const credential = your_credential;
const metadata = {
  name: 'Your Boost Name',
  description: 'Your Boost Description',
};

learnCard.invoke.createBoost(credential, metadata);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/boost/create" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **2. Get a Boost**

To get a boost, use the `getBoost` method. This method accepts a `uri` parameter.

```javascript
const uri = 'your_boost_uri';

learnCard.invoke.getBoost(uri);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/boost/{uri}" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **3. Get Boosts**

To retrieve all boosts, use the `getBoosts` method.

```javascript
learnCard.invoke.getBoosts();
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/boost" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **4. Get Boost Recipients**

To get boost recipients, use the `getBoostRecipients` method. This method accepts a `uri` parameter and optional `limit` and `skip` parameters.

```javascript
const uri = 'your_boost_uri';
const limit = 10;
const skip = 0;

learnCard.invoke.getBoostRecipients(uri, limit, skip);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/boost/recipients/{uri}" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **5. Update a Boost**

To update a boost, use the `updateBoost` method. This method accepts a `uri` parameter, an `updates` object, and a `credential` object (which can be an `UnsignedVC` or `VC`).

```javascript
const uri = 'your_boost_uri';
const updates = {
  name: 'Updated Boost Name',
  description: 'Updated Boost Description',
};
const credential = updated_credential;

learnCard.invoke.updateBoost(uri, updates, credential);
```

### **6. Delete a Boost**

To delete a boost, use the `deleteBoost` method. This method accepts a `uri` parameter.

```javascript
const uri = 'your_boost_uri';

learnCard.invoke.deleteBoost(uri);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/boost/{uri}" method="delete" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **7. Send a Boost**

To send a boost to another profile, use the `sendBoost` method. This method accepts a `profileId`, a `boostUri` parameter, and an optional `encrypt` parameteropconst profileId = 'janesmith';

```javascript
const boostUri = 'your_boost_uri';
const encrypt = true;

learnCard.invoke.sendBoost(profileId, boostUri, encrypt);
```

These are the API calls related to boosts management in the LearnCard Network API. Use these methods to create, update, retrieve, and delete boosts, as well as send boosts to other profiles.

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/boost/send/{profileId}" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/credential/send/{profileId}" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **Claim a Boost**

```javascript
const boostUri = 'https://example.com/boost-uri';
const challenge = 'example-challenge';

await networkLearnCard.invoke.claimBoostWithLink(boostUri, challenge);
```

These examples demonstrate some of the ways you can interact with the LearnCard Network API using the `@learncard/network-plugin`.
