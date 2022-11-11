---
description: Standing on the Shoulders of Giants
---

# Depending on Plugins

While it is useful for [The Simplest Plugin](the-simplest-plugin.md) to add its own isolated logic to a LearnCard, part of the beauty of LearnCard plugins is to _depend_ on other plugins 💪&#x20;

Plugin dependence comes in two flavors:&#x20;

* Depending on a [Control Plane](../../control-planes/)&#x20;
* Depending on one or more [methods](implementing-methods.md).

## Boilerplate Plugins

To demonstrate this, let's create a simple base plugin, as well as two plugins that we will depend on: one for Control Planes, and one for methods.

### Base Plugin

{% code title="src/dependence/types.ts" lineNumbers="true" %}
```typescript
import { Plugin } from '@learncard/core';

export type DependencePluginType = Plugin<'Dependence', any, { bar: () => 'baz' }>;
```
{% endcode %}

{% code title="src/dependence/index.ts" lineNumbers="true" %}
```typescript
import { DependencePluginType } from './types';

export const DependencePlugin: DependencePluginType = {
    name: 'Dependence',
    methods: { bar: () => 'baz' },
};
```
{% endcode %}

### Control Plane Plugin

{% code title="src/controlplane/types.ts" lineNumbers="true" %}
```typescript
import { Plugin } from '@learncard/core';

export type ControlPlanePluginType = Plugin<'Control Plane', 'id'>;
```
{% endcode %}

{% code title="src/controlplane/index.ts" lineNumbers="true" %}
```typescript
import { ControlPlanePluginType } from './types';

export const ControlPlanePlugin: ControlPlanePluginType = {
    name: 'Control Plane',
    id: {
        did: () => { throw new Error('TODO'); },
        keypair: () => { throw new Error('TODO'); },
    },
    methods: {},
}
```
{% endcode %}

### Methods Plugin

{% code title="src/methods/types.ts" lineNumbers="true" %}
```typescript
import { Plugin } from '@learncard/core';

export type MethodsPluginMethods = {
    foo: () => 'bar';
};

export type MethodsPluginType = Plugin<'Methods', any, MethodsPluginMethods>;
```
{% endcode %}

{% code title="src/methods/index.ts" lineNumbers="true" %}
```typescript
import { MethodsPluginType } from './types';

export const MethodsPlugin: MethodsPluginType = {
    name: 'Methods',
    methods: { foo: () => 'bar' },
}
```
{% endcode %}

## Dependence Convention

As a convention, plugins will often be wrapped inside of a constructor function that requires a [LearnCard](the-learncard-type.md) of a certain type be passed in.

Let's update our base plugin to see what that looks like:

<pre class="language-typescript" data-title="src/dependence/types.ts" data-line-numbers><code class="lang-typescript">import { Plugin } from '@learncard/core';

<strong>export type DependencePlugin = Plugin&#x3C;'Dependence', any, { bar: () => 'baz' }>;</strong></code></pre>

<pre class="language-typescript" data-title="src/dependence/index.ts" data-line-numbers><code class="lang-typescript"><strong>import { LearnCard } from '@learncard/core';
</strong>import { DependencePlugin } from './types';

<strong>export const getDependencePlugin: (learnCard: LearnCard&#x3C;any>): DependencePluginType => ({
</strong>    name: 'Dependence',
    methods: { bar: () => 'baz' },
<strong>});</strong></code></pre>

With this change, LearnCards that would like to add our plugin will now look slightly different:

```typescript
// Old
const withPlugin = await learnCard.addPlugin(DependencePlugin);

// New
const withPlugin = await learnCard.addPlugin(getDependencePlugin(learnCard));
```

## Adding dependency requirements

### Depending on Planes

Now that we're requiring a LearnCard be passed in, we are able to add requirements to the dependent LearnCard! Let's take a look at what that looks like by attempting to take a dependency on the [Control Plane Plugin](depending-on-plugins.md#control-plane).

{% hint style="info" %}
**Note**: The LearnCard SDK does _not_ support depending on literal plugins. It only supports depending on what plugins _implement_. In practice, this makes plugins much more flexible and easy to work with, allowing dependent plugins to be hot-swapped easily as long as they implement the same dependent methods/planes.
{% endhint %}

<pre class="language-typescript" data-title="src/dependence/index.ts" data-line-numbers><code class="lang-typescript">import { LearnCard } from '@learncard/core';
import { DependencePlugin } from './types';

<strong>export const getDependencePlugin: (learnCard: LearnCard&#x3C;any, 'id'>): DependencePluginType => {
</strong><strong>    console.log('Successfully depended on a Control Plane!', learnCard.id.did());
</strong>    
    return {
        name: 'Dependence',
        methods: { bar: () => 'baz' },
    };
};</code></pre>

The operative change is right here on line 4:

```typescript
//                                                           VVVV
export const getDependencePlugin: (learnCard: LearnCard<any, 'id'>): DependencePluginType => {
//                                                           ^^^^
```

This change allows us to call `learnCard.id.did` on line 5, and requires consumers of this plugin to pass in a LearnCard that [implements](implementing-control-planes.md) the [ID](../../control-planes/id.md) plane when adding this plugin. For example, all of the following code will throw errors:

{% tabs %}
{% tab title="Passing in an empty wallet" %}
```typescript
import { initLearnCard } from '@learncard/core';

const learnCard = await initLearnCard({ custom: true });

const errors = await learnCard.addPlugin(getDependencePlugin(learnCard));
// TS Error: Property 'id' is missing
```
{% endtab %}

{% tab title="Passing in an incorrect wallet" %}
```typescript
import { initLearnCard } from '@learncard/core';

const learnCard = await initLearnCard();

const errors = await learnCard.addPlugin(getDependencePlugin(learnCard));
// TS Error: Property 'id' is missing
```
{% endtab %}

{% tab title="Incorrect plugin config" %}
<pre class="language-typescript"><code class="lang-typescript">// --snip--
<strong>export const getDependencePlugin: (learnCard: LearnCard&#x3C;any>): DependencePluginType => {
</strong>    console.log(learnCard.id.did());
    // TS Error: Property 'id' does not exist</code></pre>
{% endtab %}
{% endtabs %}

### Depending on Methods

Depending on a specific method (or methods) rather than a Control Plane looks very similar. To demonstrate this, let's stop depending on the ID Plane for a moment, and instead just depend on the `foo` method from the [Methods Plugin](depending-on-plugins.md#methods).

<pre class="language-typescript" data-title="src/dependence/index.ts" data-line-numbers><code class="lang-typescript">import { LearnCard } from '@learncard/core';
import { DependencePlugin } from './types';

<strong>export const getDependencePlugin: (learnCard: LearnCard&#x3C;any, any, { foo: () => 'bar' }>): DependencePluginType => {
</strong><strong>    console.log('Successfully depended on a Method!', learnCard.invoke.foo());
</strong>    
    return {
        name: 'Dependence',
        methods: { bar: () => 'baz' },
    };
};</code></pre>

The operative change is, once again, on line 4:

```typescript
//                                                                VVVVVVVVVVVVVVVVVVVV
export const getDependencePlugin: (learnCard: LearnCard<any, any, { foo: () => 'bar' }>): DependencePluginType => {
//                                                                ^^^^^^^^^^^^^^^^^^^^
```

With this change in place, just like when we depended on a Control Plane, we are now able to call `learnCard.invoke.foo` on line 5. We also now require consumers of this plugin to pass in a LearnCard with a plugin that [implements](implementing-methods.md) the `foo` method. For example, all of the following code will throw errors:

{% tabs %}
{% tab title="Passing in an empty wallet" %}
```typescript
import { initLearnCard } from '@learncard/core';

const learnCard = await initLearnCard({ custom: true });

const errors = await learnCard.addPlugin(getDependencePlugin(learnCard));
// TS Error: Property 'foo' is missing
```
{% endtab %}

{% tab title="Passing in an incorrect wallet" %}
```typescript
import { initLearnCard } from '@learncard/core';

const learnCard = await initLearnCard();

const errors = await learnCard.addPlugin(getDependencePlugin(learnCard));
// TS Error: Property 'foo' is missing
```
{% endtab %}

{% tab title="Incorrect plugin config" %}
<pre class="language-typescript"><code class="lang-typescript">// --snip--
<strong>export const getDependencePlugin: (learnCard: LearnCard&#x3C;any>): DependencePluginType => {
</strong>    console.log(learnCard.invoke.foo());
    // TS Error: Property 'foo' does not exist</code></pre>
{% endtab %}
{% endtabs %}

## Adding Type Safety to The Implicit LearnCard

Thus far, when adding dependency requirements, we have _only_ added type safety to the argument of our constructor function. This works quite well, but does _not_ provide type safety to the [Implicit LearnCard](the-implicit-learncard.md) passed into every method. To add this type safety, we use the fourth and fifth generic arguments of [the `Plugin` type](the-plugin-type.md)

Let's demonstrate this by first depending on both the [Control Plane Plugin](depending-on-plugins.md#control-plane-plugin) _and_ the [Methods Plugin](depending-on-plugins.md#methods-plugin), then adding some logic that uses the Implicit LearnCard to take advantage of that dependency:

<pre class="language-typescript" data-title="src/dependence/index.ts" data-line-numbers><code class="lang-typescript">import { LearnCard } from '@learncard/core';
import { DependencePlugin } from './types';

<strong>export const getDependencePlugin: (learnCard: LearnCard&#x3C;any, 'id', { foo: () => 'bar' }>): DependencePluginType => {
</strong>    return {
        name: 'Dependence',
        methods: { 
<strong>            bar: _learnCard => {
</strong><strong>                 // these two calls with throw TS errors!
</strong><strong>                 console.log('Did is:', _learnCard.id.did());
</strong><strong>                 console.log('Foo is:', _learnCard.invoke.foo());
</strong><strong>            
</strong><strong>                return 'baz';
</strong><strong>            } 
</strong>        },
    };
};</code></pre>

Because we haven't added our dependencies to the `DependencePlugin` type itself, TS has no way of knowing that the Implicit LearnCard implements the ID Plane and the `foo` method! We can easily fix this by updating the `DependencePlugin` type:

<pre class="language-typescript" data-title="src/dependence/types.ts" data-line-numbers><code class="lang-typescript">import { Plugin } from '@learncard/core';

//                                                                             VVVVVVVVVVVVVVVVVVVVVVVVVV
<strong>export type DependencePlugin = Plugin&#x3C;'Dependence', any, { bar: () => 'baz' }, 'id', { foo: () => 'bar' }>;
</strong>//                                                                             ^^^^^^^^^^^^^^^^^^^^^^^^^^</code></pre>

With these in place, TS will know to add the ID Plane and the `foo` method to the Implicit LearnCard, and the above errors will go away!
