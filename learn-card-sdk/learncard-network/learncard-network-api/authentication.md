# Authentication

### Authenticating with the LearnCard Network API

To interact with the LearnCard Network API, you can choose one of two ways to authenticate:

1. Using the LearnCard Network Plugin (`@learncard/network-plugin`) which handles authentication for you. **(Preferred option)**
2. Directly through the API endpoints using challenge-based DID Authentication.

#### 1. Using LearnCard Network Plugin

To authenticate using the LearnCard Network Plugin (`@learncard/network-plugin`), first install the package:

```bash
pnpm install @learncard/network-plugin
```

Then, either instantiate a LearnCard Network enabled LearnCard, or add the Network Plugin to an existing LearnCard:

{% tabs %}
{% tab title="Direct Instantiation" %}
{% code lineNumbers="true" %}
```typescript
import { initLearnCard } from '@learncard/init';
import didkit from '@learncard/didkit-plugin/dist/didkit/didkit_wasm_bg.wasm?url';

const networkLearnCard = await initLearnCard({
    seed,
    network: true,
    didkit,
});
```
{% endcode %}
{% endtab %}

{% tab title="Add Plugin" %}
```typescript
import { initLearnCard } from '@learncard/core'
import { getLearnCardNetworkPlugin } from '@learncard/network-plugin';
import didkit from '@learncard/core/dist/didkit/didkit_wasm_bg.wasm?url';

const lcnAPI = 'https://network.learncard.app/trpc';

const learnCard = await initLearnCard({
    seed,
    didkit,
});

const networkLearnCard learnCard.addPlugin(
    await getLearnCardNetworkPlugin(learnCard, lcnAPI)
);
```
{% endtab %}
{% endtabs %}

When using the LearnCard Network Plugin, challenge-based DID Authentication is handled for you, so no further steps are necessary.

#### 2. Using Challenge-based DID Authentication

If you choose to use the API endpoints directly, you'll need to manage challenge-based DID Authentication for each request. Here's a simplified TypeScript example to help you implement this authentication method:

```typescript
 
async function getClient(
  url = 'https://network.learncard.com/api': string,
  didAuthFunction: (challenge?: string) => Promise<string>
) {
  let challenges: string[] = [];

  const getChallenges = async (amount = 95 + Math.round((Math.random() - 0.5) * 5)): Promise<string[]> => {
    // Call the API to get a list of challenges
    // Replace this line with your preferred way of making API calls
    const response = await fetch(url + "/challenges?amount=" + amount);
    return await response.json();
  };

  challenges = await getChallenges();

  async function getAuthHeaders() {
    if (challenges.length === 0) challenges.push(...(await getChallenges()));
    return { Authorization: `Bearer ${await didAuthFunction(challenges.pop())}` };
  }

  // Use getAuthHeaders in your API calls to set the Authorization header
}

export default getClient;
```

In this example, we first define a `getClient` function that takes a `url` and a `didAuthFunction`. The `didAuthFunction` should be an asynchronous function that returns a signed challenge as a string.

The `getChallenges` function fetches a list of challenges from the API. The `getAuthHeaders` function generates an Authorization header using the `didAuthFunction` and a challenge. This header can then be used in your API calls.

### API Quick Reference

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/challenges" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}

{% swagger src="https://network.learncard.com/docs/openapi.json" path="/did" method="get" %}
[https://network.learncard.com/docs/openapi.json](https://network.learncard.com/docs/openapi.json)
{% endswagger %}
