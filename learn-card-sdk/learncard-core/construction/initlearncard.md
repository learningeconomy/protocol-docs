---
description: One Function to Rule Them All
---

# initLearnCard

While there are many init functions that are exposed and that can be used, we recommend instead sticking to the `initLearnCard` function.

`initLearnCard` is a config-driven, heavily overloaded function, that allows you to construct a wallet flexibly, without sacrificing type safety.

Under the hood, it is simply a map between the config you provide and the init function you would normally need to call, meaning calls like `initLearnCard()` and `emptyLearnCard()` are identical.

## Example Usage

```typescript
import { initLearnCard } from '@learncard/core';

// Constructs an empty LearnCard without key material (can not sign VCs). 
// Useful for Verifying Credentials only in a light-weight form.
const emptyLearncard = await initLearnCard();

// Constructs a LearnCard from a deterministic seed. 
const learncard = await initLearnCard({ seed: 'abc123' });

// Constructs a LearnCard default connected to VC-API at https://bridge.learncard.com for handling signing
const defaultApi = await initLearnCard({ vcApi: true });

// Constructs a LearnCard connected to a custom VC-API, with Issuer DID specified.
const customApi = await initLearnCard({ vcApi: 'vc-api.com', did: 'did:key:123' });

// Constructs a LearnCard connected to a custom VC-API that implements /did discovery endpoint.
const customApiWithDIDDiscovery = await initLearnCard({ vcApi: 'https://bridge.learncard.com' });

// Constructs a LearnCard with no plugins. Useful for building your own bespoke LearnCard
const customLearnCard = await initLearnCard({ custom: true });
```

The examples above are not exhaustive of possible ways to instantiate a LearnCard:

* For more on initialization with a VC-API, check out the [VC-API Plugin](../plugins/official-plugins/vc-api.md).&#x20;
* For more info on instantiating a wallet with a seed, click [here](learncardfromseed.md).
* For more info on instantiating an empty wallet, click [here](emptylearncard.md).&#x20;
