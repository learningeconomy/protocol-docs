# Setting Up ConsentFlow with an Independent Network

ConsentFlow contracts allow third-party applications to read from and write to a LearnCard with the consent of the LearnCard owner. This guide will walk you through setting up a ConsentFlow with an Independent **Network** (instead of the default LearnCard Network) and Independent **Wallet** (instead of the default LearnCard App) to connect your external, 3rd party application.

### Prerequisites

* Node.js environment
* Access to an Independent Network endpoint (e.g., `https://scoutnetwork.org/trpc`)

### Step 1: Create a Service Profile

First, you need to initialize the LearnCard CLI and create a network LearnCard that points to your Independent Network:

```javascript
// Install and start LearnCard CLI
// pnpm dlx @learncard/cli

// Initialize LearnCard with your Independent Network
const networkLearnCard = await initLearnCard({ 
    seed: '[your secure key]', 
    network: 'https://network.independent.example.org/trpc'  // Point to your Independent Network
})

// Create a service profile
const serviceProfile = {
  displayName: 'Your App Name',
  profileId: 'your-app-unique-id',
  image: 'https://example.com/your-app-logo.jpg',
};

// Register the service profile
await networkLearnCard.invoke.createServiceProfile(serviceProfile);
```

Your service profile represents your application in the LearnCard ecosystem. Make sure to use a unique `profileId` and provide a clear `displayName` and `image` to help users recognize your service.

### Step 2: Create a ConsentFlow Contract

Next, create a ConsentFlow contract that specifies what data your application needs to read from and write to users' LearnCard wallets:

```javascript
const consentFlowContract = {
    "name": "Your App Integration",
    "subtitle": "Connect your LearnCard to Your App",
    "description": "This connection allows Your App to access and issue credentials on your LearnCard.",
    "image": "https://example.com/your-app-logo.jpg",
    "redirectUrl": "https://your-app.com/callback", // Where to redirect after consent
    "contract": {
        "read": {
            "anonymize": true, // Set to false if you need identifiable information
            "credentials": {
                "categories": {
                    // Specify credential categories your app needs to read
                    "Merit Badge": {
                        "required": true
                    },
                    "Skill": {
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
                    // Specify credential categories your app will write
                    "Merit Badge": {
                        "required": true
                    },
                    "Skill": {
                        "required": false
                    }
                }
            },
            "personal": { 
                "SomeCustomID": {
                    "required": true
                }
            }
        }
    }
};

// Create the contract and get its URI
const contractUri = await networkLearnCard.invoke.createContract(consentFlowContract);

// Generate consent flow URLs for your Independent Wallet connected to your Network
const productionUrl = `https://wallet.independent.example.org/consent-flow?uri=${contractUri}`;

console.log("Production ConsentFlow URL:", productionUrl);

```

#### Available Credential Categories

When specifying credential categories in your contract, ensure you are using categories supported by your network. For example, many networks support a subset of the following categories:

* Achievement
* Accommodation
* Accomplishment
* Course
* ID
* Job
* Learning History
* Membership
* Merit Badge
* Skill
* Social Badge
* Work History

### Step 3: Add a "Connect Your Wallet" Button to Your Website

Add a button or link on your application that directs users to the ConsentFlow URL:

```html
<a href="https://wallet.independent.example.org/consent-flow?uri=YOUR_CONTRACT_URI" 
   class="connect-button">
   Connect Your Wallet
</a>
```

When users click this button, they'll be directed to the ConsentFlow consent page where they can review and approve the permissions your app is requesting.

### Step 4: Handle the Redirect After User Consent

After a user consents to your contract, they'll be redirected to the URL specified in your contract's `redirectUrl` parameter with their DID added as a query parameter:

```
https://your-app.com/callback?did=did:method:profile-id
```

In your application, implement a handler for this callback:

```javascript
// Example Express.js route handler
app.get('/callback', (req, res) => {
  const userDid = req.query.did;
  
  if (!userDid) {
    return res.status(400).send('Missing DID parameter');
  }
  
  // Store the DID in your database, associating it with the user's account
  storeUserDid(currentUser.id, userDid)
    .then(() => {
      res.redirect('/dashboard?connection=success');
    })
    .catch(error => {
      console.error('Failed to store user DID:', error);
      res.status(500).send('Failed to complete connection');
    });
});

// Function to store the DID in your database
async function storeUserDid(userId, did) {
  // Implementation depends on your database
  await db.users.update({
    where: { id: userId },
    data: { learnCardDid: did }
  });
}
```

### Step 5: Reading Data from Connected LearnCards

To read data from users who have consented to your contract:

```javascript
// Retrieve ConsentFlow data for your contract
async function getLearnCardData(contractUri, options = {}) {
  let data = await networkLearnCard.invoke.getConsentFlowData(contractUri, options);
  
  // Process the returned records
  for (const record of data.records) {
    // Access shared credentials by category
    const meritBadges = record.credentials.categories['Merit Badge'] || [];
    
    for (const credentialUri of meritBadges) {
      // Read the credential
      const credential = await networkLearnCard.read.get(credentialUri);
      // Process the credential
      console.log('Retrieved credential:', credential);
    }
    
    // Access personal information if shared
    const userName = record.personal['Name'];
    
    // Store or process the retrieved data
  }
  
  // Handle pagination if there are more records
  if (data.hasMore) {
    // Get the next page
    const nextPageData = await getLearnCardData(contractUri, { cursor: data.cursor });
    // Combine with current data
    data.records = [...data.records, ...nextPageData.records];
  }
  
  return data;
}
```

### Step 6: Sending Credentials to Users

To issue credentials to connected users:

```javascript
// Function to send a credential to a user by their DID
async function sendCredentialToUser(did, credentialData) {
  // Extract the profileId from the DID
  // This is a simplified example - you'll need to implement proper DID resolution
  const profileId = did.split(':').pop();
  
  // Create a new credential
  const newCredential = await networkLearnCard.invoke.newCredential({
        type: 'boost', 
        boostName: 'Hello from External App',
        boostImage: 'https://placehold.co/400x400?text=External+App', // Optional placeholder image
        achievementType: 'Achievement',
        achievementName:'Connected External App',
        achievementDescription: 'Awarded for connecting to a 3rd party app.',
        achievementNarrative: 'Created and connected a full external app.'
        achievementImage: 'https://placehold.co/400x400?text=External+App', // Optional placeholder image   
    });
  
  // Issue the credential
  const vc = await networkLearnCard.invoke.issueCredential(newCredential);
  
  // Send the credential to the user (encrypted for security)
  const encrypt = true;
  await networkLearnCard.invoke.sendCredential(profileId, vc, encrypt);
  
  return vc;
}
```

### Best Practices

1. **Security**: Always use a strong, secure seed for your LearnCard initialization.
2. **Privacy**: Only request access to the credential categories and personal information that your application actually needs.
3. **User Experience**: Clearly explain to users why your application needs access to their LearnCard and what benefits they'll receive.
4. **Error Handling**: Implement robust error handling for all LearnCard operations.
5. **Persistence**: Store the contract URI securely - you'll need it for all future operations with that contract.

### Troubleshooting

* **Connection Issues**: Ensure your network endpoint is correctly configured and accessible.
* **Missing DIDs**: Verify that users are completing the consent process and your redirect handler is properly extracting the DID.
* **Credential Read Failures**: Check that your contract has the necessary read permissions for the credential categories you're trying to access.
* **Credential Write Failures**: Verify that your contract has the necessary write permissions and that you're using the correct profileId when sending credentials.

By following this guide, you should be able to successfully integrate LearnCard with your application using an Independent Network, allowing users to connect their LearnCards and exchange credentials securely.
