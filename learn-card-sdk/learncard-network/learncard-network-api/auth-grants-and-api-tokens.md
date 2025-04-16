# Auth Grants and API Tokens

### Overview

AuthGrants are a secure permission system that allows third-party applications to access the LearnCard Network API with specific, limited permissions. This documentation explains how to create and manage AuthGrants, generate API tokens, and use them to make authenticated API requests.

### Understanding AuthGrants

#### What is an AuthGrant?

An AuthGrant is a permission object that:

* Defines specific access rights (scopes) granted to a client application
* Has a defined lifecycle (creation, active period, expiration, revocation)
* Includes metadata such as name, description, and status
* Serves as the basis for generating API tokens for authentication

#### Scope System

AuthGrants use a scope-based permission model following the pattern: `{resource}:{action}`

**Resources:**

* `boosts`
* `claimHook`
* `profile`
* `profileManager`
* `credential`
* `presentation`
* `storage`
* `utilities`
* `contracts`
* `didMetadata`
* `authGrants`

**Actions:**

* `read`: Permission to view resources
* `write`: Permission to create or update resources
* `delete`: Permission to remove resources

**Special Patterns:**

* All access: `*:*`
* Read all: `*:read`
* Resource-wide: `authGrants:*`
* Multiple scopes: Space-separated list (e.g., `"authGrants:read contracts:write"`)

**Common Scope Bundles:**

```javascript
// Common scope bundles
const AUTH_GRANT_READ_ONLY_SCOPE = '*:read';
const AUTH_GRANT_FULL_ACCESS_SCOPE = '*:*';
const AUTH_GRANT_NO_ACCESS_SCOPE = '';
const AUTH_GRANT_PROFILE_MANAGEMENT_SCOPE = 'profile:* profileManager:*';
const AUTH_GRANT_CREDENTIAL_MANAGEMENT_SCOPE = 'credential:* presentation:* boosts:*';
const AUTH_GRANT_CONTRACTS_SCOPE = 'contracts:*';
const AUTH_GRANT_DID_METADATA_SCOPE = 'didMetadata:*';
const AUTH_GRANT_AUTH_GRANTS_SCOPE = 'authGrants:*';
```

### Creating an AuthGrant

Use the LearnCard SDK's `addAuthGrant` method to create a new AuthGrant:

```javascript
const authGrantID = await learnCard.invoke.addAuthGrant({
    name: "Example Auth Grant",
    description: "Full Access Auth Grant",
    scope: '*:*',
})
```

#### AuthGrant Properties

* `id`: Unique identifier (auto-generated if not provided)
* `name`: Name of the AuthGrant
* `description`: (Optional) Description of the purpose or use case
* `challenge`: Security challenge string (must start with AuthGrant prefix)
* `status`: Either 'active' or 'revoked'
* `scope`: Permission scope string
* `createdAt`: ISO 8601 datetime string of creation (auto-generated if not provided)
* `expiresAt`: (Optional) ISO 8601 datetime string for expiration

### Generating an API Token

Once you have an AuthGrant, you can generate an API token using the `getAPITokenForAuthGrant` method:

```javascript
const apiToken = await learnCard.invoke.getAPITokenForAuthGrant(authGrantID)
```

This token encapsulates the permissions defined in the AuthGrant and should be used for authentication in API requests.

### Using the API Token for HTTP Requests

Use the generated API token in the Authorization header with the Bearer scheme:

```javascript
const response = await fetch(
    'https://api.learncard.network/api/boost/send/via-signing-authority/RECIPIENT_ID',
    {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${apiToken}`,
        },
        body: JSON.stringify(payload),
    }
);
```

### Complete End-to-End Example

Here's a complete example showing how to:

1. Create an AuthGrant
2. Generate an API token
3. Use the token to send a boost via the HTTP API

```javascript
// Step 1: Create an AuthGrant with specific permissions
const grantId = await learnCard.invoke.addAuthGrant({
    name: "Boost Sender Auth",
    description: "Permission to send boosts",
    status: 'active',
    challenge: 'auth-grant:example-challenge',
    createdAt: new Date().toISOString(),
    scope: 'boosts:write',
});

// Step 2: Generate an API token from the AuthGrant
const token = await learnCard.invoke.getAPITokenForAuthGrant(grantId);

// Step 3: Prepare the payload for your API request
const payload = {
    boostUri: "uri-of-the-boost-to-send",
    signingAuthority: "your-signing-authority"
};

// Step 4: Make an authenticated HTTP request using the token
const response = await fetch(
    `https://api.learncard.network/api/boost/send/via-signing-authority/RECIPIENT_PROFILE_ID`,
    {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${token}`,
        },
        body: JSON.stringify(payload),
    }
);

// Step 5: Process the response
if (response.status === 200) {
    const sentBoostUri = await response.json();
    console.log(`Boost sent successfully: ${sentBoostUri}`);
} else {
    console.error(`Error sending boost: ${response.status}`);
    const errorDetails = await response.json();
    console.error(errorDetails);
}
```

### Managing AuthGrants

#### Retrieving AuthGrants

```javascript
// Get a single AuthGrant by ID
const authGrant = await learnCard.invoke.getAuthGrant(authGrantID);

// Get multiple AuthGrants with optional filtering
const authGrants = await learnCard.invoke.getAuthGrants({
    query: {
        status: 'active',
        name: { contains: 'API' }
    }
});
```

#### Updating AuthGrants

```javascript
// Update an existing AuthGrant
const updatedGrant = await learnCard.invoke.updateAuthGrant(authGrantID, {
    description: "Updated description",
    scope: "boosts:read boosts:write"
});
```

#### Revoking AuthGrants

```javascript
// Revoke an AuthGrant to invalidate its tokens
await learnCard.invoke.revokeAuthGrant(authGrantID);

// Or delete it completely
await learnCard.invoke.deleteAuthGrant(authGrantID);
```

### Security Considerations

* Store API tokens securely; they grant access according to the AuthGrant's scope
* Use the principle of least privilege: request only the scopes needed for your application
* Set appropriate expiration times for AuthGrants when creating them
* Revoke AuthGrants when they are no longer needed
