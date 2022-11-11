---
description: What is a plugin?
---

# The Plugin Type

If you're creating a plugin, it is _highly_ recommended you use TypeScript and take advantage of the `Plugin` type.

## How to use the `Plugin` Type

### Complex Example Plugin

The `Plugin` type is a [generic](https://www.typescriptlang.org/docs/handbook/2/generics.html) type, taking in up to five total generic parameters. A Plugin using all five parameters would look like this:

{% code title="Complex Plugin" %}
```typescript
import { Plugin } from '@learncard/core';

type Methods = { foo: () => 'bar' }';
type DependentMethods = { bar: () => 'baz' };

type ComplexPlugin = Plugin<'Complex', 'store', Methods, 'id', DependentMethods>;
```
{% endcode %}

This type describes a plugin named `'Complex'` that implements the [Store](../../control-planes/store.md) [Control Plane](../../control-planes/), as well as the method `foo`. This plugin is also [dependent](depending-on-plugins.md) on plugins that implement the [ID](../../control-planes/id.md) Control Plane, as well as the method _bar_.

Let's break down what each of these arguments are doing one at a time.

### Arg 1: Name

```typescript
//                          VVVVVVVVV
type ComplexPlugin = Plugin<'Complex', 'store', Methods, 'id', DependentMethods>;
//                          ^^^^^^^^^
```

This argument simply names a plugin. It is a required string, and is used by some Control Planes.

Specifying a name will force objects that have been set to this type to use that name!

### Arg 2: Planes Implemented

```typescript
//                                     VVVVVVV
type ComplexPlugin = Plugin<'Complex', 'store', Methods, 'id', DependentMethods>;
//                                     ^^^^^^^
```

This argument specifies which [Control Planes](../../control-planes/) the plugin implements. It can be:

* `any` or `never`, which specifies that this plugin does not implement any Control Planes
* A single string (such as used in the example above), which specifies that this plugin implements a single Control Plane
* A [union](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html#union-types) of strings (e.g. `'store' | 'read'`), which specifies that this plugin implements multiple Control Planes

This argument defaults to `any`, specifying that this plugin does not implement any Control Planes.

Specifying one or more Control Planes implemented will force objects that have been set to this type to implement those planes!

### Arg 3: Methods Implemented

```typescript
//                                              VVVVVVV
type ComplexPlugin = Plugin<'Complex', 'store', Methods, 'id', DependentMethods>;
//                                              ^^^^^^^
```

This argument specifies which [methods](implementing-methods.md) the plugin implements. It is an object whose values are functions.

This argument defaults to `Record<never, never>`, specifying that this plugin does not implement any methods.

Specifying methods implemented will force objects that have been set to this type to implement those methods!

### Arg 4: Dependent Planes

```typescript
//                                                       VVVV
type ComplexPlugin = Plugin<'Complex', 'store', Methods, 'id', DependentMethods>;
//                                                       ^^^^
```

This argument specifies which [Control Planes](../../control-planes/) the plugin depends on. It can be:

* `any` or `never`, which specifies that this plugin does not depend on any Control Planes
* A single string (such as used in the example above), which specifies that this plugin depends on a single Control Plane
* A [union](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html#union-types) of strings (e.g. `'store' | 'read'`), which specifies that this plugin depends on multiple Control Planes

This argument defaults to `never`, specifying that this plugin does not depend on any Control Planes.

Specifying one or more Dependent Control Planes will add those planes to the [implicit LearnCard](the-implicit-learncard.md) passed into each plugin method!

{% hint style="warning" %}
Specifying Dependent Planes here will _not_ force LearnCards to implement those planes when adding this plugin! Please see [Depending on Plugins](depending-on-plugins.md) for more information.
{% endhint %}

### Arg 5: Dependent Methods

```typescript
//                                                             VVVVVVVVVVVVVVVV
type ComplexPlugin = Plugin<'Complex', 'store', Methods, 'id', DependentMethods>;
//                                                             ^^^^^^^^^^^^^^^^
```

This argument specifies which [methods](implementing-methods.md) the plugin depends on. It is an object whose values are functions.

This argument defaults to `Record<never, never>`, specifying that this plugin does not depend on any methods.

Specifying dependent methods will add those methods to the [implicit LearnCard](the-implicit-learncard.md) passed into each plugin method!

{% hint style="warning" %}
Specifying Dependent Methods here will _not_ force `LearnCards` to implement those methods when adding this plugin! Please see [Depending on Plugins](depending-on-plugins.md) for more information.
{% endhint %}
