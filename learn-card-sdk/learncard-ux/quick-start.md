---
description: >-
  Get started quickly with reusable UX components for visualizing and
  interacting with verifiable credentials.
---

# Quick Start

### Install

```bash
pnpm install @learncard/react
```

### Usage

```tsx
import React, { useState, useEffect } from "react";
import '@learncard/react/dist/base.css'; // if not already using tailwind
import '@learncard/react/dist/main.css';
import { initLearnCard } from "@learncard/core";
import { VCCard } from "@learncard/react";
import { VC } from "@learncard/types";

const Test = () => {
    const [vc, setVc] = useState<VC | null>(null);
    
    useEffect(() => {
        const getVc = async () => {
            const learnCard = await initLearnCard({ seed: 'a' }); // Bad practice! You should be generating keys...
            const uvc = learnCard.invoke.newCredential();
            setVc(await learnCard.invoke.issueCredential(uvc));
        };
        
        getVc();
    }, []);
    
    if (!vc) return <>Generating Credential...</>; // Loading placeholder while credential is generated
    
    return <VCCard credential={vc} />; // Show card for the generated credential with validation results
};
```

### Styles

`@learncard/react` uses [tailwind](https://tailwindcss.com/) for styles, and exports two css files for consumers: `base.css` and `main.css`. If you are already using Tailwind, you do not need to import `base.css`, as it is simply re-exposing `@tailwind base` and `@tailwindcss/components`. However, you _will_ need to import `main.css`, because it imports the tailwind classes used by our components, as well as our bespoke CSS classes.\


**If using Tailwind already**

```
import '@learncard/react/dist/main.css';
```

**If not using Tailwind already**

```
import '@learncard/react/dist/base.css';
import '@learncard/react/dist/main.css';
```
