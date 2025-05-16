---
description: The (Deprecated) building block of the LearnCard URI
---

# VC Resolution

{% hint style="danger" %}
**Removed**

As of `@learncard/core@9.0.0`, this plugin has been removed. Please use the Read and Store Control Planes instead!
{% endhint %}

{% hint style="warning" %}
**Deprecated**

This plugin is now deprecated in favor of using the Read and Store Control Planes! It _will_ be removed in the future
{% endhint %}

The VC Resolution plugin doesn't do much on its own, but rather lays the groundwork for the LearnCard URI!

## LearnCard URI

The LearnCard URI is a [URI](https://en.wikipedia.org/wiki/Uniform\_Resource\_Identifier) that allows a Universal Wallet to resolve a credential. It is freely extensible and any plugin can add to it in any way. However standard plugins will adhere to a format of `lc:${method}:${location}`. For example, the IDX plugin adds `lc:ceramic:${streamID}` URI support.

## ResolveCredential

LearnCard URIs act as an alias to a credential, much like a URL acts as an alias to an IP Address. In order to get to that credential, we must _resolve_ the URI. This is done via the `resolveCredential` method exposed by this plugin. If a wallet is instantiated with _only_ the VC Resolution plugin, the `resolveCredential` method will simply error with a message saying that there are no plugins able to resolve the URI.&#x20;

## ResolutionExtension

In order to become useful, `resolveCredential` must be re-exposed by another plugin. This is made easier with the `ResolutionExtension` type exposed by this plugin.

The `ResolutionExtension` type can be used by plugins to implement a new LearnCard URI. In order to do this, the plugin will need to define its URI scheme, then intersect the `ResolutionExtension` type with the type of its methods.

## Dissecting the Ceramic Plugin

Let's look at an example: the Ceramic Plugin!

### Defining Types

The Ceramic plugin exposes lots of methods via the `CeramicPluginMethods` type, but we can mostly ignore them. With that in mind, the `CeramicPluginMethods` type looks something like this:

<pre class="language-typescript"><code class="lang-typescript">export type CeramicPluginMethods = {
//-- snip
<strong>} &#x26; ResolutionExtension&#x3C;CeramicURI>;
</strong></code></pre>

This type is then used in the function signature of `getCeramicPlugin` like this:

<pre class="language-typescript"><code class="lang-typescript">export const getCeramicPlugin = async (
    wallet: Wallet&#x3C;any, any, CeramicPluginDependentMethods>,
    //-- snip
<strong>): Promise&#x3C;Plugin&#x3C;'Ceramic', any, CeramicPluginMethods>> => {
</strong></code></pre>

The presence of `ResolutionExtension` in the `CeramicPluginMethods` type signature forces the return value of `getCeramicPlugin` to include a `resolveCredential` method that takes in a `CeramicURI` and returns a `VC`.

### CeramicURI

A Ceramic URI is a URI of the form `lc:ceramic:${streamID}`. In TypeScript, we can (and do) capture this with the type `` `lc:ceramic:${string}` `` though in practice, it is quite a bit easier to just treat it as a string.

What _is_ useful, however, is to be able to validate and parse these URIs. The Ceramic Plugin makes use of the [zod](https://github.com/colinhacks/zod) validation library to easily validate strings and ensure that they are Ceramic URIs:

```typescript
export const CeramicURIValidator = z
    .string()
    .refine(
        string => string.split(':').length === 3 && string.split(':')[0] === 'lc',
        'URI must be of the form lc:${storage}:${url}'
    )
    .refine(
        string => string.split(':')[1] === 'ceramic',
        'URI must use storage type ceramic (i.e. must be lc:ceramic:${streamID})'
    );
```

### The resolveCredential Method

With the above information in mind, let's take a quick look at how the Ceramic Plugin implements the `resolveCredential` method:

<pre class="language-typescript"><code class="lang-typescript">export const getCeramicPlugin = async (
    wallet: Wallet&#x3C;any, CeramicPluginDependentMethods>,
    //-- snip
): Promise&#x3C;Plugin&#x3C;'Ceramic', any, CeramicPluginMethods>> => {
    //-- snip

    return {
        methods: {
            //-- snip
            resolveCredential: async (_wallet, uri) => {
<strong>                const verificationResult = await CeramicURIValidator.spa(uri);
</strong><strong>                
</strong><strong>                if (!verificationResult.success) return wallet.pluginMethods.resolveCredential(uri);
</strong><strong>                
</strong><strong>                //-- Resolve Credential via Ceramic
</strong>            },
        }
    };
};
</code></pre>

Essentially, what this code is doing is validating the incoming URI to see if it is a Ceramic URI using the `CeramicURIValidator`. If it is _not_ a Ceramic URI, this plugin that passes it down to the existing wallet's `resolveCredential` method, giving other plugins the chance to take a crack at resolving this URI. If is _is_ a Ceramic URI, it goes about it's business resolving it!

This pattern is _extremely_ important when writing plugins that implement `ResolutionExtension`. If a plugin does not delegate resolution to the existing wallet when resolving a credential, it will effectively make all previous resolution extensions worthless!
