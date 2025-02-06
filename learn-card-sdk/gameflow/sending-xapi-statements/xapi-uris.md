---
description: URL/URI Best Practices in xAPI Statements
---

# xAPI URIs



### Understanding Activity IDs

When creating xAPI statements, you'll encounter two types of URLs:

1. **Standard xAPI Verbs**: These are predefined by ADL (Advanced Distributed Learning) and should be used as-is:

```javascript
verb: {
    id: "http://adlnet.gov/expapi/verbs/completed",
    display: {
        "en-US": "completed"
    }
}
```

2. **Activity IDs**: These are URIs you create to identify your activities:

```javascript
object: {
    id: "http://yourgame.com/activities/level-1/custom-challenge",
    definition: {
        name: { "en-US": "Level 1 Custom Challenge" },
        description: { "en-US": "First custom challenge of the game" },
        type: "http://adlnet.gov/expapi/activities/simulation"
    }
}
```

### Best Practices for Activity IDs

#### 1. Structure

* Use a consistent URI pattern
* Include meaningful path segments
* Keep IDs human-readable when possible

#### 2. Documentation

Best practice is to make these URIs resolvable to actual documentation. For example:

```javascript
// Good: Links to actual documentation
object: {
    id: "https://docs.yourgame.com/xapi/activities/custom-challenge",
    // ...
}

// Also acceptable, but less ideal: Non-resolvable URI
object: {
    id: "http://yourgame.com/activities/custom-challenge",
    // ...
}
```

If the URI is resolvable, it should lead to:

* Activity description
* Expected outcomes
* Related skills or competencies
* Usage context
* Any other relevant metadata

#### 3. Persistence

* Once you define an activity ID, maintain it
* Create new IDs for new versions of activities
* Don't reuse IDs for different activities

#### 4. Domain Usage

You can use:

* A domain you control (preferred)
* A made-up domain (acceptable)
* A subdomain specific to xAPI activities

The key is consistency and uniqueness within your system, but making URIs resolvable to actual documentation is strongly recommended for better interoperability and clarity.

Remember: While non-resolvable URIs are technically valid, resolvable URLs that link to activity definitions make your xAPI implementation more maintainable and useful to others who might need to understand your learning activities.
