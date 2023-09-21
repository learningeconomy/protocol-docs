---
description: Trust, but verify
---

# Context

## Description

When working with [JSON-LD](https://json-ld.org/), such as with [Verifiable Credentials](https://www.w3.org/TR/vc-data-model/), you'll often need to resolve contexts. These contexts are themselves JSON-LD documents, being hosted at the URL embedded in the JSON-LD object. While it is easy enough to make a simple request to that URL and retrieve that document, there are many reasons why you might not want to do that every time. Most notably, for security and performance.

The Context Control Plane allows plugins to control how these JSON-LD contexts get resolved. Because it should be considered a security hole to resolve a context at runtime, plugins are expected to expose two different methods for static and dynamic resolution. On the final resulting `LearnCard` object, there is then only one method with an argument allowing for contexts to be resolved dynamically.

The Context Plane implements one method: `resolveDocument`

### context.resolveDocument

The `resolveDocument` method takes in the URI to a JSON-LD Context and returns the full JSON-LD Context. By passing in `true` as the second argument, contexts may be resolved dynamically.

### context.resolveStaticDocument \[For Plugins]

When creating a Plugin that implements the Context Plane, you _must_ implement the `resolveStaticDocument` method. This method simply does the same as the `LearnCard`-level `resolveDocument` method, but does not allow passing in a second argument to denote resolving dynamically.

### context.resolveRemoteDocument \[For Plugins]

When creating a Plugin that implements the Context Plane, you _may_ implement the `resolveRemoteDocument` method. This method is identical to `resolveStaticDocument`, but by using this method, you are signifying that contexts will be loaded dynamically.

## Security Considerations

Resolving JSON-LD contexts dynamically comes with some serious security implications! Please read the following for more detail: [https://www.w3.org/TR/json-ld11/#iana-security](https://www.w3.org/TR/json-ld11/#iana-security)

## Example Plugins that implement the Context Plane

{% content-ref url="../plugins/official-plugins/didkit.md" %}
[didkit.md](../plugins/official-plugins/didkit.md)
{% endcontent-ref %}

{% content-ref url="../plugins/official-plugins/dynamic-loader.md" %}
[dynamic-loader.md](../plugins/official-plugins/dynamic-loader.md)
{% endcontent-ref %}
