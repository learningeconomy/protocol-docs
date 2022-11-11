---
description: Component for displaying the front face of a unique Card issued to a user
---

# LearnCard Front

{% embed url="https://627179acf7d591004aeca143-rcfucpryjx.chromatic.com/iframe.html?id=learncardcreditcardfrontface--learn-card-credit-card-front-face-test&viewMode=story" %}
Learn Card - Card Front Face
{% endembed %}

```tsx
import { LearnCardCreditCardFrontFace } from '@learncard/react';

const handleOnClick = () => {};

<LearnCardCreditCardFrontFace
   userImage="https://userimage.png"
   qrCodeValue="https://www.npmjs.com/package/@learncard/react"
   className="customClass"
   showActionButton
   actionButtonText="Open Card"
   onClick={handleOnClick}
/>
```

## Storybook Docs

{% hint style="info" %}
**Update the fields below, to see live changes! 🚀**

try: **`showActionButton: false`**
{% endhint %}

{% embed url="https://627179acf7d591004aeca143-rcfucpryjx.chromatic.com/?path=/docs/learncardcreditcardfrontface--learn-card-credit-card-front-face-test" %}



## Properties

### userImage

| **Description** | Image of the user issued the card |
| --------------- | --------------------------------- |
| **Type**        | `string \| undefined`             |
| **Default**     | `undefined`                       |

### qrCodeValue

| **Description** | value encoded as a QR code |
| --------------- | -------------------------- |
| **Type**        | `string \| undefined`      |
| **Default**     | `undefined`                |

### showActionButton

| **Description** | Show or hide the action button |
| --------------- | ------------------------------ |
| **Type**        | `boolean \| undefined`         |
| **Default**     | `false`                        |

### actionButtonText

|                 |                             |
| --------------- | --------------------------- |
| **Description** | Title for the action button |
| **Type**        | `string \| undefined`       |
| **Default**     | `'Open Card'`               |

### className

|                 |                       |
| --------------- | --------------------- |
| **Description** | Custom css class      |
| **Type**        | `string \| undefined` |
| **Default**     | `""`                  |

### onClick

| **Description** | Custom onClick handler    |
| --------------- | ------------------------- |
| **Type**        | `() => void \| undefined` |
| **Default**     | `() => {}`                |





