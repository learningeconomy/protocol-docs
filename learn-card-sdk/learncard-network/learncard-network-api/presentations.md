---
description: Presentations Management
---

# Presentations

### **1. Send a Presentation**

To send a presentation to another profile, use the `sendPresentation` method. This method accepts a `profileId`, a `vp` object, and an optional `encrypt` parameter.

```javascript
const profileId = 'janesmith';
const vp = your_presentation;
const encrypt = true;

await learnCard.invoke.sendPresentation(profileId, vp, encrypt);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/presentation/send/{profileId}" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **2. Accept a Presentation**

To accept a presentation, use the `acceptPresentation` method. This method accepts a `uri` parameter.

```javascript
const uri = 'your_presentation_uri';

await learnCard.invoke.acceptPresentation(uri);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/presentation/accept/{uri}" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **3. Get Received Presentations**

To retrieve all received presentations, use the `getReceivedPresentations` method. This method accepts an optional `from` parameter.

```javascript
const from = 'johnsmith';

await learnCard.invoke.getReceivedPresentations(from);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/presentation/received" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **4. Get Sent Presentations**

To retrieve all sent presentations, use the `getSentPresentations` method. This method accepts an optional `to` parameter.

<pre class="language-javascript"><code class="lang-javascript">const to = 'janesmith';

<strong>await learnCard.invoke.getSentPresentations(to);
</strong></code></pre>

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/presentation/sent" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **5. Get Incoming Presentations**

To retrieve all incoming presentations, use the `getIncomingPresentations` method. This method accepts an optional `from` parameter.

```javascript
const from = 'johnsmith';

await learnCard.invoke.getIncomingPresentations(from);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/presentation/incoming" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **6. Delete a Presentation**

To delete a presentation, use the `deletePresentation` method. This method accepts a `uri` parameter.

```javascript
const uri = 'your_presentation_uri';

await learnCard.invoke.deletePresentation(uri);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/presentation/{uri}" method="delete" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}
