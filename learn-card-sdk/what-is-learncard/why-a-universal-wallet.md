# Why a Universal Wallet?

### Overview

The wallet encapsulates the protocol as a standard interface developers can integrate into their applications. The wallet specification is open source and can be used by anyone. The purpose is to allow developers supporting VC exchange use cases to have a single library that handles all major procedures as outlined above, abstracting out specific details so they can focus on their own business logic.

### [Control Planes](../learncard-core/control-planes/)

Control Planes are a primary way for consumers to interact with a LearnCard. A Control Plane provides an abstraction for a higher-order wallet object to initiate complex workflows while being agnostic to the means of accomplishing the workflow. Control Planes align plugins based on primary action categories—such as Identity, Signing, Verification, Storage, and Communication—and specify interfaces for conforming plugins to implement.&#x20;

### [Plugins](why-a-universal-wallet.md#plugin-framework)

At the wallet’s core is a suite of plugins, enabling developers to choose what functionality they will support in their application.

Building the protocol as a set of plugins allows for standard protocol call patterns to improve over time with best practices. It prevents vendor lock-in and encourages support for a broad set of solutions.

### Providers

Plugins are provided by community and core contributors. Given the plugin’s nature, they may also host and maintain infrastructure necessary to sustain its call patterns. For example, an IPFS storage provider might also provide a pinning service, a DID document provider might host document endpoints, etc.

These details are to be provided along with the plugin.
