# DIDKit

LearnCard makes use of the wonderful rust library [didkit](https://github.com/spruceid/didkit) under the hood. However, because didkit is written in Rust, it must first be converted to [WebAssembly](https://webassembly.org/) before it can be used in the browser, resulting in a large (\~6.6 MB) .wasm file that must be delivered to users.

The naïve approach to this would be to simply include the wasm in the initial bundle that is sent with everything else. This has the advantage of being incredibly simple to implement, however because of the size of the wasm payload, it is simply impractical to do.

To overcome this huge payload, the wasm is retrieved asynchronously when instantiating a wallet, allowing [TTFCP](https://web.dev/fcp/) to stay low while still making use of the didkit library. There are two ways to achieve this, and Learn Card gives consumers both options.

### Public Endpoint

An up-to-date copy of the wasm payload is uploaded to WeLibrary's filestack, and its URL is used as a default if nothing else is provided during LearnCard construction. This has the benefit of being extremely simple for consumers to use, allowing you to not even think about didkit at all. However, this has the issue of being relatively slow in comparison to hosting the didkit wasm binary yourself.

### Hosting it Locally

The wasm binary is exposed in the npm package, and can be imported like so (depending on your specific server setup):

{% tabs %}
{% tab title="Webpack 5" %}
```typescript
import didkit from '@learncard/didkit-plugin/dist/didkit/didkit_wasm_bg.wasm';
```
{% endtab %}

{% tab title="Vite" %}
```typescript
import didkit from '@learncard/didkit-plugin/dist/didkit/didkit_wasm_bg.wasm?url';
```
{% endtab %}
{% endtabs %}

Doing the above will use your site's web server to host the wasm payload, allowing clients to download that payload faster (especially if you are using HTTP/2!) This method is also a bit safer. On the off-chance that `@learncard/didkit-plugin` updates the wasm payload without uploading the updated wasm and updating the default URL, you will still have the most up-to-date wasm payload!
