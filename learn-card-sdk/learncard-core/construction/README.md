# Construction

Depending on your use-case and specific needs, constructing a LearnCard is likely as simple as the following code:

```typescript
import { initLearnCard } from '@learncard/core';

const learnCard = await initLearnCard({ seed: 'abc123' });
```

For a full description of instantiating a LearnCard by configuration, check out the full documentation on the [`initLearnCard`](initlearncard.md) function:

{% content-ref url="initlearncard.md" %}
[initlearncard.md](initlearncard.md)
{% endcontent-ref %}

## Key Generation

{% hint style="danger" %}
**There be dragons here.** 🐉&#x20;

In production environments, take great care and caution when generating and storing key material. Insufficient entropy or insecure storage, among other vectors, can easily compromise your data and identities.&#x20;
{% endhint %}

How to generate and store keys is left to you, the consumer. However, if you'd like to simply generate a random key, you can do so with the following code:

{% tabs %}
{% tab title="Browser" %}
```typescript
const randomKey = Array.from(crypto.getRandomValues(new Uint8Array(32)), dec =>
  dec.toString(16).padStart(2, "0")
).join("");
```
{% endtab %}

{% tab title="Node" %}
```typescript
import crypto from 'node:crypto';

const randomKey = crypto.randomBytes(32).toString('hex');
```
{% endtab %}
{% endtabs %}

To speed up instantiation of the wallet, you can host our[ didkit](https://github.com/spruceid/didkit) wasm binary yourself.

{% tabs %}
{% tab title="Webpack 5" %}
```typescript
import { initLearnCard } from '@learncard/core';
import didkit from '@learncard/core/dist/didkit/didkit_wasm_bg.wasm';

const learnCard = await initLearnCard({ seed: 'abc123', didkit });
```
{% endtab %}

{% tab title="Vite" %}
```typescript
import { initLearnCard } from '@learncard/core';
import didkit from '@learncard/core/dist/didkit/didkit_wasm_bg.wasm?url';

const learnCard = await initLearnCard({ seed: 'abc123', didkit });
```
{% endtab %}
{% endtabs %}

If you're curious about what the above code is doing, read more[ here](didkit.md).

## Ceramic/IDX config

The `ceramicIdx` field is passed directly to the [IDX Plugin](broken-reference). If you'd like to use the WeLibrary public Ceramic node, you may omit passing this in. For reference, have a look at the [@glazed/did-datastore](https://developers.ceramic.network/reference/glaze/modules/did\_datastore/) documentation, as well as the [@ceramicnetwork/http-client](https://developers.ceramic.network/reference/core-clients/ceramic-http/) documentation. Additionally, we do expose one bespoke field, `credentialAlias`, which allows you to specify what IDX alias to use by default when storing/retrieving credentials.
