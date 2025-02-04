---
description: Thumbnail for displaying a verifiable credential
---

# VC Thumbnail



{% embed url="https://627179acf7d591004aeca143-mtzhuexrnc.chromatic.com/iframe.html?args=&id=vcthumbnail--vc-thumbnail-test&viewMode=story" %}
VC Thumbnail Full View
{% endembed %}

```tsx
import { VCThumbnail } from '@learncard/react';

const handleOnClick = () => {};

<VCThumbnail
   title="Hello World!"
   createdAt="June, 3 2022"
   issuerImage="https://issuerimage.png"
   userImage="https://userimage.png"
   badgeImage="https://badgeimage.png"
   listView={false}
   className="customClass"
   onClick={handleOnClick}
/>
```

## Storybook Docs

{% hint style="info" %}
**Update the fields below, to see live changes! 🚀**

try: **`listView: true`**
{% endhint %}

{% embed url="https://627179acf7d591004aeca143-mtzhuexrnc.chromatic.com/iframe.html?args=&globals=backgrounds.value:!hex(F8F8F8)&id=vcthumbnail--vc-thumbnail-test&viewMode=docs" %}



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

### userImage

| **Description** | Image of the user issued the credential |
| --------------- | --------------------------------------- |
| **Type**        | `string \| undefined`                   |
| **Default**     | `undefined`                             |

### badgeImage

| **Description** | Open badge image      |
| --------------- | --------------------- |
| **Type**        | `string \| undefined` |
| **Default**     | `undefined`           |

### listView

| **Description** | Specifies what style of thumbnail should display, by default it displays the full thumbnail.  |
| --------------- | --------------------------------------------------------------------------------------------- |
| **Type**        | `boolean \| undefined`                                                                        |
| **Default**     | `false`                                                                                       |

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





