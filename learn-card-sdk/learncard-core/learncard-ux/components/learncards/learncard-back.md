---
description: Component for displaying the back face of a unique Card issued to a user
---

# LearnCard Back

{% embed url="https://627179acf7d591004aeca143-rcfucpryjx.chromatic.com/iframe.html?id=learncardcreditcardbackface--learn-card-credit-card-back-face-test&viewMode=story" %}
Learn Card - Card Front Face
{% endembed %}

```tsx
import { 
   LearnCardCreditCardBackFace, 
   LearnCardCreditCardProps, 
   LearnCardCreditCardUserProps 
} from '@learncard/react';

const handleOnClick = () => {};

const user: LearnCardCreditCardUserProps = {
   fullName: 'Jane Doe',
   username: 'jane_doe_2022'
}

const card: LearnCardCreditCardProps = {
  cardNumber: "0000 0000 0000 0000",
  cardIssueDate: "2022",
  cardExpirationDate: "00/00",
  cardSecurityCode: "000"
}

<LearnCardCreditCardBackFace
   user={user}
   card={card}
   className="customClass"
/>
```

## Storybook Docs

{% hint style="info" %}
**Update the fields below, to see live changes! 🚀**
{% endhint %}

{% embed url="https://627179acf7d591004aeca143-rcfucpryjx.chromatic.com/?path=/docs/learncardcreditcardbackface--learn-card-credit-card-back-face-test" %}



## Properties

### user

| **Description** | user to display                             |
| --------------- | ------------------------------------------- |
| **Type**        | `LearnCardCreditCardUserProps \| undefined` |
| **Default**     | `undefined`                                 |

### card

| **Description** | card to display                        |
| --------------- | -------------------------------------- |
| **Type**        | `LearnCardCreditCardProps\| undefined` |
| **Default**     | `undefined`                            |

### className

|                 |                       |
| --------------- | --------------------- |
| **Description** | Custom css class      |
| **Type**        | `string \| undefined` |
| **Default**     | `undefined`           |





