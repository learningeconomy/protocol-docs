---
description: 'Tutorial: Create and Send Your First Digital Credential'
---

# Create a Credential

Welcome! This tutorial will walk you through creating your very first digital Verifiable Credential (VC) and sending it to your LearnCard app. Think of a VC as a secure, digital certificate or badge that can prove something, like an achievement or a skill.

{% embed url="https://www.figma.com/board/DPGBfPLlss2K6KmDLCN3ul/LearnCard-Docs?node-id=131-661&p=f&t=fk1wywzjUFmakXJE-0" %}

## **What you'll accomplish:**

1. Set up a simple "Issuer" environment using the LearnCard SDK.
2. Design and create a "Workshop Completion" Verifiable Credential.
3. Digitally sign (issue) the credential to make it official.
4. Send this credential to your own LearnCard app using your Profile ID.
5. View the received credential in your LearnCard app.

**Why is this useful?** Understanding this basic flow is the first step to building applications that can issue digital badges, certificates, or any other kind of verifiable proof to users, empowering them with portable and trustworthy records.

{% embed url="https://codepen.io/Jacks-n-Smith/pen/YPPgyyM" fullWidth="false" %}

## **Prerequisites:**

1. **LearnCard App Installed:** You need the LearnCard app installed on your mobile device or accessible [as a web app](https://learncard.app/). This is where you'll receive and view the credential.
2. **Your LearnCard Profile ID:** You'll need your unique Profile ID from your LearnCard app.
   * **How to find it:** Open your LearnCard app, navigate to your profile section by clicking it in the upper right corner. Click "My Account." Copy the Profile ID accurately; it's case-sensitive and usually looks something like `@your-chosen-profile-id` or a longer unique string.
3. **Development Environment (for Issuing):**
   * Node.js installed on your computer.
   * A new project folder for this tutorial.
   *   LearnCard SDK installed. Open your terminal or command prompt in your project folder and run:Bash

       ```bash
       npm install @learncard/init @learncard/didkit-plugin
       # or
       # pnpm install @learncard/init @learncard/didkit-plugin
       # or
       # yarn add @learncard/init @learncard/didkit-plugin
       ```
4. **Basic Understanding:** While this is a beginner tutorial, a quick read of our [What is a Verifiable Credential?](../core-concepts/credentials-and-data/verifiable-credentials-vcs.md) and [What is a DID?](../core-concepts/identities-and-keys/decentralized-identifiers-dids.md) Core Concept pages will be helpful.

***

## Part 1: Setting Up Your Issuer Environment

For this tutorial, your computer will act as the "Issuer" – the entity creating and sending the credential.

### **Step 1.1: Create an Issuer Script**&#x20;

Create a new file in your project folder, for example, `issueCredential.ts` (if using TypeScript) or `issueCredential.js`.

### **Step 1.2: Initialize LearnCard SDK for the Issuer**&#x20;

This instance will represent your workshop organization.

```typescript
// issueCredential.ts
import { initLearnCard } from '@learncard/init';
// For Node.js, you might need to polyfill fetch or use a library like node-fetch
// global.fetch = require('node-fetch'); // Uncomment if needed in Node.js without native fetch

// If you're using DIDKit and need to provide the wasm file in Node.js,
// you might need a slightly different import or setup for the wasm.
// For simplicity, we'll assume basic init. Add wasm if your setup errors.

async function setupIssuerLearnCard() {
    // IMPORTANT: Replace 'your-unique-issuer-seed-phrase-or-hex-seed'
    // with a strong, unique seed for your issuer.
    // Keep this seed very secure if this were a real issuer!
    const issuerSeed = 'your-unique-issuer-seed-phrase-or-hex-seed-keep-safe';

    const learnCardIssuer = await initLearnCard({
        seed: issuerSeed, // This generates the Issuer's DID and keys
        network: true,     // We need network capabilities to send the credential
        allowRemoteContexts: true // We will issue a credential with a remote context 
    });

    console.log("Issuer LearnCard Initialized.");
    console.log("Issuer DID:", learnCardIssuer.id.did());
    return learnCardIssuer;
}

// (We'll call this function later)
```

This code initializes a LearnCard instance.&#x20;

{% hint style="info" %}
The `seed` is used to generate a unique Decentralized Identifier (DID) and cryptographic keys for your Issuer. In a real application, this seed must be kept extremely secure. [Learn more](../core-concepts/identities-and-keys/seed-phrases.md).
{% endhint %}

### **Step 1.3:  Ensure Issuer Has a Service Profile**&#x20;

To interact with the LearnCard Network effectively (like sending credentials), your Issuer's DID should be associated with a Service Profile.&#x20;

```typescript
// Add this function to issueCredential.ts

async function ensureIssuerProfile(learnCardIssuer: any) { // Use 'any' or the specific LearnCard type
    const issuerServiceProfileData = {
      profileId: 'my-awesome-workshop-issuer', // Choose a unique ID
      displayName: 'My Awesome Workshop Series',
      // Add other relevant details for your issuer profile
    };

    try {
        // Check if profile exists first, to avoid errors if run multiple times
        let profile = await learnCardIssuer.invoke.getProfile(issuerServiceProfileData.profileId);
        if (!profile) {
            console.log(`Creating service profile for issuer: ${issuerServiceProfileData.profileId}`);
            await learnCardIssuer.invoke.createServiceProfile(issuerServiceProfileData);
            console.log('Issuer Service Profile created successfully.');
        } else {
            console.log('Issuer Service Profile already exists.');
        }
    } catch (error) {
        console.error('Error ensuring issuer profile:', error.message);
        // If it's a "profile already exists" error, you might want to ignore it for this script
    }
}

// (We'll call this after setupIssuerLearnCard)
```

***

## Part 2: Designing Your "Workshop Completion" Credential

Now, let's define what information our "Workshop Completion" credential will hold.

### **Step 2.1: Define the Credential Content**&#x20;

A Verifiable Credential is a set of claims made by an Issuer about a Subject (the recipient).

<pre class="language-typescript"><code class="lang-typescript">// Add this to issueCredential.ts

// IMPORTANT: Replace with the Profile ID you got from YOUR LearnCard App
const recipientProfileId = 'YOUR_LEARNCARD_APP_PROFILE_ID'; 

// Retrieve recipient profile to retrieve their DID
const recipientProfile = await learnCardIssuer.invoke.getProfile(recipientProfileId);
if(!recipientProfile) {
    throw new Error("Recipient LearnCard Profile ID does not exist in LearnCloud Network.")
}
// This will also be the credentialSubject.id if the credential is about the recipient directly.
const recipientDidForCredential = recipientProfile.did;

const workshopCredentialContent = {
<strong>    // "@context" defines the vocabulary used (like a dictionary for terms)
</strong>    "@context": [
      "https://www.w3.org/2018/credentials/v1",
      "https://purl.imsglobal.org/spec/ob/v3p0/context-3.0.1.json",
      "https://ctx.learncard.com/boosts/1.0.0.json",
    ],
    // "type" specifies what kind of credential this is
    "type": [
      "VerifiableCredential",
      "OpenBadgeCredential",
      "BoostCredential"
    ] // Standard VC type + OpenBadge type + Boost type
    // "issuanceDate" will also be filled in automatically if not provided
    "issuanceDate": new Date().toISOString(), // Today's date
    // "issuer" will be filled in automatically by LearnCard SDK during signing, but we'll be explicit about it
    "issuer": learnCardIssuer.id.did(),
    "name": "LearnCard Basics Workshop",
     // "credentialSubject" is about whom or what the credential is
    "credentialSubject": {
      "achievement": {
        "achievementType": "Badge",
        "criteria": {
          "narrative": "Awarded for successfully completing the interactive LearnCard tutorial."
        },
        "description": "This badge was generated in the CodePen demonstration project in the LearnCard Developer Docs.",
        "id": "urn:uuid:" + crypto.randomUUID(), // Generate a unique ID
        "image": "https://example.com/badge-images/teamwork.png",
        "name": "LearnCard Basics Workshop",
        "type": [
          "Achievement"
        ]
      },
      "id": recipientDidForCredential, // The DID of the person who completed the workshop
      "type": [
        "AchievementSubject"
      ]
    },
    // Additional Boost Display Fields for Extra Customization
    "display": {
      "backgroundColor": "#40cba6",
      "displayType": "badge"
    },
    "image": "https://cdn.filestackcontent.com/YjQDRvq6RzaYANcAxKWE",
    // "proof" will be added automatically when the credential is signed
  };
</code></pre>

{% hint style="success" %}
✨ **Key Points:**

* **`@context`**: Tells systems how to interpret the fields.
* **`type`**: Helps categorize the credential. `VerifiableCredential` is standard.
* **`credentialSubject`**: This is the core information. The `id` here should be the DID of the person receiving the credential. For this tutorial, we're using the `recipientProfileId` (which you got from your app) to construct a DID.
{% endhint %}

***

## Part 3: Creating and Signing the Credential (Issuance)

Let's take the content and make it an official, signed Verifiable Credential.

### **Step 3.1: "Issue" / "Sign" the Unsigned Credential**&#x20;

The LearnCard SDK helps you with this:

```typescript
// Add this function to issueCredential.ts

async function createAndSignCredential(learnCardIssuer: any, unsignedVc: any) {
    console.log("Unsigned VC:", JSON.stringify(unsignedVc, null, 2));

    console.log("Now signing (issuing) the credential...");
    const signedVc = await learnCardIssuer.invoke.issueCredential(unsignedVc);
    console.log("Signed VC created successfully!");
    console.log(JSON.stringify(signedVc, null, 2));
    return signedVc;
}

// (We'll call this later)
```

{% hint style="info" %}
`issueCredential` adds the issuer's DID, issuance date, and a cryptographic signature, making it verifiable.
{% endhint %}

***

## Part 4: Sending the Credential to Your LearnCard App

Now, let's send this official credential to your LearnCard app.

### **Step 4.1: Use `sendCredential`**&#x20;

This function from the LearnCard SDK (via the Network plugin) handles the delivery.

```typescript
// Add this function to issueCredential.ts

async function sendVcToRecipient(learnCardIssuer: any, recipientLcnProfileId: string, signedVc: any) {
    console.log(`Sending credential to Profile ID: ${recipientLcnProfileId}`);
    try {
        // The 'encrypt' parameter is optional, defaults may vary.
        // For simplicity, we'll try without explicit encryption,
        // but in production, you'd likely want encryption (encrypt: true).
        const sentCredentialUri = await learnCardIssuer.invoke.sendCredential(
            recipientLcnProfileId,
            signedVc,
            // encrypt: true // Optional: consider encryption for sensitive credentials
        );
        console.log('Credential sent successfully! Sent Credential URI:', sentCredentialUri);
        return sentCredentialUri;
    } catch (error) {
        console.error('Error sending credential:', error);
        throw error;
    }
}

// (We'll call this later)
```

***

## Part 5: Putting It All Together & Viewing in Your App

Let's create a main function to run these steps.

### **Step 5.1: Main Script Logic**

```typescript
// Add this main execution block at the end of issueCredential.ts

async function main() {
    if (recipientProfileId === 'YOUR_LEARNCARD_APP_PROFILE_ID') {
        console.error("Please replace 'YOUR_LEARNCARD_APP_PROFILE_ID' with your actual Profile ID from the LearnCard app in the 'recipientProfileId' variable.");
        return;
    }
    if (await setupIssuerLearnCard().then(issuer => issuer.id.did() === 'did:key:z6Mkpissg9N3752fGusN7f5KkHobbWp8rW4xY8y3JYR8XnpZ')) { // Default DID for an empty seed, prompt user to change
        console.warn("You are using a default/empty seed for the issuer. Please change 'your-unique-issuer-seed-phrase-or-hex-seed-keep-safe' to a unique value for a real issuer.");
    }


    const learnCardIssuer = await setupIssuerLearnCard();
    await ensureIssuerProfile(learnCardIssuer); // Make sure the issuer has a service profile

    const signedVc = await createAndSignCredential(learnCardIssuer, workshopCredentialContent);

    if (signedVc) {
        await sendVcToRecipient(learnCardIssuer, recipientProfileId, signedVc);
        console.log("\nTutorial complete! Check your LearnCard app for the new credential.");
        console.log("It might take a moment to receive a notification.");
    } else {
        console.log("Credential creation or signing failed. Cannot send.");
    }
}

main().catch(err => console.error("Tutorial encountered an error:", err));
```

### **Step 5.2: Run Your Script**

1. **Replace Placeholders:**
   * In `issueCredential.ts`, find `YOUR_LEARNCARD_APP_PROFILE_ID` and replace it with the Profile ID you copied from your LearnCard app.
   * Also, replace `'your-unique-issuer-seed-phrase-or-hex-seed-keep-safe'` with your own unique string for the issuer's seed.
2. Save the file.
3. Open your terminal in your project directory and run:
   * If using TypeScript: `npx ts-node issueCredential.ts`
   * If using JavaScript: `node issueCredential.js`

### **Step 5.3: View in Your LearnCard App**&#x20;

After the script runs successfully, open your LearnCard app on your device. You should see the new "Workshop Completion Certificate" appear! It might take a few moments for you to get the notification, depending on how the app is configured.

***

## Summary & What's Next

Congratulations! You've successfully: ✅ Set up a basic Issuer using the LearnCard SDK. ✅ Defined, created, and digitally signed a Verifiable Credential. ✅ Sent that credential to your own LearnCard app.

This tutorial covers the fundamental flow of issuing credentials. From here, you can explore:

* Creating more complex credentials with different [**Schemas and Types**](../core-concepts/credentials-and-data/achievement-types-and-categories.md).
* Using [**ConsentFlows**](../core-concepts/consent-and-permissions/consentflow-overview.md) to manage data sharing before issuing credentials.
* Integrating this issuance logic into your own applications and backend services.

Explore the rest of our documentation to learn more about the powerful features of LearnCard!
