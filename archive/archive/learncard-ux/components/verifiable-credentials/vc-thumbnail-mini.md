---
description: Minified version of the VC Thumbnail for displaying a verifiable credential
---

# VC Thumbnail, Mini

{% embed url="https://627179acf7d591004aeca143-mtzhuexrnc.chromatic.com/iframe.html?args=&globals=backgrounds.value:!hex(F8F8F8)&id=minivcthumbnail--mini-vc-thumbnail-test&viewMode=story" %}

```tsx
import { MiniVCThumbnail } from '@learncard/react';

const handleOnClick = () => {};

<MiniVCThumbnail
   title="Hello World!"
   createdAt="June, 3 2022"
   issuerImage="https://issuerimage.png"
   badgeImage="https://badgeimage.png"
   className="customClass"
   onClick={handleOnClick}
/>
```

## Storybook Docs

{% hint style="info" %}
**Update the fields below, to see live changes! 🚀**

try: **`issuerImage: ""`**
{% endhint %}

{% embed url="https://627179acf7d591004aeca143-mtzhuexrnc.chromatic.com/iframe.html?args=&globals=backgrounds.value:!hex(F8F8F8)&id=minivcthumbnail--mini-vc-thumbnail-test&viewMode=docs" %}

## Properties

### title

| **Description** | Thumbnail title       |
| --------------- | --------------------- |
| **Type**        | `string \| undefined` |
| **Default**     | `undefined`           |

### createdAt

| **Description** | Credential issue date |
| --------------- | --------------------- |
| **Type**        | `string \| undefined` |
| **Default**     | `undefined`           |

### issuerImage

| **Description** | Credential issuer image |
| --------------- | ----------------------- |
| **Type**        | `string \| undefined`   |
| **Default**     | `undefined`             |

### badgeImage

| **Description** | Open badge image      |
| --------------- | --------------------- |
| **Type**        | `string \| undefined` |
| **Default**     | `undefined`           |

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
