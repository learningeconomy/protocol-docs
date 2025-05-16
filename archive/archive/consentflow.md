---
description: >-
  ConsentFlow contracts allow you to read and write to a LearnCard with the
  consent of the LearnCard owner
---

# ConsentFlow OLD

## Creating a ConsentFlow Contract

### 1. Start up the LearnCard CLI

`pnpm dlx @learncard/cli`

### 2. Create a Network LearnCard

`const networkLearnCard = await initLearnCard({ seed: '[your secure key]', network: true })`

### 3. Create a service profile ([docs](broken-reference))

```
const serviceProfile = {
  displayName: 'Learning Platform',
  profileId: 'learningplatform',
  image: 'https://example.com/service-avatar.jpg',
};

await networkLearnCard.invoke.createServiceProfile(serviceProfile);
```

### 4. Create a contract

```typescript
const exampleConsentFlowContract = {
    "name": "Docs Contract",
    "subtitle": "Example contract for The Docs",
    "description": "Look here. This is how you ConsentFlow contract.",
    "image": "https://media-be.chewy.com/wp-content/uploads/2022/09/27110948/cute-dogs-hero-1024x615.jpg",
    "contract": {
        "read": {
            "anonymize": true,
            "credentials": {
                "categories": {
                    "Social Badge": {
                        "required": false
                    },
                    "Achievement": {
                        "required": true
                    }
                }
            },
            "personal": {
                "Name": {
                    "required": false
                }
            }
        },
        "write": {
            "credentials": {
                "categories": {
                    "ID": {
                        "required": true
                    },
                    "Learning History": {
                        "required": false
                    }
                }
            },
            "personal": {
                "SomeCustomID": {
                    "required": true
                }
            }
        }
    }
};

const contractUri = await networkLearnCard.invoke.createContract(exampleConsentFlowContract);
```

Supported values for credential categories are:

* `Achievement`
* `Accommodation`
* `Accomplishment`
* `Course`
* `ID`
* `Job`
* `Learning History`
* `Membership`
* `Merit Badge`
* `Skill`
* `Social Badge`
* `Work History`

#### Additional Fields

If you'd like to set an expiration for your contract you can use the `expiresAt` parameter e.g.

```
"expiresAt": "2022-02-22T12:34:56.789Z" // ISO format
```

If your contract is inteded for minors use the `needsGuardianConsent`parameter

```
"needsGuardianConsent": true
```

If you'd like to specify a url to direct a user to after they've consented to use the `redirectUrl`parameter

Upon consenting to the contract users will be redirected to this url with the consenting user's did added as a url parameter

```
"redirectUrl": "https://yourUrl.com"

// User will be redirected to "https://yourUrl.com?did=..."
```

### 5. Generate URL

This is the url that users will use to consent to this contract

`` const url = `https://learncard.app/consent-flow?uri=${contractUri}` ``

Additionally, you can specify a url to return to after the user has consented to the contract (note: redirect urls must begin with `http://` or `https://`)

`` const urlWithRedirect = `https://learncard.app/consent-flow?uri=${contractUri}&returnTo=${redirectUrl}` ``

### 6. (optional) Get Listed in LearnCard

If you want your ConsentFlow contract to be displayed in [learncard.app/launchpad](https://learncard.app/launchpad), please contact LearningEconomy (support@learningeconomy.io) with the uri of your contract



## Reading From a ConsentFlow Contract

### 1. Retrieve the ConsentFlow data for a contract

`let data = await networkLearnCard.invoke.getConsentFlowData(contractUri)`

This will return paginated records in the form of:

```
{
    cursor: string;   // ISO date string used for pagination
    hasMore: boolean; // whether there are more records
    records: {
        credentials: {
            categories: {
                [categoryName]: string[]; // array of credential uris 
            };
        };
        personal: {
            [personalFieldName]: string;
        };
        date: string;
    }[];
}
```

To retrieve the next page of paginated results use

```
if (data.hasMore) {
    data = await networkLearnCard.invoke.getConsentFlowData(contractUri, { cursor: data.cursor } )
}
```

### 2. Read Credential

Use the credential uri to read the user's credential

```
// For example, if the user at records[0] has shared an Achievement via this contract
const credentialUri = data.records[0].credentials.categories['Achievement'][0];

// Read the credential
const credential = await networkLearnCard.read.get(credentialUri);
```

### 3. (optional) Do a little dance

✨💃🪩🕺✨

