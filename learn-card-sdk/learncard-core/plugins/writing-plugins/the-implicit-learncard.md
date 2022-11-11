---
description: Easily keep up-to-date!
---

# The Implicit LearnCard

## What is it?

When implementing [Control Planes](implementing-control-planes.md) or [Methods](implementing-methods.md), you may have noticed [an unused `_learnCard` parameter get added.](implementing-control-planes.md#putting-it-all-together) This is what we call the _Implicit LearnCard_, and it can be very helpful!

## What does it do?

The Implicit LearnCard allows your Plugin's methods to access an up-to-date version of the LearnCard that it has been added to. This means that you can have access to a full LearnCard without having to wrap your Plugin in a function!

## Why would you use it?

There are a few use-cases for using the Implicit LearnCard, such as:

* Calling a method that is implemented in the same plugin
* Ensuring the most up-to-date method is called

Let's implement a quick plugin that generates names to demonstrate this. The plugin will expose three methods: `generateFirstName`, `generateLastName`, and `generateFullName`. The types for this plugin look like this (using [the `Plugin` type](the-plugin-type.md)):

{% code title="src/types.ts" lineNumbers="true" %}
```typescript
import { Plugin } from '@learncard/core';

export type NamePluginMethods = {
    generateFirstName: () => string;
    generateLastName: () => string;
    generateFullName: () => string;
};

export type NamePluginType = Plugin<'Name', any, NamePluginMethods>;
```
{% endcode %}

The implementation for this plugin can have `generateFullName` easily call `generateFirstName` and `generateLastName` without having to define them outside of the function thanks to the Implicit LearnCard:

<pre class="language-typescript" data-title="src/index.ts" data-line-numbers><code class="lang-typescript">import { NamePluginType } from './types';

export const NamePlugin: NamePluginType = {
    name: 'Name',
    methods: {
        generateFirstName: () => 'First', // Not very useful....
        generateLastName: () => 'Last',   // Imagine a huge list of names being chosen at random
<strong>        generateFullName: learnCard => 
</strong><strong>            `${learnCard.invoke.generateFirstName()} ${learnCard.invoke.generateLastName()}`
</strong>    }
};</code></pre>

While this example may be a bit contrived, it _does_ demonstrate a few important benefits of the Implicit LearnCard:

* We were able to reuse plugin methods without defining them outside the plugin
* Other plugins are now able to override the functionality of `generateFirstName` and `generateLastName` and `generateFullName` will _automatically_ call the overriden methods!
  * This allows plugins to easily define interfaces for _sub-plugins_ or plugin extensions.
  * This also gives plugins the ability to monkey-patch pieces of another plugin, enhancing or changing that earlier plugin's functionality

## When would you not use it?

### Privacy

The Implicit LearnCard can be _very_ handy for plugin extensibility and composition. However, there are times you _don't_ want a plugin to be able to be monkey-patched or extended. In such a case, it is a better idea _not_ to use the Implicit LearnCard, and just define the re-usable functions outside the plugin:

<pre class="language-typescript" data-title="src/index.ts" data-line-numbers><code class="lang-typescript">import { NamePluginType } from './types';

export const getNamePlugin = (): NamePluginType => {
<strong>    const generateFirstName = () => 'First';
</strong><strong>    const generateLastName = () => 'Last';
</strong>    
    return {
        name: 'Name',
        methods: {
            generateFirstName, // Not very useful....
            generateLastName,   // Imagine a huge list of names being chosen at random
<strong>            generateFullName: learnCard => 
</strong><strong>                `${generateFirstName()} ${generateLastName()}`
</strong>        }
    };
};</code></pre>

### Plugin Extensions

Another reason not to use the Implicit LearnCard is when you _specifically_ want an old version of a method you are overriding. To demonstrate this, let's build a quick [Verification Extension](../official-plugins/vc/#verification-extension)

#### Types

Building a Verification Extension is super easy with the `VerifyExtension` type coming from the [VC Plugin](../official-plugins/vc/):&#x20;

{% code title="src/types.ts" lineNumbers="true" %}
```typescript
import { Plugin, VerifyExtension } from '@learncard/core';

export type ExtensionPlugin = Plugin<'Extension', any, VerifyExtension>;
```
{% endcode %}

<pre class="language-typescript" data-title="src/index.ts" data-line-numbers><code class="lang-typescript">import { LearnCard, VerifyExtension } from '@learncard/core';
import { ExtensionPlugin } from './types';

export const getExtensionPlugin = (
    learnCard: LearnCard&#x3C;any, any, VerifyExtension>
): ExtensionPlugin => ({
    name: 'Extension',
    methods: {
        verifyCredential: async (_learnCard, credential) => {
<strong>            const verificationCheck = await learnCard.invoke.verifyCredential(credential);
</strong>            
            verificationCheck.checks.push('Extension! 😄');
            
            return verificationCheck;
        }
    }
})</code></pre>

{% hint style="info" %}
See [Depending on Plugins](depending-on-plugins.md) for more information about how we are depending on a LearnCard with the `verifyCredential` method here.
{% endhint %}

The `VerifyExtension` type defines one method: `verifyCredential` that takes in a Verifiable Credential and returns a `VerificationCheck` object. To add our extension, we depend on a LearnCard that already has the `verifyCredential` function (using the same `VerifyExtension` type!), then call the _old_ `verifyCredential` function at the top of our _new_ `verifyCredential` function.

This pattern allows any number of plugins to add extra verification logic to the `verifyCredential` function easily!
