# LearnCard Network

### Using the LearnCard Network Plugin

The LearnCard Network Plugin (`@learncard/network-plugin`) simplifies the process of interacting with the LearnCard Network API by providing a set of convenient methods for managing profiles, connections, credentials, presentations, and boosts. This guide will help you understand how to use this plugin in your application.

#### Installation

First, install the LearnCard Network Plugin:

```bash
pnpm install @learncard/network-plugin
```

#### Initialization

To start using the LearnCard Network Plugin, you'll need to import it and initialize it with your application. Here's an example of how to do this:

```javascript
import { initLearnCard } from '@learncard/core'
import { getLearnCardNetworkPlugin } from '@learncard/network-plugin';
import didkit from '@learncard/core/dist/didkit/didkit_wasm_bg.wasm?url';

const lcnAPI = 'https://network.learncard.app/trpc';

const learnCard = await initLearnCard({
    seed,
    didkit,
});

const networkLearnCard = learnCard.addPlugin(
    await getLearnCardNetworkPlugin(learnCard, lcnAPI)
);
```

#### Accessing Plugin Methods

Once you've initialized the LearnCard Network Plugin, you can access the methods by calling `learnCard.invoke.<LearnCardNetworkPluginMethods>`. For example, to get a user's profile with a `profileId` of `johnsmith` you can call:

```javascript
await networkLearnCard.invoke.getProfile('johnsmith');
```

Here's a brief overview of the available methods in the `LearnCardNetworkPluginMethods`:

1. **Profile Management**: Create, update, delete, and retrieve user profiles.
2. **Connections**: Manage connections between users, including sending and accepting connection requests, and fetching connection information.
3. **Credentials**: Send, accept, retrieve, and delete credentials between users.
4. **Presentations**: Send, accept, retrieve, and delete presentations between users.
5. **Boosts**: Create, send, update, delete, and claim boosts for users on the network.
6. **Storage**: Resolve a URI to a credential or presentation.
7. **Signing Authorities**: Register and retrieve signing authorities for the LearnCard Network.

For detailed information on the method signatures and their parameters, refer to the [type definitions](https://github.com/learningeconomy/LearnCard/blob/main/packages/plugins/learn-card-network/src/types.ts) provided in the [`@learncard/network-plugin` package](https://github.com/learningeconomy/LearnCard/tree/main/packages/plugins/learn-card-network).

#### Examples

Here are a few examples of how to use the LearnCard Network Plugin in your application:

**Create a Profile**

```javascript
const profile = {
  profileId: 'johnsmith',
  displayName: 'John Smith',
  image: 'https://example.com/avatar.jpg',
};

await networkLearnCard.invoke.createProfile(profile);
```

**Connect with Another Profile**

```javascript
const profileId = 'janesmith';

await networkLearnCard.invoke.connectWith(profileId);
```

**Send a Credential**

```javascript
const profileId = 'janesmith';
const vc = await networkLearnCard.invoke.issueCredential(networkLearnCard.invoke.newCredential())
const encrypt = true;

await networkLearnCard.invoke.sendCredential(profileId, vc, encrypt);
```

**Claim a Boost**

```javascript
const boostUri = 'https://example.com/boost-uri';
const challenge = 'example-challenge';

await networkLearnCard.invoke.claimBoostWithLink(boostUri, challenge);
```

These examples demonstrate some of the ways you can interact with the LearnCard Network API using the `@learncard/network-plugin`.&#x20;
