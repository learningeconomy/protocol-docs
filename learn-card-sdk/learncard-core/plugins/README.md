---
description: What is a plugin?
---

# Plugins

A plugin is a Plain Old Javascript Object that defines a set of functionality to be added to a Universal Wallet.

### Plugins Are:

* Core bundles of execution.
* Have no hard requirements they must conform to.
* Atomic.
* Not categorical.
* Typically fall into larger execution workflows. _See_ [_Control Planes_](../control-planes/)_._

Plugins can implement arbitrary functionality, or optionally choose to implement any number of Control Planes. Via a common instantiation pattern, it is also easily possible for plugins to depend on other plugins via their exposed interfaces, as well as to happily hold private and public fields.

Plugins are at the heart of LearnCard and the base LearnCard wallet without any plugins attached to it can do, well... nothing!&#x20;

Additionally, because plugins and plugin hierarchies work entirely through interfaces rather than explicit dependencies, any plugin can be easily hotswapped by another plugin that implements the same interface, and plugins implementing Control Planes can easily be stacked on top of each other to further enhance the functionality of that Control Plane for the wallet.
