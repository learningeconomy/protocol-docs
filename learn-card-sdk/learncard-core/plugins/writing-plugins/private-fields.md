---
description: >-
  Are you on the list? I can't give you access to these fields unless you're on
  the list.
---

# Private Fields

Sometimes it is important for a Plugin to keep private state/data. This can be done using the lexical scope of the constructor function described in [Depending on Plugins](depending-on-plugins.md#dependence-convention)!

To demonstrate this, let's build a quick secret message plugin that gates a string behind a password. This plugin will use a constructor function that takes in a message and a password, exposing a `getMessage` method that will return the message if the correct password is passed in and `changePassword`/`changeMessage` methods that allow updating the password/message.

{% code title="src/types.ts" lineNumbers="true" %}
```typescript
import { Plugin } from '@learncard/core';

export type SecretMessagePluginMethods = {
    getMessage: (password: string) => string;
    changePassword: (oldPassword: string, newPassword: string) => boolean;
    changeMessage: (message: string, password: string) => boolean;
};

export type SecretMessagePlugin = Plugin<'Secret Message', any, SecretMessagePluginMethods>;
```
{% endcode %}

<pre class="language-typescript" data-title="src/index.ts" data-line-numbers><code class="lang-typescript">import { SecretMessagePlugin } from './types';

export const getSecretMessagePlugin = (message: string, password: string): SecretMessagePlugin => {
<strong>    let currentMessage = message;
</strong><strong>    let currentPassword = password;
</strong>    
    return {
        name: 'Secret Message',
        methods: {
            getMessage: (_learnCard, _password) => {
<strong>                if (_password !== currentPassword) throw new Error('Wrong password!');
</strong>                
<strong>                return currentMessage;
</strong>            },
            changePassword: (_learnCard, oldPassword, newPassword) => {
<strong>                if (oldPassword !== currentPassword) throw new Error('Wrong password!');
</strong>                
<strong>                currentPassword = newPassword;
</strong>                
                return true;
            },
            changeMessage: (_learnCard, newMessage, _password) => {
<strong>                if (_password !== currentPassword) throw new Error('Wrong password!');
</strong>                
<strong>                currentMessage = newMessage;
</strong>                
                return true;
            },
        },
    };
};</code></pre>

This plugin can be used like so:

```typescript
const secretMessageLearnCard = await learnCard.addPlugin(getSecretMessagePlugin('nice', 'pw'));

secretMessageLearnCard.invoke.getMessage(); // Error: Wrong password!
secretMessageLearnCard.invoke.getMessage('pw') // 'nice'

secretMessageLearnCard.invoke.changePassword('pw', 'test') // true
secretMessageLearnCard.invoke.getMessage('pw') // Error: Wrong password!
secretMessageLearnCard.invoke.getMessage('test') // 'nice'

secretMessageLearnCard.invoke.changeMessage('Neat!', 'test') // true
secretMessageLearnCard.invoke.getMessage('test') // 'Neat!'
```
