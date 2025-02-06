# Reading xAPI Statements

### Querying Your Statements

After sending xAPI statements, you can retrieve them using the same endpoint:

```typescript
// Basic GET request for statements
const actor = {
    account: { 
        homePage: "https://www.w3.org/TR/did-core/",
        name: userDid  // Your user's DID
    },
    name: userDid
};

// Convert actor to URL parameter
const params = new URLSearchParams({ 
    agent: JSON.stringify(actor) 
});

// Fetch statements
const response = await fetch(`${endpoint}/statements?${params}`, {
    method: 'GET',
    headers: {
        'Content-Type': 'application/json',
        'X-Experience-API-Version': '1.0.3',
        'X-VP': jwt  // Your authentication JWT
    }
});
```

### Important Security Notes

1. Users can only read statements about themselves
2. The DID in the JWT (X-VP header) must match the actor's DID
3. A 401 error means either:
   * Invalid authentication
   * Trying to read another user's statements
   * Expired or malformed JWT

### Delegated Access

If you need to allow another party to read statements:

1. Create a delegate credential:

```typescript
const delegateCredential = await userA.invoke.issueCredential({
    type: 'delegate',
    subject: userB.id.did(),
    access: ['read']  // Can be ['read'], ['write'], or ['read', 'write']
});
```

2. Use the delegate credential to create a presentation:

```typescript
const unsignedPresentation = await userB.invoke.newPresentation(delegateCredential);
const delegateJwt = await userB.invoke.issuePresentation(unsignedPresentation, {
    proofPurpose: 'authentication',
    proofFormat: 'jwt'
});
```

3. Use this JWT in the X-VP header to read statements

### Voiding Statements

To remove a statement (mark it as void):

```typescript
// First get the statement ID from the original POST response
const statementId = (await postResponse.json())[0];

// Create void statement
const voidStatement = {
    actor,
    verb: XAPI.Verbs.VOIDED,
    object: { 
        objectType: 'StatementRef', 
        id: statementId 
    }
};

// Send void request
const voidResponse = await fetch(`${endpoint}/statements`, {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'X-Experience-API-Version': '1.0.3',
        'X-VP': jwt
    },
    body: JSON.stringify(voidStatement)
});
```

Important: You can only void statements that you created.

### Validation Tips

1. Check Response Status:
   * 200: Success
   * 401: Authentication/permission error
   * Other: Server/request error
2. Common Implementation Issues:
   * JWT not matching actor DID
   * Missing or malformed agent parameter
   * Incorrect content type header
   * Missing xAPI version header
3. Testing Checklist:
   * Can read own statements
   * Cannot read others' statements
   * Delegate access works as expected
   * Can void own statements
   * Cannot void others' statements

Remember: The xAPI server maintains strict permissions - users can only read and modify their own statements unless explicitly delegated access by the statement owner.
