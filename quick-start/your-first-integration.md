---
description: Claim Your First Digital Badge in 5 Minutes!
---

# Your First Integration

Welcome to your first LearnCard integration! In just a few lines of code, you'll create a verifiable, claimable digital badge—what we call a **Boost**.

This quickstart helps you:

* Install LearnCard tools
* Create a demo issuer profile
* Generate a verifiable Boost (credential)
* Output a link that anyone can claim

No experience required. Just code, coffee, and a terminal.

### ⭐️ What You'll Be Making

{% embed url="https://codepen.io/Jacks-n-Smith/pen/KwwEbjY" fullWidth="false" %}

### 🧰 Installation

Choose your preferred package manager:

```bash
# Using npm
npm install @learncard/init @learncard/claimable-boosts-plugin @learncard/simple-signing-plugin

# Using yarn
yarn add @learncard/init @learncard/claimable-boosts-plugin @learncard/simple-signing-plugin

# Using pnpm
pnpm add @learncard/init @learncard/claimable-boosts-plugin @learncard/simple-signing-plugin

```

### 🚀 Quickstart Script

This script:

1. Initializes a LearnCard wallet
2. Creates an issuer profile
3. Defines a Boost template
4. Issues the Boost to the network
5. Generates a claim link for anyone to redeem

#### ✅ Prerequisites

* Node.js (v14+)
* A secure seed phrase (stored in `SECURE_SEED`)
* A unique ID for your issuer (e.g. `my-awesome-org-profile`)

#### 📁 Create `createBoost.js`:

```javascript
import { initLearnCard } from '@learncard/init';
import { getClaimableBoostsPlugin } from '@learncard/claimable-boosts-plugin';
import { getSimpleSigningPlugin } from '@learncard/simple-signing-plugin';

const seed = process.env.SECURE_SEED;
const profileId = 'my-awesome-org-profile';
const profileName = 'My Awesome Org';

if (!seed) {
  console.error('Error: SECURE_SEED environment variable is not set.');
  process.exit(1);
}

async function quickstartBoost() {
  try {
    console.log('Initializing LearnCard...');
    const learnCard = await initLearnCard({
      seed: seed,
      network: true,
      allowRemoteContexts: true
    });

    const signingLearnCard = await learnCard.addPlugin(
      await getSimpleSigningPlugin(learnCard, 'https://api.learncard.app/trpc')
    );

    const claimableLearnCard = await signingLearnCard.addPlugin(
      await getClaimableBoostsPlugin(signingLearnCard)
    );
    console.log('LearnCard initialized with plugins.');

    try {
      console.log(`Creating profile "${profileId}"...`);
      await claimableLearnCard.invoke.createProfile({
        profileId: profileId,
        displayName: profileName,
        description: 'Issuing awesome credentials.',
      });
      console.log(`Profile "${profileId}" created successfully.`);
    } catch (error) {
      if (error.message?.includes('Profile ID already exists')) {
        console.log(`Profile "${profileId}" already exists, continuing.`);
      } else {
        throw new Error(`Failed to create profile: ${error.message}`);
      }
    }

    console.log('Creating boost template...');
    const boostTemplate = await claimableLearnCard.invoke.newCredential({
      type: 'boost', 
      boostName: 'Quickstart Achievement',
      boostImage: 'https://placehold.co/400x400?text=Quickstart',
      achievementType: 'Influencer',
      achievementName:'Quickstart Achievement',
      achievementDescription: 'Completed the quickstart guide!',
      achievementNarrative: 'User successfully ran the quickstart script.',
      achievementImage: 'https://placehold.co/400x400?text=Quickstart'
    });
    console.log('Boost template created.');

    console.log('Creating boost on the network...');
    const boostUri = await claimableLearnCard.invoke.createBoost(
      boostTemplate,
      {
        name: boostTemplate.name,
        description: boostTemplate.achievementDescription,
      }
    );
    console.log(`Boost created with URI: ${boostUri}`);

    console.log('Generating claim link...');
    const claimLink = await claimableLearnCard.invoke.generateBoostClaimLink(boostUri);
    console.log('\n✅ Success! Your Claimable Boost link is ready:');
    console.log(claimLink);

    return claimLink;

  } catch (error) {
    console.error('\n❌ Error during quickstart process:', error);
    process.exit(1);
  }
}

quickstartBoost();

```

### 🏃‍♂️ Run the Script

1. Set your seed (demo only – never hardcode in production):

```bash
export SECURE_SEED="your-very-secret-seed-phrase-here"
```

2. Run the script:

```bash
node createBoost.js
```

### 🎉 What You'll See

The console will print a claimable URL like:

```arduino
✅ Success! Your Claimable Boost link is ready:
https://claim.learncard.app/boost/abc123...
```

Anyone with that link can scan or click to claim their badge. It’s a live verifiable credential issued by your script.

### ➡️ Next Steps

* 🔐 Add expiration, limits, or QR codes (see [Detailed Usage](../sdks/official-plugins/claimable-boosts.md))
* 🧠 Learn how Boosts work under the hood (see Core Concepts)
* 🛠️ Issue credentials dynamically in your app or game

**You just built your first digital credential.**\
You’ve touched real-world decentralized identity and verifiable credentials—with just a few lines of code.

We’re glad you’re here. Ready to build something great?
