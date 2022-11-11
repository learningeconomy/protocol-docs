---
description: Get the holder's identity
---

# ID

## Description

The ID Control Plane is the interface responsible for managing the holder's identity. This means storing/managing key material.

Plugins that implement this Control Plane will generally need to be instantiated in some way, and with some kind of input, such as a seed/existing key material, or by making a request to a third party that can provide key material.

The ID Plane implements two methods: `did`, and `keypair`

### id.did

The `did` method (optionally) takes in a [method](https://www.w3.org/TR/did-core/#methods), and returns a did.

### id.keypair

The `keypair` method (optionally) takes in a cryptographic algorithm (e.g. ed25519, secp256k1, etc), and returns  a [JWK](https://www.rfc-editor.org/rfc/rfc7517).

## Example plugins that implement the ID Plane

{% content-ref url="../plugins/official-plugins/did-key.md" %}
[did-key.md](../plugins/official-plugins/did-key.md)
{% endcontent-ref %}
