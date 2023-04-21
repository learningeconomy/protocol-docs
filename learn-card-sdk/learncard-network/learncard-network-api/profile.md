---
description: >-
  A comprehensive guide on how to use all profile-related API calls with the
  LearnCard Network Plugin
---

# Profile

## **Profile Core**

### **1. Create a Profile**

To create a new profile, use the `createProfile` method. This method accepts an object containing the profile information, excluding the `did` and `isServiceProfile` properties.

```javascript
const profile = {
  displayName: 'John Smith',
  profileId: 'johnsmith',
  image: 'https://example.com/avatar.jpg',
};

await  learnCard.invoke.createProfile(profile);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/create" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **2. Create a Service Profile**

To create a new service profile, use the `createServiceProfile` method. This method accepts an object containing the profile information, excluding the `did` and `isServiceProfile` properties.

```javascript
const serviceProfile = {
  dipslayName: 'Learning Platform',
  profileId: 'learningplatform',
  image: 'https://example.com/service-avatar.jpg',
};

await learnCard.invoke.createServiceProfile(serviceProfile);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/create-service" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **3. Update a Profile**

To update an existing profile, use the `updateProfile` method. This method accepts an object containing the profile information that you want to update, excluding the `did` and `isServiceProfile` properties.

```javascript
const updatedProfile = {
  displayName: 'Jane Smith',
};

await learnCard.invoke.updateProfile(updatedProfile);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **4. Delete a Profile**

To delete an existing profile, use the `deleteProfile` method. This method does not require any parameters.

```javascript
await learnCard.invoke.deleteProfile();
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile" method="delete" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **5. Get a Profile**

To retrieve a specific profile, use the `getProfile` method. This method accepts an optional `profileId` parameter. If no `profileId` is provided, it returns the current user's profile.

```javascript
const profileId = 'johnsmith';

await learnCard.invoke.getProfile(profileId);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/{profileId}" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **6. Search Profiles**

To search for profiles, use the `searchProfiles` method. This method accepts an optional `profileId` parameter and an `options` object. The `options` object can contain the following properties:

* `limit`: Maximum number of profiles to return.
* `includeSelf`: Whether to include the current user's profile in the results.
* `includeConnectionStatus`: Whether to include connection status in the results.

```javascript
const profileId = 'johnsmith';
const options = { limit: 10, includeSelf: false, includeConnectionStatus: true };

learnCard.invoke.searchProfiles(profileId, options);
```

These are all the profile-related API calls available with the LearnCard Network Plugin. Use these methods to manage and interact with user profiles on the LearnCard Network.

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/search/profiles/{input}" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

## Connections Management

### **1. Connect with a Profile**

To send a connection request to another profile, use the `connectWith` method. This method accepts a `profileId` parameter.

```javascript
const profileId = 'janesmith';

await learnCard.invoke.connectWith(profileId);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/{profileId}/connect" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **2. Connect with a Profile using an Invite**

To connect with another profile using an invite, use the `connectWithInvite` method. This method accepts a `profileId` and a `challenge` parameter.

<pre class="language-javascript"><code class="lang-javascript">const profileId = 'janesmith';
const challenge = 'your_challenge';

<strong>await learnCard.invoke.connectWithInvite(profileId, challenge);
</strong></code></pre>

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/{profileId}/connect/{challenge}" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **3. Cancel a Connection Request**

To cancel a pending connection request, use the `cancelConnectionRequest` method. This method accepts a `profileId` parameter.

```javascript
const profileId = 'janesmith';

await learnCard.invoke.cancelConnectionRequest(profileId);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/{profileId}/cancel-connection-request" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **4. Disconnect with a Profile**

To disconnect from an existing connection, use the `disconnectWith` method. This method accepts a `profileId` parameter.

<pre class="language-javascript"><code class="lang-javascript">const profileId = 'janesmith';

<strong>await learnCard.invoke.disconnectWith(profileId);
</strong></code></pre>

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/{profileId}/disconnect" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **5. Accept a Connection Request**

To accept a connection request from another profile, use the `acceptConnectionRequest` method. This method accepts a `profileId` parameter.

```javascript
const profileId = 'janesmith';

await learnCard.invoke.acceptConnectionRequest(profileId);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/credential/accept/{uri}" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **6. Get Connections**

To retrieve all connections, use the `getConnections` method. This method does not require any parameters.

```javascript
await learnCard.invoke.getConnections();
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/connections" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **7. Get Pending Connections**

To retrieve all pending connections, use the `getPendingConnections` method. This method does not require any parameters.

```javascript
await learnCard.invoke.getPendingConnections();
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/pending-connections" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **8. Get Connection Requests**

To retrieve all connection requests, use the `getConnectionRequests` method. This method does not require any parameters.

```javascript
await learnCard.invoke.getConnectionRequests();
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/pending-connections" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **9. Generate an Invite**

To generate an invite, use the `generateInvite` method. This method accepts an optional `challenge` parameter.

<pre class="language-javascript"><code class="lang-javascript">const challenge = 'your_challenge';

<strong>await learnCard.invoke.generateInvite(challenge);
</strong></code></pre>

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/generate-invite" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

These are all the connection-related API calls available with the LearnCard Network Plugin. Use these methods to manage and interact with connections on the LearnCard Network.

## User Blocking

### **1. Block a Profile**

To block a profile, use the `blockProfile` method. This method accepts a `profileId` parameter.

<pre class="language-javascript"><code class="lang-javascript">const profileId = 'janesmith';

<strong>await learnCard.invoke.blockProfile(profileId);
</strong></code></pre>

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/{profileId}/block" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **2. Unblock a Profile**

To unblock a profile, use the `unblockProfile` method. This method accepts a `profileId` parameter.

```javascript
const profileId = 'janesmith';

await learnCard.invoke.unblockProfile(profileId);
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/{profileId}/unblock" method="post" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

### **3. Get Blocked Profiles**

To retrieve all blocked profiles, use the `getBlockedProfiles` method. This method does not require any parameters.

```javascript
await learnCard.invoke.getBlockedProfiles();
```

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/profile/blocked" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

These are all the user-blocking related API calls available with the LearnCard Network Plugin. Use these methods to manage and control user-blocking on the LearnCard Network.
