---
description: What is a LearnCard?
---

# The LearnCard Type

To add better type safety to a project using LearnCards, it is _highly_ recommended you use TypeScript and take advantage of the `LearnCard` type.

## How to use the `LearnCard` type

### Option 1: Specify a list of plugins

If you know the exact order and number of plugins you have, you can use the `LearnCard` type to specify a `LearnCard` with those plugins like so:

```typescript
import { LearnCard } from '@learncard/core';
import { PluginA, PluginB, PluginC } from './plugins';

type CustomLearnCard = LearnCard<[PluginA, PluginB, PluginC]>;
```

With this code, `CustomLearnCard` will automatically infer all methods and planes implemented by `PluginA`, `PluginB`, and `PluginC`!

### Option 2: Specify implemented planes and/or methods

If you don't know the exact order and number of plugins you have, but you know that you would like to specify a `LearnCard` that implements certain planes or methods, you can do that like this:

```typescript
import { LearnCard } from '@learncard/core';

type ImplementsIdPlane = LearnCard<any, 'id'>;
type ImplementsFoo = LearnCard<any, any, { foo: () => 'bar'; }>;
type ImplementsBoth = LearnCard<any, 'id', { foo: () => 'bar': }>;
```

With this code, `ImplementsIdPlane` will accept any `LearnCard` that has plugins that implement the [ID](../../control-planes/id.md) [Control Plane](../../control-planes/), `ImplementsFoo` will accept any `LearnCard` that implements a method named `foo` that returns `'bar'`, and `ImplementsBoth` will accept any `LearnCard` that implements both.
