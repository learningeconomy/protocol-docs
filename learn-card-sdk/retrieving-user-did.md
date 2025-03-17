# Retrieving and Saving User DIDs

This guide explains how to retrieve and save a user's Decentralized Identifier (DID) for verification purposes. There are two primary approaches you can use:

1. **Badge Claiming Method**: Have a user claim a specific credential and then retrieve their DID
2. **ConsentFlow Method**: Create a consent contract for your application

## Method 1: Badge Claiming Approach

### 1. Create a Credential for Users to Claim

```typescript
// Initialize your LearnCard
const issuerLearnCard = await initLearnCard({ seed: '[your secure seed]', network: true });

// Create an unsigned credential for users to claim
const unsignedCredential = {
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://w3id.org/security/suites/ed25519-2020/v1"
  ],
  "type": ["VerifiableCredential", "Achievement"],
  "name": "Verification Badge",
  "description": "This badge verifies your account"
};

// Issue the credential
const credential = await issuerLearnCard.invoke.issueCredential(unsignedCredential);

// Get the credential URI to share
const credentialUri = await issuerLearnCard.store.LearnCloud.upload(credential);
```

### 2. Share the Credential with Users

Provide users with a way to claim the credential, such as a QR code, link, or other sharing method:

```typescript
// Generate a sharing link for the credential
const sharingUrl = `https://learncard.app/claim?uri=${encodeURIComponent(credentialUri)}`;

// Display this URL to your users (e.g., as a QR code or link)
```

### 3. Retrieve and Save the User's DID

After a user claims the credential, you can retrieve their DID from the verifiable presentation:

```typescript
// Retrieve presentations of this credential from the LearnCard Network
const presentations = await issuerLearnCard.invoke.getPresentationsForCredential(credentialUri);

// For each presentation, extract the holder's DID
presentations.forEach(presentation => {
  const userDid = presentation.holder;
  
  // Save this DID to your database for future verification
  saveUserDidToDatabase(userDid, userId);
});
```

## Method 2: ConsentFlow Approach

### 1. Create a ConsentFlow Contract

```typescript
// Initialize your LearnCard with network capabilities
const networkLearnCard = await initLearnCard({ seed: '[your secure seed]', network: true });

// Create a service profile if you haven't already
const serviceProfile = {
  displayName: 'Your Application Name',
  profileId: 'your-app-id',
  image: 'https://example.com/your-app-logo.jpg',
};
await networkLearnCard.invoke.createServiceProfile(serviceProfile);

// Create a ConsentFlow contract
const consentFlowContract = {
  "name": "Account Verification",
  "subtitle": "Verify your account",
  "description": "Allow our application to verify your identity",
  "image": "https://example.com/your-verification-image.jpg",
  "redirectUrl": "https://your-app.com/verification-complete",
  "contract": {
    "read": {
      "anonymize": false,
      "credentials": {
        "categories": {
          "ID": {
            "required": false
          }
        }
      },
      "personal": {
        "Name": {
          "required": false
        }
      }
    },
    "write": {
      "credentials": {
        "categories": {
          "Achievement": {
            "required": false
          }
        }
      }
    }
  }
};

// Create the contract and get the contract URI
const contractUri = await networkLearnCard.invoke.createContract(consentFlowContract);
```

### 2. Generate and Share a Verification URL

```typescript
// Generate the URL for users to consent to your contract
const verificationUrl = `https://learncard.app/consent-flow?uri=${contractUri}`;

// Share this URL with your users to complete verification
```

### 3. Retrieve and Save the User's DID

When a user consents to your contract, they'll be redirected to your `redirectUrl` with their DID as a parameter:

```typescript
// On your redirect handler page:
function handleRedirect() {
  // Extract DID from URL parameters
  const urlParams = new URLSearchParams(window.location.search);
  const userDid = urlParams.get('did');
  
  if (userDid) {
    // Save the user's DID to your database
    saveUserDidToDatabase(userDid, userId);
    
    // Complete the verification process
    completeVerification();
  }
}
```

Alternatively, you can retrieve consented users through the ConsentFlow API:

```typescript
// Retrieve all users who have consented to your contract
const consentData = await networkLearnCard.invoke.getConsentFlowData(contractUri);

// Process each user's data
consentData.records.forEach(record => {
  // The DID is available from the record
  const userDid = record.did;
  
  // Save this DID to your database for future verification
  saveUserDidToDatabase(userDid, userId);
});
```

## Verifying Users by DID

Once you have saved a user's DID, you can use it to verify their identity in future interactions:

```typescript
// When a user performs an action requiring verification
function verifyUserAction(userAction, claimedDid) {
  // Retrieve the stored DID for this user
  const storedDid = retrieveDidFromDatabase(userId);
  
  // Compare the DIDs to verify the user
  if (storedDid === claimedDid) {
    // User is verified, proceed with the action
    processVerifiedAction(userAction);
  } else {
    // Verification failed
    handleVerificationFailure();
  }
}
```

## Best Practices

1. **Security**: Store DIDs securely in your database with appropriate access controls
2. **Privacy**: Inform users about how their DID will be used and stored
3. **Expiration**: Consider implementing expiration for verification to require periodic re-verification
4. **Recovery**: Provide a way for users to update their DID if they need to create a new wallet
5. **Multiple DIDs**: Some users may have multiple DIDs; your system should account for this possibility