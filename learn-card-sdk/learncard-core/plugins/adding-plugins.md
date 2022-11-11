---
description: Bringing it all together!
---

# Adding Plugins

In order to create a fully functioning LearnCard, you will need to add some plugins. Specifically, you will (probably) want to add at least one plugin that implements each Control Plane.

{% hint style="info" %}
To learn more about [Control Planes](../control-planes/), as well as find recommended Plugins for each Control Plane, click [here](../control-planes/)!
{% endhint %}

In code, constructing a LearnCard completely from scratch looks like this:

```typescript
const baseLearnCard = await initLearnCard({ custom: true });
const didkitLearnCard = await baseLearnCard.addPlugin(await getDidKitPlugin());
const didkeyLearnCard = await didkitLearnCard.addPlugin(await getDidKeyPlugin(didkitLearnCard, 'a', 'key'));
// repeat for any more plugins you'd like to add
```

However, you don't have to start from scratch! Each instantiation function is completely able to add bespoke plugins to it:

```typescript
const emptyLearnCard = await initLearnCard();
const customLearnCard = await emptyLearnCard.addPlugin(CustomPlugin);
```
