---
description: ✈
---

# Implementing Control Planes

In order to promote convergence across Plugin APIs to support common functionality over complex workflows, plugins may choose to implement [Control Planes](../../control-planes/). Because each plane is slightly different, _how_ they are actually implemented will also be slightly different. For the most part, there are some standard conventions that plugins must follow when implementing methods for a plane.

To demonstrate this, let's build a plugin that implements the [Read](../../control-planes/read.md) and [Store](../../control-planes/store.md) planes using [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage).

## Types

Let's start with the types! We will use [the `Plugin` type](the-plugin-type.md) to define a Plugin that implements the Read and Store planes like so:

{% code title="src/types.ts" lineNumbers="true" %}
```typescript
import { Plugin } from '@learncard/core';

export type LocalStoragePlugin = Plugin<'LocalStorage', 'read' | 'store'>;
```
{% endcode %}

## Implementation

### Skeleton

Before actually implementing the localStorage functionality, let's build out the skeleton of what our implementation will look like:

<pre class="language-typescript" data-title="src/index.ts" data-line-numbers><code class="lang-typescript">import { LocalStoragePlugin } from './types';

export const getLocalStoragePlugin = (): LocalStoragePlugin => {
    return {
        name: 'LocalStorage',
<strong>        read: { get: () => {} },
</strong><strong>        store: { upload: () => {} },
</strong>        methods: {},
    };
};</code></pre>

Because we specified that this plugin is implementing the `read` and `store` planes, we _must_ include those keys in the returned `Plugin` object. The Read Plane requires we implement a `get` method, and the Store Plane requires we implement at least an `upload` method, so these methods have been stubbed out.

### Implementing the Store Plane

#### URI Scheme

Let's start by implementing the Store Plane! The [Store Plane docs](../../control-planes/store.md) mention that the `upload` method should return a [`URI`](../../uris.md), so we will now devise a URI scheme. It looks like this:

```typescript
`lc:localStorage:${id}`
```

Where `id` is the identifier used as a key in `localStorage`.

#### UUID

To easily create unique identifiers, we will use the [`uuid`](https://www.npmjs.com/package/uuid) npm package. Creating an ID using that package looks like this:

```typescript
import { v4 as uuidv4 } from 'uuid';
uuidv4(); // '9b1deb4d-3b7d-4bad-9bdd-2b0d7b3dcb6d'
```

#### Putting it all together

With our URI scheme defined and ID generation in place, let's implement our Store Plane!

<pre class="language-typescript" data-title="src/index.ts" data-line-numbers><code class="lang-typescript">import { v4 as uuidv4 } from 'uuid';

import { LocalStoragePlugin } from './types';

export const getLocalStoragePlugin = (): LocalStoragePlugin => {
    return {
        name: 'LocalStorage',
        read: { get: () => {} },
<strong>        store: { 
</strong><strong>            upload: async (_learnCard, vc) => {
</strong><strong>                const id = uuidv4();
</strong><strong>                
</strong><strong>                localStorage.setItem(id, JSON.stringify(vc));
</strong><strong>                
</strong><strong>                return `lc:localStorage:${id}`;
</strong><strong>            } 
</strong><strong>        },
</strong>        methods: {},
    };
};</code></pre>

{% hint style="info" %}
Wondering what that unused `_learnCard` variable is about? It's [the implicit LearnCard](the-implicit-learncard.md)! Check out what it is and how to use it [here](the-implicit-learncard.md)!
{% endhint %}

With this code in place, the Store Plane has successfully been implemented! Verifiable Credentials can now be stored by a LearnCard using this plugin with the following code:

```typescript
const uri = await learnCard.store.LocalStorage.upload(vc);
```

Now the we can _store_ credentials in localStorage, let's implement _getting_ them out!

### Implementing the Read Plane

To implement the Read Plane, we simply need to verify that the incoming `URI` is one that matches our scheme, and if so, read the value stored in localStorage! This can be done with the following code:

<pre class="language-typescript" data-title="src/index.ts" data-line-numbers><code class="lang-typescript">import { v4 as uuidv4 } from 'uuid';

import { LocalStoragePlugin } from './types';

export const getLocalStoragePlugin = (): LocalStoragePlugin => {
    return {
        name: 'LocalStorage',
<strong>        read: { 
</strong><strong>            get: async (_learnCard, uri) => {
</strong><strong>                const sections = uri.split(':');
</strong><strong>                
</strong><strong>                if (sections.length !== 3 || !uri.startsWith('lc:localStorage')) {
</strong><strong>                    return undefined; // Let another plugin resolve this URI!
</strong><strong>                }
</strong><strong>                
</strong><strong>                const storedValue = localStorage.getItem(sections[2]);
</strong><strong>                
</strong><strong>                return storedValue ? JSON.parse(storedValue) : undefined;
</strong><strong>            } 
</strong><strong>        },
</strong>        store: { 
            upload: async (_learnCard, vc) => {
                const id = uuidv4();
                
                localStorage.setItem(id, JSON.stringify(vc));
                
                return `lc:localStorage:${id}`;
            } 
        },
        methods: {},
    };
};</code></pre>

With this in place, the Read and Store planes have been implemented and LearnCards may use our plugin to store and retrieve credentials from localStorage with the following code:

```typescript
const uri = await learnCard.store.LocalStorage.upload(vc);

// ...Later

const vc = await learnCard.read.get(uri);
```
