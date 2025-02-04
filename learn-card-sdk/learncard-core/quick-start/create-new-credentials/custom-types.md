# Custom Types

### **Overview**

**`Custom AchievementTypes`**, include the **`ext:`** prefix and allow for user-defined or external achievements. These custom types must adhere to specific formatting rules.

#### **Rules for Custom Types**

1. **Prefix**: Custom types must begin with **`ext:`**.
2.  **Validation**: Custom types must match the regex:

    ```typescript
    ^([a-zA-Z]+\s*){3,25}$
    ```
3.  **Structure**: Custom types follow this format:

    ```typescript
    ext:LCA_CUSTOM:<CategoryType>:<TransformedAchievementType>
    ```

    Example: `ext:LCA_CUSTOM:Learning History:The_Coolest_Dog`

***

#### **Formatting Logic**

Custom types are formatted using helper functions:

**Capitalize Words**

Converts lowercase strings like `cool cat` to `Cool Cat`:

```typescript
const capitalizeWordsAfterSpace = (str: string): string => {
    return str.replace(/(?:^|\s)\w/g, (match) => match.toUpperCase());
};
```

**Replace Spaces with Underscores**

Converts "Cool Cat" to "Cool\_Cat":

```typescript
const replaceWhiteSpacesWithUnderscores = (str: string): string => {
    return str.replace(/\s+/g, '_');
};
```

**Construct the Final Type**

Combines the category and transformed achievement type:

```typescript
const constructCustomType = (categoryType: string, customAchievementType: string) => {
    const capitalized = capitalizeWordsAfterSpace(customAchievementType);
    const transformed = replaceWhiteSpacesWithUnderscores(capitalized);
    return `ext:LCA_CUSTOM:${categoryType}:${transformed}`;
};
```

Example:

```typescript
constructCustomType("Learning History", "The Coolest Dog");
// Output: ext:LCA_CUSTOM:Learning History:The_Coolest_Dog
```

***

#### **Internal Handling of Custom Types**

Custom types are processed internally using the following helper functions:

**Check if a Type is Custom**

This function checks if a given type string contains the **`LCA_CUSTOM`** identifier:

```typescript
export const isCustomType = (str: string): boolean => {
    const regex = /LCA_CUSTOM/;
    const result = regex.test(str);
    return result;
};
```

**Extract Achievement Type from Custom Type**

This function extracts the specific achievement type from a custom type string:

```typescript
export const getAchievementTypeFromCustomType = (str: string) => {
    // ie: str -> "ext:LCA_CUSTOM:Learning History:The_Coolest_Dog";
    const regex = /^((?:[^:]+:){3})([^:]+)/;
    const result = str.match(regex)?.[2]; // "The_Coolest_Dog"
    return result;
};
```

**Extract Category Type from Custom Type**

This function extracts the category type from a custom type string:

```typescript
export const getCategoryTypeFromCustomType = (str: string) => {
    // ie: str -> "ext:LCA_CUSTOM:Learning History:The_Coolest_Dog";
    const regex = /(?:[^:]*:){2}([^:]*)(?::|$)/;
    const result = str.match(regex)?.[1]; // "Learning History"
    return result;
};
```

***

### **FAQ**

#### **How do I pass a type into a credential?**

Types can be passed into credentials using the `newCredential` method. Here is an example:

1.  **Passing a standard type:**

    ```typescript
    // Returns an unsigned, achievement credential
    const achievementCredential = learnCard.invoke.newCredential({ type: 'CommunityService' });
    ```
2.  **Passing a custom type:**

    ```typescript
    // Returns an unsigned, custom credential
    const customCredential = learnCard.invoke.newCredential({ type: 'ext:LCA_CUSTOM:Learning History:The_Coolest_Dog' });
    ```

**Can I create new categories?**

No, our system only supports the following pre defined categories&#x20;

```typescript
export const CATEGORIES = {    
    Achievement: 'Achievement',
    ID: 'ID',
    LearningHistory: 'Learning History',
    WorkHistory: 'Work History',
    SocialBadge: 'Social Badge',
    Membership: 'Membership',
    Accomplishment: 'Accomplishment',
    Accommodation: 'Accommodation',
    Family: 'Family',
};
```

#### **How do I validate a custom type?**

Use the **`CUSTOM_TYPE_REGEX`** to ensure compliance:&#x20;

```typescript
/^([a-zA-Z]+\s*){3,25}$/;
```

You can also test the formatting of your custom type to ensure it works internally:

1.  **Check if the type is custom:** Use the **`isCustomType`** function:

    ```typescript
    const isCustom = isCustomType('ext:LCA_CUSTOM:Learning History:The_Coolest_Dog');
    console.log(isCustom); // Output: true
    ```
2.  **Extract the achievement type:** Use the **`getAchievementTypeFromCustomType`** function:

    ```typescript
    const achievementType = getAchievementTypeFromCustomType('ext:LCA_CUSTOM:Learning History:The_Coolest_Dog');
    console.log(achievementType); // Output: The_Coolest_Dog
    ```
3.  **Extract the category type:** Use the `getCategoryTypeFromCustomType` function:

    ```typescript
    const categoryType = getCategoryTypeFromCustomType('ext:LCA_CUSTOM:Learning History:The_Coolest_Dog');
    console.log(categoryType); // Output: Learning History
    ```
