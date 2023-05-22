---
description: Ceramic / IDX Config
---

# IDX Config

The `ceramicIdx` field is passed directly to the [Ceramic](../plugins/official-plugins/ceramic.md) and [IDX ](broken-reference)Plugins. If you'd like to use the WeLibrary public Ceramic node, you may omit passing this in. For reference, have a look at the [@glazed/did-datastore](https://developers.ceramic.network/reference/glaze/modules/did\_datastore/) documentation, as well as the [@ceramicnetwork/http-client](https://developers.ceramic.network/reference/core-clients/ceramic-http/) documentation. Additionally, we do expose one bespoke field, `credentialAlias`, which allows you to specify what IDX alias to use by default when storing/retrieving credentials.
