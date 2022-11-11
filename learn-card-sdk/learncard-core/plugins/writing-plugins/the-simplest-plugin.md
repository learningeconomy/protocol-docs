# The Simplest Plugin

## Quick Start

### Boilerplate

Start with a basic TypeScript node package boilerplate. If you've never done that before, we recommend using [aqu](https://www.npmjs.com/package/aqu?activeTab=readme):&#x20;

{% hint style="info" %}
If you don't have aqu installed, you can install it globally with `npm i -g aqu.`
{% endhint %}

{% tabs %}
{% tab title="pnpm" %}
<pre class="language-bash"><code class="lang-bash"><strong>pnpm dlx aqu create simple-plugin
</strong>
? Pick package manager: pnpm
? Specify package description: ()
? Package author:
? Git repository (only for package.json information):
? Pick license: MIT
<strong>? Pick template: typescript
</strong>
cd simple-plugin</code></pre>
{% endtab %}

{% tab title="yarn" %}
<pre class="language-bash"><code class="lang-bash"><strong>yarn dlx aqu create simple-plugin
</strong>
? Pick package manager: yarn
? Specify package description: ()
? Package author:
? Git repository (only for package.json information):
? Pick license: MIT
<strong>? Pick template: typescript
</strong>
cd simple-plugin</code></pre>
{% endtab %}

{% tab title="npm" %}
<pre class="language-bash"><code class="lang-bash"><strong>npx aqu create simple-plugin
</strong>
? Pick package manager: npm
? Specify package description: ()
? Package author:
? Git repository (only for package.json information):
? Pick license: MIT
<strong>? Pick template: typescript
</strong>
cd simple-plugin</code></pre>
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you'd like to publish your plugin to npm for others to use, please see our documentation on [publishing plugins](publishing-a-plugin-to-npm.md)
{% endhint %}

### Install @learncard/core

Using your preferred package manager, install `@learncard/core`

{% tabs %}
{% tab title="pnpm" %}
```bash
pnpm i @learncard/core
```
{% endtab %}

{% tab title="yarn" %}
```bash
yarn add @learncard/core
```
{% endtab %}

{% tab title="npm" %}
```bash
npm i @learncard/core
```
{% endtab %}
{% endtabs %}

### Create the Types

To ease plugin development, it's best to start by defining the interface for your plugin. This can be done quite easily using [the `Plugin` type](the-plugin-type.md):

{% code title="src/types.ts" lineNumbers="true" %}
```typescript
import { Plugin } from '@learncard/core';

export type MyPluginMethods = {
    getFavoriteNumber: () => number;
};

export type MyPluginType = Plugin<'MyPluginName', any, MyPluginMethods>;
```
{% endcode %}

The preceding file defines a plugin named `MyPluginName` that exposes one method: `getFavoriteNumber`

### Create the Plugin

{% code title="src/index.ts" lineNumbers="true" %}
```typescript
import { MyPluginType } from './types';

export const MyPlugin: MyPluginType = {
    name: 'MyPluginName',
    methods: { getFavoriteNumber: () => 4 },
};
```
{% endcode %}

### Create a Test for Your Plugin

It's important to write tests for your plugins, so others can rely on them :thumbsup:

{% tabs %}
{% tab title="pnpm" %}
```bash
pnpm i --save-dev jest @types/jest
```
{% endtab %}

{% tab title="yarn" %}
```bash
yarn add jest @types/jest --dev
```
{% endtab %}

{% tab title="npm" %}
```bash
npm i --save-dev jest @types/jest
```
{% endtab %}
{% endtabs %}

Then, write your test:

{% code title="test/index.test.ts" lineNumbers="true" %}
```typescript
import { initLearnCard } from '@learncard/core';
import { MyPlugin } from '../src/index';

describe('MyPlugin', () => {
	it('should return my favorite number', async () => {
		const learnCard = await initLearnCard();
		const learnCardWithMyPlugin = await learnCard.addPlugin(MyPlugin);

		const favoriteNumber = learnCardWithMyPlugin.invoke.getFavoriteNumber();
		
		expect(favoriteNumber).toBe(4);
	});
});
```
{% endcode %}

If all looks good, you should be able to `pnpm test` and successfully pass the test:

<img src="../../../../.gitbook/assets/Screen Shot 2022-11-11 at 4.19.56 PM.png" alt="" data-size="original">

**That's it—you've got a simple plugin! 🎉**

Now you can add it to a LearnCard object:

```typescript
const learnCard = await initLearnCard();
const learnCardWithMyPlugin = await learnCard.addPlugin(MyPlugin);

console.log(learnCard.invoke.getFavoriteNumber()); // 4
```

For more info on adding plugins to a LearnCard:

{% content-ref url="../adding-plugins.md" %}
[adding-plugins.md](../adding-plugins.md)
{% endcontent-ref %}

For more info on constructing the LearnCard object:

{% content-ref url="../../construction/" %}
[construction](../../construction/)
{% endcontent-ref %}

To see how to publish this plugin to NPM for others to use:

{% content-ref url="publishing-a-plugin-to-npm.md" %}
[publishing-a-plugin-to-npm.md](publishing-a-plugin-to-npm.md)
{% endcontent-ref %}
