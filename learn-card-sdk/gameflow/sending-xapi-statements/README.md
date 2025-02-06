---
description: >-
  This guide explains how to send learning activity data to LearnCloud using the
  xAPI (Experience API) standard. LearnCloud is a service that collects and
  tracks learning experiences across different pl
---

# Sending xAPI Statements

## Overview

### Prerequisites

Before you begin, you'll need:

* A LearnCloud-provided JWT token for authentication
* A DID (Decentralized Identifier) for the user
* The LearnCloud xAPI endpoint URL
  * [https://cloud.learncard.com/xapi](https://cloud.learncard.com/xapi)

If you _don't_ have any of these, check out the [Game Flow docs ](../)and come back here.

### Understanding Key Concepts

#### What is xAPI?

xAPI (Experience API) is a specification that allows you to track learning experiences. It uses a simple structure of "Actor - Verb - Object" to describe activities, similar to how you might say "John completed the course" in plain English.

#### What is a DID?

A DID (Decentralized Identifier) is a unique identifier for your user that works across different systems. Think of it like an email address that works everywhere but is more secure and private.

### Basic Implementation

Here's how to send an xAPI statement to LearnCloud:

```typescript
interface XAPIStatement {
    actor: {
        objectType: "Agent";
        name: string;
        account: {
            homePage: string;
            name: string;
        };
    };
    verb: {
        id: string;
        display: {
            "en-US": string;
        };
    };
    object: {
        id: string;
        definition: {
            name: { "en-US": string };
            description: { "en-US": string };
            type: string;
        };
    };
}

async function sendXAPIStatement(
    statement: XAPIStatement, 
    jwt: string, 
    endpoint: string = "https://cloud.learncard.com/xapi"
) {
    const response = await fetch(`${endpoint}/statements`, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'X-Experience-API-Version': '1.0.3',
            'X-VP': jwt
        },
        body: JSON.stringify(statement)
    });
    
    return response;
}
```

### Tracking Game Activities

Here are examples of tracking different activities in a skills-building game:

#### 1. Tracking Activity Attempts

```typescript
// When a player starts a new challenge
const attemptStatement = {
    actor: {
        objectType: "Agent",
        name: userDid,  // Use the user's DID here
        account: {
            homePage: "https://www.w3.org/TR/did-core/",
            name: userDid
        }
    },
    verb: {
        id: "http://adlnet.gov/expapi/verbs/attempted",
        display: {
            "en-US": "attempted"
        }
    },
    object: {
        id: "http://yourgame.com/activities/level-1-challenge",
        definition: {
            name: { "en-US": "Level 1 Challenge" },
            description: { "en-US": "First challenge of the game" },
            type: "http://adlnet.gov/expapi/activities/simulation"
        }
    }
};
```

#### 2. Tracking Skill Development

```typescript
// When a player demonstrates a skill
const skillStatement = {
    actor: {
        objectType: "Agent",
        name: userDid,
        account: {
            homePage: "https://www.w3.org/TR/did-core/",
            name: userDid
        }
    },
    verb: {
        id: "http://adlnet.gov/expapi/verbs/demonstrated",
        display: {
            "en-US": "demonstrated"
        }
    },
    object: {
        id: "http://yourgame.com/skills/problem-solving",
        definition: {
            name: { "en-US": "Problem Solving" },
            description: { "en-US": "Successfully solved a complex game challenge" },
            type: "http://adlnet.gov/expapi/activities/skill"
        }
    }
};
```

#### 3. Tracking Achievements with Results

```typescript
// When a player completes a milestone with specific metrics
const achievementStatement = {
    actor: {
        objectType: "Agent",
        name: userDid,
        account: {
            homePage: "https://www.w3.org/TR/did-core/",
            name: userDid
        }
    },
    verb: {
        id: "http://adlnet.gov/expapi/verbs/mastered",
        display: {
            "en-US": "mastered"
        }
    },
    object: {
        id: "http://yourgame.com/achievements/speed-runner",
        definition: {
            name: { "en-US": "Speed Runner" },
            description: { "en-US": "Completed level with exceptional speed" },
            type: "http://adlnet.gov/expapi/activities/performance"
        }
    },
    result: {
        success: true,
        completion: true,
        extensions: {
            "http://yourgame.com/xapi/extensions/completion-time": "120_seconds",
            "http://yourgame.com/xapi/extensions/score": "95"
        }
    }
};
```

### Common Gotchas and Tips

1. **DID Usage**: Always use the same DID in both `actor.name` and `actor.account.name`. This DID should come from your authentication process.
2. **Verb Selection**: Use standard xAPI verbs when possible. Common ones include:
   * attempted
   * completed
   * mastered
   * demonstrated
   * failed
   * progressed
3. **Activity IDs**: Use consistent, unique URLs for your activity IDs. They don't need to be real URLs, but they should be unique identifiers following URL format.
4. **Authentication**: The JWT token should be sent in the `X-VP` header. This is specific to LearnCloud's implementation.
5. **Error Handling**: Always implement proper error handling:

```typescript
try {
    const response = await sendXAPIStatement(statement, jwt);
    if (!response.ok) {
        const error = await response.json();
        console.error('xAPI Statement Error:', error);
    }
} catch (err) {
    console.error('Network Error:', err);
}
```

### Testing Your Implementation

Before sending real user data, test your implementation with sample statements. Verify that:

1. The authentication works (200 status code)
2. The statements are properly formatted
3. The DIDs are correctly included in both required locations
4. The verbs and activity types make sense for your use case

### Need Help?

If you encounter issues or need clarification:

1. Check that your JWT token is valid
2. Verify your statement structure matches the examples
3. Ensure all required fields are present
4. Contact LearnCloud support if issues persist
