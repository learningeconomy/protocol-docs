# Advanced xAPI Statement Queries

### Filtering Large Statement Sets

When dealing with large statement volumes or statements with extensive data in extensions, you can use the following techniques to retrieve more manageable subsets of data.

#### Basic Query Parameters

The xAPI API supports several query parameters to limit and filter your results:

```typescript
// Basic query with filtering
const queryParams = new URLSearchParams({
  agent: JSON.stringify(actor),
  limit: "10",                             // Limit to 10 results
  since: "2024-03-01T00:00:00Z",           // Only statements after this date
  until: "2024-03-31T23:59:59Z",           // Only statements before this date
  verb: "http://adlnet.gov/expapi/verbs/completed" // Only specific verb
});

const response = await fetch(`${endpoint}/statements?${queryParams}`, {
  method: 'GET',
  headers: {
    'Content-Type': 'application/json',
    'X-Experience-API-Version': '1.0.3',
    'X-VP': jwt
  }
});
```

#### Key Filtering Parameters

| Parameter   | Description                               | Example                                           |
| ----------- | ----------------------------------------- | ------------------------------------------------- |
| `limit`     | Maximum number of statements to return    | `limit=20`                                        |
| `since`     | ISO 8601 date to filter statements after  | `since=2024-03-01T00:00:00Z`                      |
| `until`     | ISO 8601 date to filter statements before | `until=2024-03-31T23:59:59Z`                      |
| `verb`      | Filter by verb ID                         | `verb=http://adlnet.gov/expapi/verbs/completed`   |
| `activity`  | Filter by activity ID                     | `activity=http://yourgame.com/activities/level-1` |
| `ascending` | Return in ascending order (oldest first)  | `ascending=true`                                  |

#### Using Pagination

For very large datasets, implement pagination:

```typescript
// First page
let more = "";
const getPage = async (more) => {
  const url = more || `${endpoint}/statements?${queryParams.toString()}`;
  
  const response = await fetch(url, {
    method: 'GET',
    headers: {
      'Content-Type': 'application/json',
      'X-Experience-API-Version': '1.0.3',
      'X-VP': jwt
    }
  });
  
  const data = await response.json();
  
  // Process the statements
  processStatements(data.statements);
  
  // Check if there are more pages
  return data.more || null;
};

// Initial request
more = await getPage();

// Get next page if available
if (more) {
  more = await getPage(more);
}
```

#### Reducing Statement Size

If dealing with extremely large data in extensions:

1. **Reference Instead of Embed**: Store large data elsewhere and include a reference URL in your statement:

```javascript
extensions: {
  "http://yourdomain.com/xapi/extensions/detailed-data": {
    dataId: "123abc",
    dataUrl: "https://storage.yourdomain.com/data/123abc.json"
  }
}
```

2. **Summarize Data**: Include only essential information in statements:

```javascript
extensions: {
  "http://yourdomain.com/xapi/extensions/user-progress": {
    level: "intermediate",
    completionPercentage: 68,
    keyMetrics: ["accuracy:85%", "speed:72", "participation:high"]
  }
}
```

### Specialized Queries

#### Activity-Specific Statements

To retrieve all statements about a specific activity regardless of verb:

```typescript
const activityParams = new URLSearchParams({
  agent: JSON.stringify(actor),
  activity: "http://yourdomain.com/activities/skill-assessment"
});

const response = await fetch(`${endpoint}/statements?${activityParams}`, {
  // headers as before
});
```

#### Timeline Analysis

To analyze progress over time, sort statements in chronological order:

```typescript
const timelineParams = new URLSearchParams({
  agent: JSON.stringify(actor),
  ascending: "true",
  since: "2024-01-01T00:00:00Z"
});

const response = await fetch(`${endpoint}/statements?${timelineParams}`, {
  // headers as before
});
```

#### Skill-Based Filtering

To filter statements related to a specific skill or competency:

```typescript
const skillParams = new URLSearchParams({
  agent: JSON.stringify(actor),
  activity: "http://yourdomain.com/skills/problem-solving"
});

const response = await fetch(`${endpoint}/statements?${skillParams}`, {
  // headers as before
});
```

#### Completion Status

To find all completed activities:

```typescript
const completedParams = new URLSearchParams({
  agent: JSON.stringify(actor),
  verb: "http://adlnet.gov/expapi/verbs/completed",
  since: "2024-01-01T00:00:00Z"
});

const response = await fetch(`${endpoint}/statements?${completedParams}`, {
  // headers as before
});
```

#### Aggregation Queries

To retrieve summary data rather than individual statements:

```typescript
// First, retrieve statements with aggregation parameter
const aggregateParams = new URLSearchParams({
  agent: JSON.stringify(actor),
  verb: "http://adlnet.gov/expapi/verbs/experienced",
  since: "2024-01-01T00:00:00Z",
  format: "ids" // Retrieve only IDs for faster processing
});

const response = await fetch(`${endpoint}/statements?${aggregateParams}`, {
  // headers as before
});

// Then process locally to generate summaries
const statements = await response.json();
const activityCounts = {};

statements.forEach(statement => {
  const activityId = statement.object.id;
  activityCounts[activityId] = (activityCounts[activityId] || 0) + 1;
});

// Now activityCounts shows frequency of each activity
```

### Best Practices for Large Data Sets

1. **Use IDs Effectively**: Query by specific activity IDs to get only statements related to particular challenges or learning objectives
2. **Time-Based Queries**: Filter by recent time periods when monitoring current progress
3. **Aggregate First**: If analyzing patterns, consider creating aggregated statements that summarize multiple detailed statements
4. **Batch Processing**: For analysis, retrieve data in small batches and process incrementally
5. **Cache Common Queries**: If your application frequently needs the same filtered view, consider caching the results
