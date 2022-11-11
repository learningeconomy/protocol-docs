---
description: Keep LearnCard Weird!
---

# Implementing Methods

Sometimes plugins need to expose some bespoke logic that doesn't fit neatly into one of the [Control Planes](../../control-planes/). Plugin methods allow plugins to expose this logic directly on the resulting LearnCard object.

We have already seen this in action in [The Simplest Plugin](the-simplest-plugin.md), but let's go into a bit more depth about what's happening here by making a quick plugin that implements a basic counter.

## Types

Before implementing methods on a Plugin object, it's best to get the types in order. In general, starting with the types can be easier to think through, and once they're in place, they can guide the implementation. To add types for methods, we use the third generic argument of [the `Plugin` type](the-plugin-type.md).

{% code title="src/types.ts" lineNumbers="true" %}
```typescript
import { Plugin } from '@learncard/core';

export type CounterPluginMethods = {
    getCounterValue: () => number;
    incrementCounter: () => void;
    resetCounter: () => void;
};

export type CounterPlugin = Plugin<'Counter', any, CounterPluginMethods>;
```
{% endcode %}

The types above have defined a Plugin with three methods: `get`, `increment`, and `reset`, which will provide basic counter controls.

## Implementation

### Skeleton

With the above types in place, we can build out a skeleton plugin before actually implementing anything:

{% code title="src/index.ts" lineNumbers="true" %}
```typescript
import { CounterPlugin } from './types';

export const getCounterPlugin = (): CounterPlugin => {
    return {
        name: 'Counter',
        methods: {
            getCounterValue: () => {},
            incrementCounter: () => {},
            resetCounter: () => {},
        },
    };
};
```
{% endcode %}

{% hint style="info" %}
We need to wrap the plugin in a `getCounterPlugin` function to be able to store the counter state later
{% endhint %}

### Implementing the Methods

With our boilerplate out of the way, implementing the Counter plugin will be a cakewalk! 🍰&#x20;

We will use the lexical scope of the `getCounterPlugin` function to store out counter state, and manipulate it via the exposed methods.

<pre class="language-typescript" data-title="src/index.ts" data-line-numbers><code class="lang-typescript">import { CounterPlugin } from './types';

export const getCounterPlugin = (): CounterPlugin => {
<strong>    let value = 0;
</strong><strong>    
</strong>    return {
        name: 'Counter',
        methods: {
<strong>            getCounterValue: () => value,
</strong><strong>            incrementCounter: () => {
</strong><strong>                value += 1;
</strong><strong>            },
</strong><strong>            resetCounter: () => {
</strong><strong>                value = 0;
</strong><strong>            },
</strong>        },
    };
};</code></pre>

Our plugin is now complete, and we have successfully implemented bespoke method. Easy as 🍰.&#x20;

Our plugin can be added to and used in a LearnCard like so:

```typescript
const counterLearnCard = await learnCard.addPlugin(getCounterPlugin());

counterLearnCard.invoke.getCounterValue(); // 0

counterLearnCard.invoke.incrementCounter();
counterLearnCard.invoke.getCounterValue(); // 1

counterLearnCard.invoke.incrementCounter();
counterLearnCard.invoke.incrementCounter();
counterLearnCard.invoke.getCounterValue(); // 3

counterLearnCard.invoke.resetCounter();
counterLearnCard.invoke.getCounterValue(); // 0
```
